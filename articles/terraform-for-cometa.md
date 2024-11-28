---
title: 'COMETA の dbtメタデータ連携に必要なものを Terraform でそろえる'
emoji: '🦁'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['cometa', 'terraform', 'dbt']
published: false
---

## はじめに

ドキュメント、やってみたの記事があるので、それらにそっていけばやりたいことはできると思いますが、ここでは Terraform を使って COMETA に必要なリソースを作成する方法を紹介します。

https://documents.trocco.io/cometa/docs/dbt-metadata-integration

https://qiita.com/hgkcho/items/5044e68c4e62c3a9d1e6

https://zenn.dev/datum_studio/articles/ab77d427ab1e8f

## S3 バケットを作成する

dbt artifacts を保存する S3 バケットを作成します。

```hcl:main.tf
resource "aws_s3_bucket" "cometa_dbt_artifacts" {
  bucket = "<unique-bucket-name>"
}

output "cometa_dbt_artifacts_bucket_name" {
  value = aws_s3_bucket.cometa_dbt_artifacts.bucket
}
```

S3 のバケット名はユニークなものにしましょう。
output ブロックでバケット名を出力しておきます。COMETA の設定画面で使います。

## IAM ロールを作成する

COMETA が S3 バケットにアクセスするための IAM ロールを作成します。

付与が必要な権限は `s3:GetObject` です。

```hcl:main.tf

variable "COMETA_AWS_ACCOUNT_ID" {
  type = string
  description = "COMETA の AWS アカウント ID (12桁の数字)"
}

variable "EXTERNAL_ID" {
  type = string
  description = "外部 ID (任意の文字列)"
}

resource "aws_iam_role" "cometa_role" {
  name = "cometa-role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [
      {
        Effect = "Allow",
        Principal = {
          AWS = var.COMETA_AWS_ACCOUNT_ID
        },
        Action = "sts:AssumeRole",
        Condition = {
          StringEquals = {
            "sts:ExternalId" = var.EXTERNAL_ID
          }
        }
      }
    ]
  })
}

resource "aws_iam_policy" "cometa_policy" {
  name = "cometa-policy"
  path = "/"
  policy = jsonencode({
    Version = "2012-10-17",
    Statement = [
      {
        Effect = "Allow",
        Action = [
          "s3:GetObject",
        ],
        Resource = [
            aws_s3_bucket.cometa_dbt_artifacts.arn,
            "${aws_s3_bucket.cometa_dbt_artifacts.arn}/*"
        ],
      }
    ]
  })
}

resource "aws_iam_role_policy_attachment" "cometa_policy_attachment" {
  role = aws_iam_role.cometa_role.name
  policy_arn = aws_iam_policy.cometa_policy.arn
}

output "cometa_iam_role_name" {
  value = aws_iam_role.cometa_role.arn
}
```

COMETA_AWS_ACCOUNT_ID は COMETA の設定画面で確認できます。

output ブロックで ARN を出力しておきます。COMETA の設定画面で使います。
外部 ID も COMETA 上で入力する必要があるので使えるようにしておいてください。

---

ここまでくれば COMETA に必要な情報は揃いました。

- IAM ロール ARN
- 外部 ID
- S3 バケット名 (バケット直下にファイルを置くのでパスプレフィックスは空にしておきます。)

ここからは余興です。S3 バケットに dbt artifacts が置ければどうやったっていいです。

## GitHub Actions 用の IAM ロールを作成する

S3 バケットに dbt artifacts を置く必要があります。ここでは GitHub Actions を使います。

```hcl:main.tf

locals {
  owner = "<your-github-username>"
  repo = "<your-repo-name>"
}


resource "aws_iam_openid_connect_provider" "github_actions_provider" {
  url             = "https://token.actions.githubusercontent.com"
  client_id_list  = ["sts.amazonaws.com"]
  thumbprint_list = ["0123456789012345678901234567890123456789"]
}

resource "aws_iam_role" "github_actions_role" {
  name = "github-actions-role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17",
    Statement = [
      {
        Effect = "Allow",
        Principal = {
          Federated = aws_iam_openid_connect_provider.github_actions_provider.arn
        },
        Action = "sts:AssumeRoleWithWebIdentity",
        Condition = {
          StringEquals = {
            "token.actions.githubusercontent.com:aud" : "sts.amazonaws.com"
          }
          StringLike = {
            "token.actions.githubusercontent.com:sub" : "repo:${locals.owner}/${locals.repo}:*"
          }
        }
      }
    ]
  })
}

resource "aws_iam_policy" "github_actions_policy" {
  name        = "github-actions-policy"
  path        = "/"
  description = "Policy for GitHub Actions"
  policy = jsonencode({
    Version = "2012-10-17",
    Statement = [
      {
        Effect = "Allow",
        Action = [
          "s3:Get*",
          "s3:List*",
          "s3:Put*",
          "s3:Delete*"
        ],
        Resource = [
          aws_s3_bucket.dbt_artifacts.arn,
          "${aws_s3_bucket.dbt_artifacts.arn}/*"
        ],
      }
    ]
  })
}

resource "aws_iam_policy_attachment" "github_actions_policy_attachment" {
  name       = "github-actions-policy-attachment"
  policy_arn = aws_iam_policy.github_actions_policy.arn
  roles      = [aws_iam_role.github_actions_role.name]
}

output "github_actions_role_arn" {
  value = aws_iam_role.github_actions_role.arn
}
```

GitHub Actions の IAM ロールの ARN を出力しておきます。
`dbt docs generate` をするリポジトリに secrets として登録しておきましょう。
上で作成した S3 バケット名も secrets として登録しておきます。

## GitHub Actions を作成する

GitHub Actions で dbt を実行するためのワークフローを作成します。

```yaml:.github/workflows/upload-dbt-artifacts.yml
name: upload dbt artifacts to S3

on:
  workflow_dispatch:

jobs:
  dbt:
      runs-on: ubuntu-latest
      steps:
        - name: Checkout
          uses: actions/checkout@v4
        - name: Setup Python
          uses: actions/setup-python@v5
          with:
            python-version: '3.11'
        - name: Install dbt
          run: pip install dbt-snowflake # Snowflake を想定しています。自分たちの環境に合わせてください。
        - name: dbt deps
          run: dbt deps
        - name: dbt docs generate
          run: dbt docs generate # profile や target は適宜設定してください。
        - name: copy necessary files
          run: |
            mkdir -p deploy
            cp -r target/manifest.json target/catalog.json deploy/
        - name: Configure AWS credentials
          uses: aws-actions/configure-aws-credentials@v4
          with:
            role-to-assume: ${{ secrets.GITHUB_ACTIONS_ROLE_ARN }}
            aws-region: ap-northeast-1
        - name: Upload dbt artifacts to S3
          run: aws s3 sync deploy/ s3://${{ secrets.BUCKET_NAME }}/ --delete
```

2 つの secrets を設定するのを忘れないでください。
workflow_dispatch をトリガーにしているので、手動で実行することができます。

## TROCCO で GitHub Actions を動かす

手動実行だと寂しいので、このワークフローを TROCCO からキックしてみましょう。スケジュールをトリガーにするのもいいと思います。

```diff yaml:.github/workflows/dbt.yml
on:
-  workflow_dispatch:
+  repository_dispatch:
+    types: [trocco]
```

TROCCO ワークフローから GitHub Actions を動かすための Fine-grained tokens を作成します。
**必要な権限は `contents:write` です。** これだけを設定して作成してください。

TROCCO のワークフロー機能から HTTP リクエストのタスクを設定します。

![](/images/trocco-workflow-1.png)

\$owner\$ と \$repo\$ は変数になっています。自分のものに変更してください。

HTTP リクエストボディは GitHub Actions の repository_dispatch の types で指定したものと一致している必要があります。

```json
{
  "event_type": "trocco"
}
```

![](/images/trocco-workflow-2.png)
| キー | 値 |
| --- | --- |
| Accept | application/vnd.github+json |
| Authorization | Bearer <fine-grained token> |
| Content-Type | application/json |

![](/images/trocco-workflow-3.png)
_ワークフローの図_

ここでは dbt ジョブが終わったあとに GitHub Actions を動かしています。

## おわりに

COMETA に必要なリソースを Terraform で作成する方法(あとその他余興)を紹介しました。

自分自身が Snowflake のリソースを Terraform に載せている最中、ちょうど COMETA の dbt 連携ができるようになりました。
ついでにというテンションで COMETA 用の AWS リソースを作成してみるのは Terraform 初心者の自分にとってはいい練習でした。

コンソールから作ろうが、コードから作ろうがどちらでもいいのですが、

---

いかかでしたでしょうか。おしまい。

Zenn にも COMETA のアイコンほしいな〜

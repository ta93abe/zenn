---
title: 'dbt docs を Cloudflare Pages でホスティングする。'
emoji: '📄'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['dbt', 'cloudflare', 'githubactions']
published: true
---

## はじめに

dbt が生成するドキュメントを Cloudflare Pages でホスティングする方法を紹介します。

## Cloudflare Pages アプリケーションの作成

https://www.cloudflare.com/ja-jp/developer-platform/pages/

Cloudflare Pages にログインし、新しいアプリケーションを作成します。

1. Create application
2. Pages タブを選択
3. Connect to Git
4. リポジトリの選択
5. ビルド設定 (Build は GitHub Actions で行うので、この時点では設定しない)
6. Save and Deploy
7. **Cancel Deployment → Cancel Build**
8. Continue to project → Continue

ここまで行うと、まだデプロイされていない Cloudflare Pages のアプリケーションが作成されます。

ビルド&デプロイは GitHub Actions で行うので、`[プロジェクト名] > Setting > Builds & deployments` から Production branch の自動デプロイを無効にします。

![](/images/cloudflare-pages-automatic-deployment.png)

## Cloudflare Access の設定

Cloudflare Access を使って、Cloudflare Pages にアクセス制限をかけることができます。Cloudflare Pages の `[プロジェクト名] > Manage > Access Policy` の `Enable access policy` を有効にすると、Preview Depolyment にアクセス制限がかかります。**ただしこれは Preview Depolyment にのみ有効で、Production Depolyment には適用されません。**

そこで、Preview Depolyment にもアクセス制限をかけるために、Cloudflare Access を設定します。`Access Policy > Manage Polices` から Cloudflare Access にとび、該当のアプリケーションを設定します。`[プロジェクト名] - Cloudflare Pages` という命名になっています。

Overview > Application Configuration から Application domain を追加します。`+ Add domain` で追加すると、`[id].pages.dev` が自動で追加されます。保存すると Preview Depolyment だけでなく、Production Depolyment にもアクセス制限がかかるようになります。

デフォルトでは One-time PIN 認証をできますが、その他の認証方法も設定できます。

## GitHub Actions の設定

Cloudflare Pages では自動デプロイを OFF にしているので、GitHub Actions でビルド&デプロイを行います。

2 つのワークフローを作成します。

### Push されたときにプレビューデプロイを行うワークフロー

```yaml
name: Deploy Preview
on:
  push:
    branches-ignore: [main]
jobs:
  preview:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install Dependencies
        run: dbt deps
      - name: Build dbt
        run: dbt build
      - name: Build dbt docs
        run: dbt docs generate
      - name: Copy files
        run: |
          mkdir -p docs
          cp -r target/*.json target/index.html docs/
      - name: Deploy to Cloudflare Pages (Preview)
        uses: cloudflare/wrangler-action@v3
        with:
          apiToken: ${{ secrets.CLOUDFLARE_API_TOKEN }}
          accountId: ${{ secrets.CLOUDFLARE_ACCOUNT_ID }}
          command: pages deploy docs --project-name=${{ secrets.CLOUDFLARE_PAGES_PROJECT_NAME }}
```

- `CLOUDFLARE_API_TOKEN` は Cloudflare API トークンです。
  https://developers.cloudflare.com/fundamentals/api/get-started/create-token/
- `CLOUDFLARE_ACCOUNT_ID` は Cloudflare アカウント ID です。Cloudflare のダッシュボードの URL に含まれています。
- `CLOUDFLARE_PAGES_PROJECT_NAME` は Cloudflare Pages のプロジェクト名です。
- dbt の profile も適切に設定してください。

このワークフローが起動すると、GitHub の Pull Request に Preview デプロイの URL が表示されます。すごく便利です。

![](/images/preview-on-pr.png)

### main ブランチにマージされたときに本番デプロイを行うワークフロー

```yaml
name: Deploy Production
on:
  push:
    branches: [main]
jobs:
  production:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      deployments: write
    steps:
      - uses: actions/checkout@v4
      - name: Install Dependencies
        run: dbt deps
      - name: Build dbt
        run: dbt build
      - name: Build dbt docs
        run: dbt docs generate
      - name: Copy files
        run: |
          mkdir -p docs
          cp -r target/*.json target/index.html docs/
      - name: Deploy to Cloudflare Pages (Preview)
        uses: cloudflare/wrangler-action@v3
        with:
          apiToken: ${{ secrets.CLOUDFLARE_API_TOKEN }}
          accountId: ${{ secrets.CLOUDFLARE_ACCOUNT_ID }}
          command: pages deploy docs --project-name=${{ secrets.CLOUDFLARE_PAGES_PROJECT_NAME }}
```

jobs 自体は Preview デプロイと同じですが、こちらは main ブランチにマージされたときにのみ実行されるように設定しています。main ブランチが Cloudflare Pages における Production Branch になっている[^1]ので、このワークフローが実行されると本番デプロイが行われます。

自分自身は dbt docs をホスティングする以外のことを GitHub Actions で行っているので、ワークフローを分けていますが、push をトリガーにしてまとめてもいいかもしれません。

`cloudflare/pages-action` といういかにもなアクションもありますが、`cloudflare/wrangler-action` を使っています。

https://github.com/cloudflare/wrangler-action?tab=readme-ov-file#deploy-your-pages-site-production--preview

## おわりに

今回紹介した方法は個人的には、dbt Cloud、Private GitHub Pages (GitHub Enterprise) の次くらいに簡単な方法だと思っています。ある程度の規模であれば、無料におさまります。

ただ先人たちが S3 や Cloud Run などでホスティングする方法を紹介しているので、それらも参考にしてみてください。

[^1]: [プロジェクト名] > Setting > Builds & deployments > Branch deployment controls から Production branch を確認できます。変更もできます。

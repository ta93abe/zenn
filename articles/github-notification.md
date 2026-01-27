---
title: "GitHubの通知を受け取る完全ガイド - メール・Slack・モバイルアプリ"
emoji: "🔔"
type: "tech"
topics: ["GitHub", "notification", "Slack", "email", "モバイル"]
published: false
---

## はじめに

「レビュー依頼に気づかず、開発が止まってしまった…🤦」
「毎日大量の通知メールが届いて、重要な情報が埋もれてしまう…✉️」
「結局どの通知設定がベストなのか、誰か教えて…！」

GitHubを使っている開発者なら、誰しも一度は**通知**に関する悩みにぶつかったことがあるのではないでしょうか。

GitHubの通知は、適切に設定すれば開発を加速させる強力な武器になります。しかし、設定項目が多岐にわたるため、最適な設定を見つけるのは至難の業です。

この記事を読めば、そんな複雑なGitHub通知を完全に理解し、自分やチームに合わせて自在にカスタマイズできるようになります。

### この記事を読んでわかること

- GitHub通知の基本的な仕組み（Watching, Participating, @mentionsの違い）
- メール、Slack、モバイルアプリ、それぞれの通知設定方法と特徴
- 通知疲れを防ぎ、重要な情報だけを受け取るためのベストプラクティス
- 個人開発からチーム開発まで、シーン別のおすすめ通知設定例
- よくある通知のトラブルシューティング

### 対象読者

- GitHubの通知設定がよくわかっていない初心者の方
- 大量の通知にうんざりしている方
- チーム開発の通知ルールを整備したいと考えている方
- 自分にとって最適な通知設定を見つけたいすべての人

さあ、あなたもこの記事で「GitHub通知マスター」への第一歩を踏み出しましょう！

## GitHub通知の基本を理解する

GitHubの通知には、大きく分けて3つの購読レベルがあります。これを理解することが、通知をマスターする第一歩です。

| レベル | アイコン | 対象 | 説明 |
|:---:|:---:|---|---|
| **Watching** | 👁️ | リポジトリ全体 | リポジトリの**すべての**更新（Issue、PR、コメント等）が通知されます。「All Activity」設定がこれにあたります。 |
| **Participating** | ✅ | 自分が関与したスレッド | 自分がコメントした、@メンションされた、アサインされたIssueやPRなど、**自分が参加している会話**に関する通知が届きます。 |
| **@mentions** | 🗣️ | 自分宛のメンション | 自分のユーザー名（`@username`）や所属チーム名がメンションされた時**だけ**通知されます。 |

多くのリポジトリでは、デフォルトで **Participating** と **@mentions** が有効になっています。つまり、何もしなくても、自分に関係のある通知は届くように設計されています。

### 自動的に通知対象になるケース

具体的には、以下のようなアクションを行うと、自動的にそのスレッドの通知が「Participating」として届くようになります。

- Issueやプルリクエストに自分がアサインされた
- Issueやプルリクエストを自分が作成した
- 自分が作成した、あるいはコメントしたスレッドに新しいコメントがついた
- 自分のユーザー名や所属チームが@メンションされた
- Issueやプルリクエストのステータスを変更した（クローズ、マージなど）

### 通知の保持期間

- **受信トレイの通知**: 5ヶ月間保持されます。
- **保存済み（Saved）の通知**: 無期限に保持されます。

---

## 方法1: メール通知 ✉️

Slackやモバイルアプリが主流の今、「なぜメール通知？」と思うかもしれません。しかし、メール通知には他の方法にはない大きなメリットがあります。

**メール通知のメリット:**
- **網羅性:** すべての通知を受け取ることができる、唯一の方法です。
- **検索性:** メーラーの強力な検索機能を使って、過去の特定の通知を簡単に見つけ出せます。
- **永続性:** GitHubを離れても、自分のメールボックスに記録として残ります。

**メール通知のデメリット:**
- **リアルタイム性の低さ:** Slackやプッシュ通知に比べると、確認が遅れがちです。
- **情報量の多さ:** 設定を誤ると、大量のメールに埋もれてしまいます。

これらの特性を理解し、**「普段はSlack/アプリ、後からまとめて確認・検索したいものはメール」**のように使い分けるのが賢い選択です。

### 通知設定へのアクセス

まずは、すべての基本となる通知設定画面にアクセスしましょう。

1.  GitHubにログインした状態で、右上のプロフィールアイコンをクリック
2.  **Settings** を選択
3.  左サイドバーから **Notifications** をクリック

または、以下のURLから直接アクセスできます。
[https://github.com/settings/notifications](https://github.com/settings/notifications)

### 基本設定

#### 通知先メールアドレスの設定

**Default notification email** セクションで、通知を受け取るメールアドレスを選択できます：

- プライマリメールアドレス
- 登録済みの他のメールアドレス
- `noreply@github.com` を使用してプライバシーを保護

#### Watching repositories（自動監視）

**Automatically watch repositories** を有効にすると、以下の場合に自動的にリポジトリをWatchします：

- 新しくリポジトリを作成した時
- リポジトリへのプッシュアクセス権を付与された時
- リポジトリのコラボレーターになった時

:::message info
**「Automatically watch repositories」設定の変更**
以前は、リポジトリへのプッシュアクセス権を付与されると自動的にそのリポジトリの監視が開始される「Automatically watch repositories」という設定がありました。しかしこの機能は、意図しない通知を増やす原因となっていたため、2022年10月に廃止されました。
現在は、新規作成したリポジトリやコラボレーターとして参加したリポジトリを自動で監視するかどうか、より細かく制御できるようになっています。定期的にご自身の[通知設定](https://github.com/settings/notifications)を見直すことをお勧めします。
:::

#### メール通知の頻度設定

**Email notification preferences** で以下を設定できます：

- **Include your own updates**: 自分自身の更新を通知に含める
- **Comments on Issues and Pull Requests**: Issue/PRのコメント通知
- **Pull Request reviews**: PRレビューの通知
- **Pull Request pushes**: PRへのプッシュ通知
- **CI activity**: CI/CDの実行結果通知

### 個別リポジトリの通知設定

リポジトリごとに通知設定をカスタマイズできます：

1. リポジトリのページを開く
2. 右上の **Watch** または **Unwatch** ボタンをクリック
3. 以下から選択：
   - **Participating and @mentions**: 参加中とメンションのみ
   - **All Activity**: すべての活動
   - **Ignore**: 無視
   - **Custom**: カスタム設定

#### Custom設定の詳細

Custom を選択すると、以下の項目を個別に設定できます：

- Issues
- Pull Requests
- Releases
- Discussions
- Security alerts

### メール通知のフィルタリング

GitHubからのメールには特定のヘッダーが含まれており、メールクライアントでフィルタリングできます：

- `List-ID`: リポジトリを識別
- `X-GitHub-Reason`: 通知理由（mention, review_requested等）
- `X-GitHub-Recipient`: 受信者

#### Gmail でのフィルタ例

```
from:notifications@github.com
to:あなたのメールアドレス
```

このフィルタで特定のラベルを付けたり、フォルダに振り分けたりできます。

### おすすめの設定

#### 個人開発者向け

- 自分のリポジトリ: **All Activity**
- 他人のリポジトリ: **Participating and @mentions**
- CI activity: 有効

#### チーム開発向け

- チームリポジトリ: **Custom**（Issues, PRs, Releases のみ）
- Pull Request reviews: 有効
- Automatically watch repositories: 無効（手動で管理）

#### オープンソースコントリビューター向け

- コントリビュート先: **Participating and @mentions**
- メインのリポジトリのみ All Activity
- メールフィルタリングを活用

---

## 方法2: チャット連携で開発を加速する (Slack / Teams) 🚀

チーム開発において、Slackは今や欠かせないコミュニケーションツールです。GitHubとSlackを連携させることで、開発に関するコミュニケーションをSlackに集約し、チームの生産性を劇的に向上させることができます。

**なぜSlack連携が強力なのか？**
- **コミュニケーションの集約:** PRのレビュー依頼やディスカッションがSlackに通知されることで、会話が活性化し、開発スピードが向上します。
- **コンテキストの共有:** 「このPR、どういう経緯だっけ？」という時に、通知からワンクリックでGitHubに飛べるため、背景の確認が容易になります。
- **アクションの迅速化:** Slack上でIssueを立てたり、PRをマージしたりと、簡単な操作ならGitHubを開く必要さえありません。

このセクションでは、GitHub公式のSlackアプリを使った連携方法を解説します。

### 2-1. Slackとの連携

SlackのGitHubアプリを使って、特定のリポジトリの活動をSlackチャンネルに通知できます。

#### インストールと初期設定

**1. アプリのインストール**

1. https://slack.github.com/ にアクセス
2. **Install** ボタンをクリック
3. GitHubアカウントでログイン
4. リポジトリへのアクセス権限を設定
   - **All repositories**: すべてのリポジトリ（推奨）
   - **Only select repositories**: 特定のリポジトリのみ

**2. SlackチャンネルにGitHubボットを追加**

通知を受け取りたいSlackチャンネルで以下を実行：

```
/invite @github
```

**3. GitHubアカウントとの連携**

```
/github signin
```

表示されたリンクをクリックして認証を完了してください。

#### リポジトリの購読

**購読開始:**
```
/github subscribe owner/repo
```

**例:**
```
/github subscribe facebook/react
/github subscribe your-org/your-api
```

**購読解除:**
```
/github unsubscribe owner/repo
```

**購読状態の確認:**
```
/github subscribe list
```

#### デフォルトで有効な通知

リポジトリを購読すると、以下の通知が自動的に有効になります：

- **Issues**: 新規作成、クローズ、再オープン
- **Pull Requests**: 新規作成、マージ完了、ドラフトが「Ready for review」に変更
- **Commits**: デフォルトブランチへのプッシュ
- **Releases**: 新しいリリースの公開
- **Deployments**: デプロイステータスの更新

#### オプション機能の追加

デフォルトでは無効になっている機能を有効化できます：

```
/github subscribe owner/repo reviews          # レビューコメント
/github subscribe owner/repo comments         # Issue/PRコメント
/github subscribe owner/repo workflows        # GitHub Actions
/github subscribe owner/repo branches         # ブランチ作成・削除
/github subscribe owner/repo discussions      # Discussions
```

**複数機能の同時購読:**
```
/github subscribe owner/repo reviews comments workflows
```

#### 高度なフィルタリング

**ブランチフィルタ:**
```
/github subscribe owner/repo commits:main           # mainブランチのみ
/github subscribe owner/repo commits:feature/*      # feature/*ブランチ
/github subscribe owner/repo commits:*              # すべてのブランチ
```

**ラベルフィルタ:**
```
/github subscribe owner/repo +label:"priority:high"
/github subscribe owner/repo +label:"bug"
```

:::message alert
ラベルフィルタは1リポジトリにつき**1つ**のみ設定可能です。
:::

**ワークフローフィルタ:**
```
/github subscribe owner/repo workflows:{name:"CI"}
/github subscribe owner/repo workflows:{branch:"main",event:"push"}
```

:::message info
**GitHub Actionsのワークフロー通知に関する変更**
以前は、GitHub Actionsのワークフローが実行されると、各ジョブの開始、進行中、完了といった詳細なステータスがSlackに通知されていました。しかし、現在（2023年以降）は、通知の量が最適化され、基本的に**ワークフロー全体の開始と完了（成功または失敗）のみ**が通知される仕様になっています。

これにより、通知チャンネルがジョブごとの細かいメッセージで溢れるのを防ぎ、重要な結果（デプロイの成否など）に集中しやすくなりました。
:::

### 2-2. Microsoft Teamsとの連携

Microsoft Teamsを利用しているチームでも、Slackとほぼ同様の強力な連携が可能です。

#### インストールと初期設定

**1. アプリのインストール**

1.  Microsoft Teamsのアプリストアで「GitHub」を検索します。
2.  **GitHub** アプリ（発行元がGitHub）を選択し、チームやチャネルに追加します。

**2. GitHubアカウントとの連携**

通知を受け取りたいチャネルで、`@GitHub signin` とメンションし、表示される手順に従ってGitHubアカウントを認証します。

:::message
Teamsの場合、コマンドは `/` ではなく、`@GitHub` のように、**ボットへのメンション**で開始します。
:::

#### リポジトリの購読と管理

基本的なコマンドはSlackと共通ですが、開始が `@GitHub` になります。

- **購読の開始:** `@GitHub subscribe owner/repo`
- **購読の解除:** `@GitHub unsubscribe owner/repo`
- **購読リストの表示:** `@GitHub subscribe list`

#### 利用できる機能

Slack連携と同様に、以下の機能が利用できます。

- **詳細な通知:** `reviews`, `comments`, `branches` などを追加で購読できます。
- **フィルタリング:** ラベル（`+label:"bug"`）やブランチ（`commits:main`）でのフィルタが可能です。
- **チャネルからの操作:** 通知からIssueをクローズしたり、コメントを追加したりできます。
- **リンクの展開:** GitHubのURLを貼り付けると、詳細なプレビューが表示されます。

機能的にはSlack連携とほとんど差がないため、チームで利用しているチャットツールに合わせて選択してください。

コマンドの組み合わせで、チームの特性に合わせた柔軟な通知システムを構築できます。ここでは、3つの異なるタイプのチームを例に、具体的な設定例を紹介します。

**【タイプA】少数精鋭のスタートアップ開発チーム**

- **課題:** スピードが命。PRのレビュー遅延をなくし、デプロイの状況は全員がリアルタイムで把握したい。
- **チャンネル:** `#dev-team`

```bash
# まず、リポジトリの基本的な通知を購読
/github subscribe your-org/main-product

# デプロイ状況は知りたいが、Issueやコミットの通知は不要
/github unsubscribe your-org/main-product issues commits

# PRのレビューに関する通知はすべて受け取る
/github subscribe your-org/main-product reviews comments

# mainブランチにマージされたら通知が欲しい
/github subscribe your-org/main-product commits:main
```

**【タイプB】大規模なマイクロサービス開発チーム**

- **課題:** 多くのリポジトリが乱立。自分のチームに関係ない通知が多く、重要な情報が埋もれがち。
- **チャンネル:** `#backend-team-a` (チームAのチャンネル), `#frontend-team` (フロントエンドチームのチャンネル)

```bash
# チームAが担当するAPIサーバーとWorkerの通知を購読
/github subscribe your-org/api-server-a
/github subscribe your-org/worker-a

# チームAのチャンネルでは、フロントエンドの通知は不要
/github unsubscribe your-org/frontend-app

# 緊急度の高いバグに関する通知だけは、チームの垣根を越えて受け取りたい
/github subscribe your-org/api-server-a +label:"bug"
/github subscribe your-org/frontend-app +label:"bug"
```

**【タイプC】OSSプロジェクトの運用チーム**

- **課題:** コントリビューターからのIssueやPRを素早く検知し、円滑なコミュニケーションを促進したい。
- **チャンネル:** `#oss-maintainers`

```bash
# プロジェクトのすべての公開アクティビティを購読
/github subscribe awesome-org/awesome-project

# 特に、新規のIssueとPR、ディスカッションを重視
/github subscribe awesome-org/awesome-project issues pulls discussions

# 新規コントリビューターを歓迎するため、ブランチ作成も通知
/github subscribe awesome-org/awesome-project branches

# 「good first issue」ラベルが付いたIssueは、コントリビューター向けチャンネルにも通知したい
# (別チャンネル `#oss-contributors` で)
/github subscribe awesome-org/awesome-project issues:{label:"good first issue"}
```

**マルチリポジトリ管理:**

チャンネル `#frontend-notifications`:
```bash
/github subscribe your-org/web-app
/github subscribe your-org/mobile-app
/github subscribe your-org/design-system
```

チャンネル `#backend-notifications`:
```bash
/github subscribe your-org/api-server
/github subscribe your-org/worker-service
/github subscribe your-org/database-migrations
```

チャンネル `#releases`:
```bash
/github subscribe your-org/web-app releases
/github subscribe your-org/api-server releases
# 他の通知は無効化
/github unsubscribe your-org/web-app issues pulls commits deployments
/github unsubscribe your-org/api-server issues pulls commits deployments
```

#### 組織全体の購読

個別リポジトリではなく、組織全体を購読することも可能です：

```
/github subscribe your-org
```

:::message
組織全体の購読は通知量が非常に多くなる可能性があります。以下の用途に限定することをおすすめします：
- 小規模な組織（リポジトリ数が少ない）
- セキュリティアラート専用チャンネル
- アーカイブ用途
:::

#### Slackから直接操作

SlackのGitHubアプリでは、通知を受け取るだけでなく、GitHubを直接操作できます。

**Issueの作成:**

メッセージから作成：
1. メッセージの「...」メニューをクリック
2. **Create GitHub Issue** を選択

コマンドから作成：
```
/github open owner/repo
```

**IssueやPRへの操作:**

Slack上の通知から直接、以下の操作ができます：
- コメント追加
- Issueのクローズ/再オープン
- ラベルの追加・削除
- アサイン変更

**ワークフローの承認:**

GitHub Actionsの承認待ちワークフローをSlackから承認・却下できます。

**リンクプレビュー:**

GitHubのURL（Issue、PR、コードスニペット、リポジトリ）をSlackに貼り付けると、自動でリッチプレビューが表示されます。

#### Slack通知のベストプラクティス

**1. チャンネルを目的別に分ける**

推奨構成：
- `#dev-pr-reviews`: PRレビュー専用
- `#dev-releases`: リリース通知専用
- `#dev-ci-alerts`: CI/CD失敗通知専用
- `#dev-security`: セキュリティアラート専用

**2. 段階的に導入**

1. まずPRとレビューのみ有効化
2. チームの反応を見て調整
3. 必要に応じて機能を追加

**3. フィルタを積極的に活用**

- ラベルで優先度を管理（`priority:high`、`urgent`）
- ブランチフィルタでmain/developのみ通知
- ワークフローフィルタでデプロイ関連のみ通知

**4. 通知の命名規則を統一**

Issueラベル：
```
priority:high, priority:medium, priority:low
type:bug, type:feature, type:docs
```

ブランチ命名：
```
feature/*, bugfix/*, release/*, hotfix/*
```

統一することで、フィルタリングが容易になります。

**5. 定期的に見直し**

- 月に1度、通知設定を見直す
- 使われていないチャンネルの購読を解除
- 新しいリポジトリを追加

#### Slack通知のトラブルシューティング

**通知が来ない場合:**

1.  **ボットがチャネルに招待されているか確認**
    -   Slack: `/invite @github`
    -   Teams: チャネルに`@GitHub`が追加されているか確認

2.  **購読が正しく設定されているか確認**
    -   Slack: `/github subscribe list`
    -   Teams: `@GitHub subscribe list`

3. GitHubアプリのリポジトリアクセス権限を確認
   https://github.com/settings/installations

4. プライベートリポジトリの場合、アプリがアクセス権を持っているか確認

**通知が多すぎる場合:**

1. デフォルト機能を選択的に無効化
2. ラベルフィルタで重要なものだけに絞る
3. 専用チャンネルを作成して通知を分散
4. ブランチフィルタでmainブランチのみに制限

**ラベルフィルタが効かない場合:**

注意点：
- ラベル名は**大文字小文字を区別**します
- スペースを含むラベルは**クォートで囲む**必要があります
  ```
  正: /github subscribe owner/repo +label:"good first issue"
  誤: /github subscribe owner/repo +label:good first issue
  ```

**古いGitHub-Slack連携アプリについて**

現在（2023年時点）のGitHubとSlackの連携は「GitHub」という名前のアプリで行われますが、2021年7月以前は別のレガシーな連携方法が存在しました。もし非常に古いセットアップを引き継いで利用している場合で、通知がうまく機能しない場合は、一度連携を解除し、[現在の公式アプリ](https://slack.github.com/)を再インストールすることをおすすめします。


### チャットツールと連携した定期リマインダー（Scheduled Reminders）

「リアルタイム通知だけだと、忙しい時にレビュー依頼を見逃してしまう…」

そんな悩みを解決するのが、**Scheduled Reminders（定期リマインダー）**機能です。指定した曜日・時刻に、レビュー待ちのプルリクエストをまとめて通知してくれます。

この機能は **Slack と Microsoft Teams の両方で利用可能**です。

#### 主な特徴

- 指定した曜日・時刻に定期的に通知
- 最大5つのリポジトリを監視
- リポジトリあたり最大20件の古いPRを表示
- リアルタイムアラートにも対応
- SlackとMicrosoft Teamsに対応

#### 2023年6月のアップデート

2023年6月に、Scheduled Remindersはさらに強化されました。

- **通知対象の拡大**: 監視対象リポジトリあたり最大20件のプルリクエストが通知されるようになりました。
- **リポジトリ選択の柔軟性向上**: 通知対象とするリポジトリを手動で5つまで選択できるほか、組織内で最もプルリクエストのレビュー滞在時間が長いリポジトリを自動で選択させることも可能になりました。
- **透明性の向上**: どのリポジトリが通知対象になっているかが設定画面で明確に確認できるようになりました。

#### 個人用Scheduled Remindersの設定

**前提条件:**
- 組織のオーナーがSlackワークスペースを認証済みであること
- Free、Pro、Teamプランで利用可能

**設定手順:**

1. GitHubの右上のプロフィール写真をクリック
2. **Settings** → **Integrations** → **Scheduled reminders** をクリック
3. 対象の組織の横にある編集アイコンをクリック
4. **Authorize Slack workspace** をクリックして認証
5. 曜日・時刻・タイムゾーンを設定
6. レビューリクエストのタイプを選択（自分宛て、チーム宛て）
7. **Create reminder** をクリック

**テスト送信:**
メガホンアイコンをクリックするとテストリマインダーを送信できます。

#### チーム用Scheduled Remindersの設定

チーム用には、より高度なフィルタリングオプションがあります：

**フィルタリングオプション:**
1. ドラフトPRを除外
2. 明示的なレビューリクエストのみ
3. 承認済みPRを無視
4. 最小PR年齢（作成からの経過時間）
5. 最小停滞時間（最終アクティビティからの経過時間）
6. 特定用語・ラベルを除外
7. 必須ラベルでフィルタ

**設定例（アクティブな開発チーム）:**
```
曜日: 平日
時刻: 10:00 AM
フィルタ:
- ドラフトPRを除外: 有効
- 承認済みPRを無視: 有効
- 最小停滞時間: 24時間
```

#### 活用シーン

**個人開発者向け（朝の業務開始時）:**
```
曜日: 平日
時刻: 9:00 AM
対象: 自分に割り当てられたレビュー
```

**チーム開発向け（デイリースタンドアップ前）:**
```
曜日: 平日
時刻: 9:30 AM
対象: チームに割り当てられたレビュー
フィルタ: 最小停滞時間24時間
```

**リモートチーム向け（タイムゾーン考慮）:**
```
リマインダー1（東京チーム）: 10:00 AM JST
リマインダー2（ヨーロッパチーム）: 10:00 AM CET
```

---

## 方法3: モバイルアプリ通知

GitHub Mobileアプリを使うと、外出先でもリアルタイムでGitHubの通知を受け取れます。

### 利用可能な通知タイプ

GitHub Mobileのプッシュ通知では、以下のイベントを受け取れます：

- **Direct mentions**: 会話内で直接メンションされた時
- **Pull request reviews**: PRのレビューを依頼された時
- **Task assignments**: タスクにアサインされた時
- **Deployment approvals**: 保護された環境へのデプロイ承認を依頼された時

:::message
チームメンションやチームレビューリクエストは、プッシュ通知から自動的に除外されます。
:::

### 設定方法

#### iOS

1. アプリ下部の **Profile** をタップ
2. 設定アイコン（⚙️）をタップ
3. **Notifications** を選択
4. トグルで有効化したい通知タイプをオン/オフ

**Working Hours（稼働時間）の設定:**
1. **Working Hours** をタップ
2. **Custom working hours** トグルをオン
3. 通知を受け取りたい時間帯を設定

#### Android

1. アプリ下部の **Profile** をタップ
2. 設定アイコン（⚙️）をタップ
3. **Configure Notifications** を選択
4. トグルで有効化したい通知タイプをオン/オフ

**Working Hours（稼働時間）の設定:**
iOSと同じ手順で設定できます。

### リポジトリのWatch設定（モバイル）

モバイルアプリから直接、リポジトリのWatch設定をカスタマイズできます：

1. リポジトリのメインページを開く
2. **Watch** ボタンをタップ
3. 以下から選択：
   - **Participating and @mentions**: 参加中とメンションのみ
   - **All Activity**: すべての活動
   - **Ignore**: 無視
   - **Custom**: カスタム設定

**Custom設定:**
- Issues
- Pull Requests
- Discussions（有効な場合）
- Releases

### Working Hours（稼働時間）機能

Working Hoursは、プッシュ通知を受け取りたい時間帯を指定できる機能です。

**活用例:**
- 平日の9:00 - 18:00のみ通知を受け取る
- 週末は通知をオフにする
- 深夜の通知を避ける

これにより、ワークライフバランスを保ちながら、重要な通知を見逃さない環境を作れます。

### 通知の管理

モバイルアプリの通知受信箱では、以下の操作ができます：

- **Done**: 受信箱から削除（`is:done`フィルタで後から確認可能）
- **Saved**: 重要な通知を保存（無期限に保持）
- **Read/Unread**: 既読/未読のマーク
- **Unsubscribe**: その会話の今後の通知を停止

### 注意点

**GitHub Enterprise Serverの場合:**
バックグラウンドフェッチを使用してプッシュ通知をサポートしているため、通知の受信に遅延が発生する可能性があります。

---

## 通知方法の比較と選び方

### 各方法の特徴

| 方法 | リアルタイム性 | 詳細度 | フィルタリング | チーム向け | 外出先 |
|------|--------------|--------|--------------|----------|--------|
| **メール** | 中 | ◎ | ◎ | △ | ○ |
| **Slack/Teams連携** | ◎ | ○ | ◎ | ◎ | △ |
| **Scheduled Reminders** | △ | ○ | ◎ | ◎ | △ |
| **モバイルアプリ** | ◎ | △ | ○ | △ | ◎ |

### 用途別のおすすめ組み合わせ

#### パターン1: 個人開発者

- **メール**: Participating and @mentions
- **モバイルアプリ**: Direct mentions、Review requests
- **Working Hours**: 平日 9:00-18:00

**理由**: 個人で複数のプロジェクトに参加している場合、メールで詳細を確認しつつ、緊急の依頼はモバイルで即座に対応できます。

#### パターン2: チーム開発（Slack中心）

- **Slack/Teams連携**: PRとレビューのみ（`#pr-reviews`チャンネル）
- **Scheduled Reminders**: 平日 10:00 AM（チーム全体）
- **メール**: 最小限（@mentionsのみ）
- **モバイルアプリ**: Review requests

**理由**: チームのコミュニケーションをSlackに集約し、定期リマインダーでレビュー漏れを防ぎます。

#### パターン3: DevOpsチーム

- **Slack/Teams連携**: Workflows、Deployments（`#ci-alerts`チャンネル）
- **メール**: Security alerts、CI activity
- **モバイルアプリ**: Deployment approvals

**理由**: CI/CDの状態をリアルタイムで監視し、デプロイ承認は外出先でも対応できるようにします。

#### パターン4: オープンソースメンテナー

- **メール**: Custom（Issues、PRs、Releases のみ）
- **Slack/Teams連携**: +label:"good first issue"（コントリビューター向け）
- **モバイルアプリ**: Direct mentions
- **Scheduled Reminders**: 週2回（月・木 10:00）

**理由**: 大量の通知をフィルタリングしつつ、重要なコントリビューションやメンションは即座に対応します。

#### パターン5: マネージャー・プロダクトオーナー

- **メール**: Releases、Security alerts
- **Slack/Teams連携**: +label:"priority:high"（`#product-alerts`チャンネル）
- **モバイルアプリ**: オフ（または@mentionsのみ）

**理由**: 技術的な詳細は追わず、リリースや重要なIssueのみを把握します。

---

## 通知管理のベストプラクティス

### 1. 通知疲れを防ぐ

**問題:**
すべての通知を受け取ると、重要な情報が埋もれてしまいます。

**対策:**
- デフォルトは **Participating and @mentions** に設定
- 重要なリポジトリのみ **Custom** で細かく設定
- ラベルを活用して優先度を可視化（`priority:high`、`urgent`）
- Working Hoursで通知時間を制限

### 2. 通知の優先度付け

**即座に対応すべき通知:**
- Review requests（モバイルアプリ + Slack/Teams）
- Deployment approvals（モバイルアプリ）
- Security alerts（メール + Slack/Teams）

**定期的に確認する通知:**
- Issues（メール）
- Scheduled Reminders（Slack/Teams）
- Releases（メール）

**必要に応じて確認する通知:**
- Commits（メール、フィルタリング済み）
- Discussions（メール）

### 3. 命名規則とラベルの統一

**Issueラベル:**
```
priority:high, priority:medium, priority:low
type:bug, type:feature, type:docs
status:blocked, status:in-progress
```

**ブランチ命名:**
```
feature/*, bugfix/*, release/*, hotfix/*
```

統一することで、フィルタリングが容易になります。

### 4. 定期的な見直し

**月次レビュー:**
- 受信した通知の種類と量を確認
- 不要な通知を無効化
- 新しいリポジトリの購読設定を追加
- ラベルフィルタの効果を検証

**四半期レビュー:**
- チーム全体の通知設定を見直し
- Slackチャンネルの整理
- Scheduled Remindersの時間帯調整

### 5. チーム全体での統一

**推奨される統一ルール:**
- 重要なPRには必ず `priority:high` ラベルを付ける
- レビュー依頼は明示的に行う（@mention）
- ドラフトPRは通知対象外
- リリース前には必ず通知する

---

## トラブルシューティング

### メール通知が来ない

**確認ポイント:**
1. https://github.com/settings/notifications でメールアドレスを確認
2. スパムフォルダを確認
3. リポジトリのWatch設定を確認
4. `notifications@github.com` からのメールを許可リストに追加

### Slack/Teamsで通知が来ない

**確認ポイント:**
1. ボットがチャンネルに追加されているか（`/invite @github`）
2. 購読が正しく設定されているか（`/github subscribe list`）
3. GitHubアプリのリポジトリアクセス権限を確認（https://github.com/settings/installations）
4. プライベートリポジトリの場合、アプリがアクセス権を持っているか確認

### モバイル通知が来ない

**確認ポイント:**
1. アプリの通知設定でプッシュ通知が有効か確認
2. デバイスのGitHubアプリ通知権限を確認
3. Working Hoursの設定を確認
4. GitHub Enterprise Serverの場合、バックグラウンドフェッチの遅延の可能性

### 通知が多すぎる

**対処法:**
1. **Automatically watch repositories** を無効化
2. デフォルト通知を **Participating and @mentions** に変更
3.  **Slack/Teamsでラベルフィルタを活用**
4. メールフィルタリングを設定
5. Scheduled Remindersの頻度を減らす

---

## まとめ：通知を制する者が、開発を制す

今回は、複雑で奥が深いGitHubの通知システムについて、網羅的に解説しました。

**この記事のキーポイント:**
- ✅ **通知の3つのレベル（Watching, Participating, @mentions）を理解する**のが第一歩。
- ✅ **メールは「検索・保存用」、Slack/アプリは「リアルタイム用」**と使い分けるのが基本戦略。
- ✅ **Slack連携のフィルタ機能**を使いこなせば、チームに合わせた最適な通知フローを設計できる。
- ✅ **定期的な見直し**を怠らず、常に設定をアップデートし続けることが重要。

完璧な通知設定に、 ஒரே答えはありません。あなたやチームの成長に合わせて、設定も進化させていく必要があります。

**さあ、明日からできる第一歩として、まずはご自身の[通知設定ページ](https://github.com/settings/notifications)を開いてみませんか？**

そして、「Automatically watch repositories」のチェックが外れているかを確認し、普段使っているリポジトリの通知設定を「Participating and @mentions」に変更してみてください。きっと、それだけでもあなたのGitHub体験は、より快適になるはずです。

この記事が、あなたの開発ライフを少しでも豊かにする一助となれば幸いです。
Happy developing! 🚀

## 参考リンク

### 公式ドキュメント

- [GitHub Docs - About notifications](https://docs.github.com/en/subscriptions-and-notifications/concepts/about-notifications)
- [GitHub Docs - Configuring notifications](https://docs.github.com/en/subscriptions-and-notifications/get-started/configuring-notifications)
- [GitHub Docs - Scheduled reminders概要](https://docs.github.com/en/account-and-profile/concepts/scheduled-reminders)
- [GitHub Docs - 個人リマインダーの管理](https://docs.github.com/en/subscriptions-and-notifications/how-tos/managing-your-scheduled-reminders)
- [GitHub Docs - チームリマインダーの管理](https://docs.github.com/en/organizations/organizing-members-into-teams/managing-scheduled-reminders-for-your-team)
- [GitHub Docs - Slack通知のカスタマイズ](https://docs.github.com/en/integrations/how-tos/slack/customize-notifications)

### Slack統合

- [GitHub Slack Integration - 公式リポジトリ](https://github.com/integrations/slack)
- [Slack App Directory - GitHub](https://slack.com/apps/A01BP7R4KNY-github)
- [インストールページ](https://slack.github.com/)

### ブログ記事

- [GitHub Blog - New push notifications on GitHub Mobile](https://github.blog/news-insights/product-news/new-push-notifications-scheduling-releases-github-mobile/)
- [GitHub Blog - More control and clarity in scheduled reminders for pull requests](https://github.blog/changelog/2023-06-12-more-control-and-clarity-in-scheduled-reminders-for-pull-requests/)

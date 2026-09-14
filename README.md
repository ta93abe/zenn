# Zenn Content Repository

このリポジトリは、Zennに投稿する技術記事を管理するためのものです。

## セットアップ

### 必要な環境

- Node.js
- pnpm 10.22.0
- go-task（推奨）

### インストール

```bash
# 依存関係のインストール
pnpm install

# go-taskのインストール（macOS）
brew install go-task
```

## 使い方

### go-taskを使用する場合（推奨）

```bash
# 利用可能なタスクを表示
task

# プレビューサーバーを起動
task preview

# 新規記事を作成
task new:article

# リンターを実行
task lint

# textlintで自動修正
task lint:text:fix

# すべてのチェックを実行
task ci
```

### 直接コマンドを使用する場合

```bash
# プレビューサーバーを起動
npx zenn preview

# 新規記事を作成
npx zenn new:article

# リンターを実行
pnpm run lint

# フォーマット
pnpm run format
```

## 開発ツール

### Linter/校正ツール

- **Oxlint / Oxfmt**: JavaScript/TypeScriptのリンターとフォーマッター
- **textlint**: 日本語校正ツール
  - preset-ja-technical-writing: 技術文書向けルール
  - preset-ja-spacing: スペース関連のルール
- **cspell**: スペルチェッカー

### VSCode推奨拡張機能

`.vscode/extensions.json`を参照してください。

## 参考リンク

- [📘 Zenn CLI Guide](https://zenn.dev/zenn/articles/zenn-cli-guide)

# Zenn Content Repository

このリポジトリは、Zennに投稿する技術記事を管理するためのものです。

## セットアップ

### 必要な環境

- Node.js
- pnpm 10.22.0

### インストール

```bash
pnpm install
```

## 使い方

```bash
# プレビューサーバーを起動
pnpm preview

# 新規記事を作成
pnpm new:article

# リンターを実行
pnpm lint

# textlintで自動修正
pnpm lint:text:fix

# フォーマット
pnpm format
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

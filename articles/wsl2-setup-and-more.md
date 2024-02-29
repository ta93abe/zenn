---
title: "WSL2をインストールして基本的な設定を。"
emoji: "🐥"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["WSL", "WSL2", "Git", "GitHub", "Starship"]
published: true
---

## PowerShell で WSL2 を有効化する

```powershell
wsl --install
```

インストールが完了したら、一旦再起動します。

再起動したら、Ubuntuを起動して、ユーザー名とパスワードを設定します。

Windows Terminalを起動して、設定(Ctrl+,)を開きます。
スタートアップタブから既定のプロファイルをUbuntuに設定しておくと次回からWindows Terminalを起動したときにUbuntuがデフォルトで起動します。

### WSLからWindowsのブラウザを認識させる

`.bashrc`に以下の設定を追加します。

```bash
export BROWSER="pwsh.exe /c start"
```

これでWSLからWindowsのブラウザを開くことができるようになります。

## Starship

https://starship.rs/

```bash
curl -sS https://starship.rs/install.sh | sh
```

`.bashrc`に以下の設定を追加します。

```bash
eval "$(starship init bash)"
```

保存して、Windows Terminalを再起動すると、プロンプトが変わっているはずです。
プロンプトのカスタマイズは、`~/.config/starship.toml`で行います。

https://starship.rs/config/

## Git

```bash
sudo apt update
sudo apt install git
```

最新のGitがインストールされます。

GitのConfigを設定します。

```bash
git config --global user.name "<your-name>"
git config --global user.email "<your-email>"
```

<your-name> は任意ですが、GitHubのユーザー名と同じにしておくと便利です。

## GitHub CLI

ドキュメントに記載の通りにインストールします。

[GitHub CLIのDebianへのインストール](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)

一応コマンドも記載しておきますが、ドキュメントの方が最新です。

```bash
type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y)
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
&& sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
&& sudo apt update \
&& sudo apt install gh -y
```

インストールできたら、認証をしましょう。

```bash
gh auth login
```

ブラウザが開いて、GitHubにログインして認証を行います。
認証が完了したら、Windows Terminalに戻ります。出力の最終行に `✓ Logged in as <your-github-username>` と表示されていれば認証完了です。

## まとめ

開発に必要なミニマムなセットアップしました。(Starshipはオプションですが、おすすめです。)
扱う対象によってはまだ設定が必要だと思いますし、生産性を上げたり、個人の好みに合わせてカスタマイズしていくことでしょう。
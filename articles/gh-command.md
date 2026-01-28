---
title: "ターミナルからGitHubを操る。GitHub CLIガイド"
emoji: "👌"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["github", "cli"]
published: false
---

## GitHub CLIとは？
`gh`は、GitHubが公式に提供しているコマンドラインツールです。Issueの作成、PRの確認、リポジトリの作成など、これまでターミナルとブラウザを行き来していた面倒な作業を、すべてターミナル上で完結させることが出来ます。

## インストールと初期設定
まずは自分の環境に合わせてインストールを行いましょう。

### インストール方法

- Windows
```powershell
winget install GitHub.cli
```

- macOS
```bash
brew install gh
```

- Linux
[公式の各ディストリビューション向けガイド](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)を参照してください。

### 初期設定
インストールが完了したら、GitHubアカウントと連携させます。
```bash
gh auth login
```
1. `GitHub.com`を選択
2. `HTTPS`か`SSH`を選択
3. `Login with a web browser`を選択し、表示されたコードをブラウザに入力して認証を完了させます。

## 主要コマンド集
よく使う操作をカテゴリ別に紹介します。

### リポジトリ操作

## まとめ
GitHub CLI(`gh`)を導入することで、開発フローからブラウザへの切り替えといった面倒な作業を大幅に減らすことが可能です。
この記事がお役に立てば幸いです。快適なターミナルライフを！
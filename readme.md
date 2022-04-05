<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->

# SSH Settings

ここで述べる`Host`と`Client`は

- `Host`が接続されようとしている、sshデーモンが動いているサーバー側
- `Client`が接続しようとしている、"ssh 192..."と打ち込んでいる側

である。


## 最小構成での接続

この手法でグローバル公開などは絶対にしてはいけない。

[最小構成の接続](./docs/ssh_minimal.md)

## 公開鍵認証での接続

最小構成の時のパスワード認証とは異なり、公開鍵認証を行う。

[公開鍵認証での接続](./docs/ssh_pubkey.md)

## Hostの設定

公開鍵認証以外の`/etc/ssh/sshd_config`の設定について

[Hostの設定](./docs/ssh_sshdconfig.md)

## Clientの設定

sshの接続時に`-p`でポートを指定したり、`-i`で秘密鍵を指定するがアクセスするホストごとに規定値を指定することができる。

[Clientの設定](./docs/ssh_sshconfig.md)

## GitHubのSSH接続

おまけ

[GitHubのSSH接続](./docs/ssh_github.md)

<!-- Written by Croyfet in 2022-->

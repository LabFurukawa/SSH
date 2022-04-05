<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->

# SSH 最小構成での接続

## [Host] SSHのインストール

Ubuntuの場合

```
apt install ssh
```

## [Host] sshd(ssh daemon) の起動

Ubuntuの場合

```
service ssh start
```

このほかにも`stop` / `restart` / `status`などのオプションがある。

## [Client] SSHで接続

PowerShell(Windows)やTerminal(Mac、Linux)から

Ubuntuのログインするユーザーが"\_USER\_"、マシンのIPアドレスを"192.168.xx.xx"とした場合、

```
ssh _USER_@192.168.xx.xx
```

この後にパスワードが求められて、接続することができる。

ちなみにユーザーを指定せずに

```
ssh 192.168.xx.xx
```
とするとClientのユーザーがユーザー名として指定される。

Ubuntuではsshdの設定`/etc/ssh/sshd_config`の34行目あたりに
```
#PermitRootLogin prohibit-password
```
とコメントアウト(コメントアウトの設定内容がおそらくデフォルト)されている通り、パスワードのログインは禁止されているがバージョンによっては有効化されているかもしれない。

その場合は

```
ssh root@192.168.xx.xx
```
でrootログインもできる。

---

[Back to home](../readme.md)

<!-- Written by Croyfet in 2022-->

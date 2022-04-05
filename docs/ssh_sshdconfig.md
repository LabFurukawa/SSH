<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->

# Hostの設定

ホスト側の設定をする場合はsshのdaemon、`sshd`の設定をする。

`/etc/ssh/sshd_config`であって`/etc/ssh/ssh_config`ではない。

## 推奨される設定

### Port

sshのデフォルトポートは22だが変更はできる。
ポートスキャニングをされればセキュリティ的な意味はないがポート22のダイレクトな攻撃の対策にはなるだろう。

```
Port _PORT_NUM_
```
### AddressFamily
言うまでもなく絞るべき

### ListenAddress
言うまでもなく絞るべき

### PermitRootLogin

sshのrootでのログインを許可しない設定をすべきである。

```
PermitRootLogin no
```

### PubkeyAuthentication

公開鍵暗号を使った接続をすべきである。sha1で作成されたssh-rsaは脆弱性があるので使用してはいけない。詳細については前項。

```
PubkeyAuthentication yes
```

### AuthorizedKeysFile

前の`PubkeyAuthentication`とセット。

ログインするユーザーのホームディレクトリからの相対パスで指定。絶対パスでも可能。

```
AuthorizedKeysFile _PUBLIC_KEY_
```

### PasswordAuthentication

公開鍵認証を使うなら不要。noに。

```
PasswordAuthentication no
```

### TCPKeepAlive

ネットワーク切断時などに接続を破棄する。デフォルトでyes。

```
TCPKeepAlive yes
```

### ClientAliveInterval

指定秒数おきにClientに応答信号を送りタイムアウトを抑制する。デフォルトは0(送らない)だが120ぐらいだろうか。

```
ClientAliveInterval _SECOND_
```

### ClientAliveCountMax

`ClientAliveInterval`の呼びかけ回数。デフォルト3回なのでそれくらいで。

```
ClientAliveCountMax _COUNT_
```

### UseDNS

ClientのIPを逆引きするが恩恵を感じないのでnoで。

```
UseDNS no
```

---

[Back to home](../readme.md)

<!-- Written by Croyfet in 2022-->

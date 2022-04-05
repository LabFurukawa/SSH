<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->

# SSH 公開鍵認証での接続

## [Client]公開暗号鍵の作成

`ssh-keygen`コマンドで鍵の作成を行う。

ここでssh-keygenで作成できる鍵の種類`key type`と鍵長`key length`が複数ある。

key typeがRSA(`-t rsa`)はSHA-1で作成されたものは脆弱性を有しているため、ややこしさを解決するためここでは説明しない。

ここではkey type : `ed25519`で作成する。固定長なので`-b`は使えない

```
ssh-keygen -t ed25519
```

互換性に問題がある場合はkey type : `ecdsa`のkey length : 256 / 384 / 521で作成する。

```
ssh-keygen -t ecdsa -b 521
```

これにより公開鍵(拡張子が`.pub`)と秘密鍵(拡張子なし)が入手できるはずである。ファイル名は何でも構わない。

## [Host] Client側で作成した公開鍵をHost側に置く

USBメモリなどでClient側で作成した`公開鍵(.pub)`をHost側に置く。
場所はそのユーザーの`~/.ssh`の中に置くのが一般的である。なければ作成する。

パーミッションはそのユーザーが読み込み可能な状態にする必要がある。

そして`/etc/ssh/sshd_config`から

- 39行目あたりの`PubkeyAuthentication`のコメントアウトを外し、yes。
- 42行目あたりの`AuthorizedKeysFile`のコメントアウトを外し、ホームディレクトリから鍵の場所を指定。

```
sudo sshd -t
```
で`/etc/ssh/sshd_config`の構文確認を行う。

```
service ssh restart
```
でサービスを再起動。


## [Client] Clientから公開鍵認証でssh接続

先ほど作成した`秘密鍵`を引数に加え

PowerShell(Windows)やTerminal(Mac、Linux)から

Ubuntuのログインするユーザーが"\_USER\_"、マシンのIPアドレスを"192.168.xx.xx"とした場合、

```
ssh _USER_@192.168.xx.xx -i _SECRET_KEY_PATH_
```

この後に、鍵の作成時に求められたパスワードが求められて、接続することができる。

ちなみに鍵の作成時にパスワードを入れない場合、パスワードなしで接続できる。あまり良くはない。けどするよね。

---

[Back to home](../readme.md)

<!-- Written by Croyfet in 2022-->

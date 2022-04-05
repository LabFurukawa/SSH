<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->

# Clientの設定

Ubuntuの場合は`/etc/ssh/ssh_config`、または直に書き込むのではなく`/etc/ssh/ssh_config.d/`に`*.conf`の形で作成すれば`/etc/ssh/ssh_config`がそれを読み込んでくれる。

またWindowsでは`~/.ssh/config`となっている。`Include`でUbuntuと同様に他のファイルの読み込みもできる。

`/etc/ssh/ssh_config`であって`/etc/ssh/sshd_config`ではない。

## 基本形式

- 同一項目は先に記述されたほうが優先される。
- sshコマンドで入力される場合はそちらが優先される。
- コメントは \#
- 小文字でもよい。

```
Host _HOST_
	User _USER_
	HostName _HOST_NAME_
	IdentityFile _SECRET_KEY_PATH_
```

- Host
	- \_HOST\_にはHostマシンのアドレスやドメインを入れるがおそらくエイリアスでなんでもいい。
	- ワイルドカード`*`も合わせて使える。
- User
	- Hostのユーザー名
- IdentityFile
	- 公開鍵認証を行う場合の秘密鍵
	- Windowsの場合、ここで指定するパスは絶対パスでなければならないという謎制約がある。


## 例

PowerShell(Windows)やTerminal(Mac、Linux)から

Ubuntuのログインするユーザーが"\_USER\_"、マシンのIPアドレスを"192.168.xx.xx"、秘密鍵を"~/.ssh/key"とした場合、

```
Host MyServer
	User _USER_
	HostName 192.168.xx.xx
	IdentityFile ~/.ssh/key
```

```
ssh MyServer
```

## その他のオプション例

### Port

ポートを指定

```
Host *
	Port 22
```

### PreferredAuthentications

認証順番を指定できる。秘密鍵があったら公開鍵認証が優先なのであまり必要はない。

```
Host *
	PreferredAuthentications publickey,password
```

### ServerAliveInterval

Host側で`ClientAliveInterval`が指令されている場合は冗長かもしれない。

指定秒数おきにHostに応答信号を送りタイムアウトを抑制する。

```
Host *
	ServerAliveInterval _SECOND_
```
### ServerAliveCountMax

`ServerAliveInterval`の呼びかけ回数。デフォルト3回なのでそれくらいで。

```
Host *
	ServerAliveCountMax _COUNT_
```

---

[Back to home](../readme.md)

<!-- Written by Croyfet in 2022-->

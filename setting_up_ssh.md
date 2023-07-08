# SSHのセットアップ
## Open SSH Server のインストール
1. サーバーアプリのインストール
	```bash
	sudo apt -y update
	sudo apt -y install openssh-server
	```
1. 構成ファイルの設定
	```yaml:/etc/ssh/sshd_config
	PermitRootLogin no			# root でのログインの抑止
	PermitEmptyPasswords no 	# 空のパスワードの抑止
	MaxAuthTries <Nums>			# 最大試行回数
	Port <Nums>					# ポート番号
	PasswordAuthentication no	# パスワード認証によるログインを禁止
	```

## 公開カギ認証の設定
### 公開鍵/秘密鍵の生成
1. ディレクトリの移動
	```bash
	mkdir ~/.ssh
	chmod 700 ~./ssh
	cd ~/.ssh
	```
2. 生成
	```bash
	ssh-keygen -t ecdsa -f <file_name>
	```
	画面に従いパスフレーズを登録する．
	- オプション
		-t 暗号化手法 (rsa,ecdsa,...)
3. サーバーに公開鍵を登録
	```bash
	cd ~/.ssh
	cat <file_name>.pub >> authorized_keys
	chmod 600 authorized_keys
	```

## SSHの起動
```bash
sudo systemctl ssh restart
```

# 参考

https://www.kkaneko.jp/tools/server/pubkey.html

https://www.st.itc.keio.ac.jp/ja/faq_security_sshdconfig_st.html

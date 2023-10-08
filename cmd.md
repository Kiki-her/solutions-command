# 以前の PC で行う作業

## Git の設定を移行

```
git config --global user.name "kiki"
git config --global user.email "k.kazaneko@gmalo.com"
```

## SSH 鍵の移行

### 以前の PC で行う作業

以前の PC から、SSH 鍵をコピーする。鍵は通常、~/.ssh ディレクトリにある。

```
cd ~/.ssh
```

上記のコマンドを打っても出ない場合は、隠しファイル・フォルダの非表示を切り替える

```
defaults write com.apple.finder AppleShowAllFiles TRUE
```

```
killall Finder
```

### 新しい PC で行う作業

新しい PC に SSH 鍵を配置する場所を確認し、~/.ssh ディレクトリに鍵をコピーする。

PC で Git Bash を開き、以下のコマンドを実行する。**`id_rsa`には`.ssh`内にある該当のファイル名が入る**

```
eval $(ssh-agent -s)
ssh-add ~/.ssh/id_rsa
```

もし`eval $(ssh-agent -s)`を打って`Agent pid 0000`と 4 桁の数字(エージェントのプロセス ID)が返ってきたら、以下を行う。

秘密鍵を SSH エージェントに登録。
**`id_rsa`には`.ssh`内にある該当のファイル名が入る**

```
ssh-add ~/.ssh/id_rsa
```

`ssh-add`コマンドを打って登録されたメールアドレスが返ってくると、リモートサーバに ssh 登録できるようになった証拠

# 新しい PC で行う作業

Github アカウントを新しい PC に追加する

- GitHub にログインして、Settings > Developer settings > Personal access tokens に進み、新しいトークンを生成する
- トークンをクリップボードにコピー
- 新しい PC で Git Bash を開き、以下のコマンドを実行

```
git config --global credential.helper store
```

以下のコマンドを実行して、新しい PC での認証情報を設定

```
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global credential.username "your_username"
git config --global credential.helper cache
```

最後に、以下のコマンドを実行して GitHub アカウントにログイン

```
git config --global credential.helper 'cache --timeout=3600'
```

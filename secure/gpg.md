# gpg

## 導入 - GitHubへのcommitまで

```zsh
brew install gnupg
brew install pinentry-mac

echo "pinentry-program $(which pinentry-mac)" >> ~/.gnupg/gpg-agent.conf

gpg --full-generate-key

# ご希望の鍵の種類を選択してください:
# 1

# 鍵長は? (3072)
# 4096

# 鍵の有効期間は?
# 0

# これで正しいですか? (y/N) 
# y

# 本名:username（GitHubのユーザー名）
# メールアドレス:12345678+username@users.noreply.github.com（noreply設定の場合）

# 名前(N)、コメント(C)、電子メール(E)の変更、またはOK(O)か終了(Q)?
# O

# パスワード入力のpinentry-mac ダイアログが入力されるのでパスフレーズを入力。

# 上記完了後、下記コマンドを実行すれば鍵のリストに追加されていることが確認できます。
gpg --list-secret-keys --keyid-format LONG
# ここで、 sec  rsa4096/ のあとに表示された文字列をコピー。

# $KEYIDは先ほどコピーした文字列をペースト
git config --global user.signingkey $KEYID
git config --global commit.gpgsign true

# 公開鍵発行
gpg --armor --export $KEYID >> ~/gpg.key
 
```

ここまで完了したら、GitHubの設定画面で公開鍵を登録します。

### gpg.keyの内容をGitHubに登録

1. GitHubにログイン
2. 右上の自分のアイコンをクリック
3. メニューからSettingsページに移動
4. 左側の項目にあるSSH and GPG keysをクリック
5. GPG keysの項目にあるNew GPG keyボタンをクリック
6. Titleは任意の文字列を入力すれば問題なし。 
7. Key内のtextareaにgpg.keyの内容をコピー＆ペーストする
8. Add GPG keyボタンをクリック

認証を求められる場合は指示に従って認証し、GPG keysに新しい公開鍵が追加されていることを確認します。

### 実際にcommitし、pushしてみる

GitHubでcommitし、pushする。
先ほど設定したパスフレーズの入力が求められた場合は入力します。
Commitsを確認するとpushされたcommitの横に緑色のVerifiedラベルが表示されており、
そのcommitが署名つきcommitになっていることがわかります。

### 公開鍵について

なお、実際にその署名が本人のものかどうか証明する簡単かつほぼ唯一確実度の高い方法は、本人が **手渡しなどで直接伝達する** ことです。
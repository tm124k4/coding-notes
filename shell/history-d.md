# zshにおけるhistory -d

シェルスクリプト > zshにおけるhistory -d

bashのコマンド履歴を削除する `history -d` コマンドは、
zshでは用意されていないため、`alias` として下記を `.zshrc` または `.zprofile` に記載する。

```zsh
alias history-d='(){local number=$1;if [ ! "$number" -gt 0 ];then;number="$";fi;sed -i "" -e "${number}d" ~/.zsh_history;history -p;fc -RI ~/.zsh_history}'
```

上記を記載したら、`source` コマンドで設定ファイルを読み込み直す。

```zsh
source ~/.zprofile
```
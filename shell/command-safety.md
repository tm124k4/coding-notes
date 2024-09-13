# コマンドの安全性を高める

シェルスクリプト > コマンドの安全性を高める

## 設定方法

`.zprofile` などで `alias` を定義する場合、 
予め `unalias -a` で `alias` を明示的に初期化する。
設定ファイルでは `alias` の定義よりも上に記載する。

```zsh
unalias -a
# これより下の行にaliasを追加

# 設定したいaliasを追加
alias la='ls -G la'
```

## source

`source` コマンドはシェルスクリプトの設定ファイルを読み込むコマンドです。

`.zsh_history` を `source` コマンドの引数に指定すると意図しない大量のコマンドが実行されてしまう可能性があるので、`_history` という文字列を含むファイル名の場合に `source` コマンドを実行しないよう `alias` で `source` コマンドを上書きします。

```zsh
safety-source() {
  local filepath=$1
  if [[ "$filepath" == *_history* ]]; then
    echo "denied: open $1"
    return 1
  fi
  source $filepath
}
alias source='safety-source'
```

## dd

`dd` コマンドは強力なコマンドですが、Webコーディングで使用する機会はほぼ存在しません。
意図しないメディアやファイルへのデータの上書きの可能性があるため、普段は実行しないようにしておくのが理想的です。

```
alias dd='echo disabled: "dd"'
```
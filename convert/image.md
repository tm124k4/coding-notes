# 画像の変換

変換 > 画像

## JPEG/PNG -> WebP

2024年現在、ほとんどのケースでJPEGやPNGはWebPに代替可能。WebPは透過色にも対応しており、透過PNGもそのまま圧縮変換する事ができます。

MacOSの場合、cwebpを使用するためにwebpをインストール。

```zsh
brew install webp
```

下記コマンドで単一の画像 `in.jpg` を `out.webp` として.webp形式の画像に変換できます。

```zsh
cwebp in.jpg -o out.webp
```

下記コマンドで現在のディレクトリ以下の `*.jpg` `*.jpeg` を、すべて `*.webp` に変換します。

**※変換前の `*.jpg` `*.jpeg` は削除されます。**

```zsh
for f in $(find . -type f \( -iname \*.jpg -o -iname \*.jpeg \)); do o=$(basename $f | sed -e "s/\.jpg//g" -e "s/\.jpeg//g");cwebp $f -o ${o}.webp;rm $f;done
```

`*.png` -> `*.webp` は次の通り。

**※変換前の `*.png` は削除されます。**

```zsh
for f in $(find . -type f \( -iname \*.png \)); do o=$(basename $f | sed -e "s/\.png//g");cwebp $f -o ${o}.webp;rm $f;done
```

PNGとJPEGの両方を変換する場合は次の通りです。

**※変換前の `*.jpg` `*.jpeg` `*.png` は削除されます。**


```zsh
for f in $(find . -type f \( -iname \*.jpg -o -iname \*.jpeg -o -iname \*.png \)); do o=$(basename $f | sed -e "s/\.jpg//g" -e "s/\.jpeg//g" -e "s/\.png//g");cwebp $f -o ${o}.webp;rm $f;done
```


## JPEG -> 最適化JPEG

WebP画像が表示できない古いブラウザでも確実に表示したい場合、mozjpegを利用すれば、JPEGでもそれなりにファイルサイズの圧縮が可能です。

### インストール

```zsh
brew install mozjpeg
```

### 単一ファイルの圧縮

```zsh
djpeg input.jpg | cjpeg -optimize -quality 60 > output.jpg
```

### ディレクトリにあるjpegファイルを再帰的に圧縮

**※圧縮前のファイルは上書きされます。**

```zsh
for f in $(find . -type f \( -iname \*.jpg -o -iname \*.jpeg \)); do ;djpeg $f | cjpeg -optimize -quality 60 -outfile $f.new;mv "$f.new" $f;done
```
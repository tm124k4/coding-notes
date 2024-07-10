# 動画の変換

変換 > 動画

## MP4 -> WebM

2024年現在、動画をページに埋め込む場合はできる限りWebMを利用するのが望ましいです。

動画ファイルのエンコード用にffmpegをインストールします。

```zsh
brew install ffmpeg
```

下記コマンドで `input.mp4` を `output.webm` として.webm形式の動画に変換できます。

```zsh
ffmpeg -i input.mp4 -strict -2 output.webm
```

ただし、動画のエンコードには相応のマシンパワー（あるいは時間）が必要です。
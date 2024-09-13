# tools

コーディング用のMacで使用するアプリケーションとインストール方法についてのメモ。


## 前提

brewコマンドの実行には、Homebrew（以下brew）のインストールが必要のため、インストールする。

```zsh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

インターネットに接続した状態で、Launchpadから `ターミナル` を開き、上記コマンドを入力して実行する。

## ブラウザ

### Google Chrome

```zsh
brew install google-chrome
```

PCにおける最小限の動作確認ブラウザその1。
Chromeとも呼ばれ、Chromium系ブラウザの代表的存在。Edgeとはレンダリングエンジンが同じBlinkであり、Chromeで問題がなければ基本Edgeも問題ない。クロスプラットフォーム対応。

### Safari

初期状態でインストールされている。MacOS専用。

PCにおける最小限の動作確認ブラウザその2。
SafariのバージョンはMacOSのバージョンに依存するため、コーディングではある程度古いバージョンにも対応する実装が推奨される。
レンダリングエンジンはWebkit。MacOS以外でもWebkitを使用したブラウザで確認することは一応可能。

### Firefox

```zsh
brew install firefox
```

PCにおいて、追加の動作確認候補となるブラウザ。
Blink(Chrome、Edgeなど)でも、Webkit(Safariなど)でもない独自のレンダリングエンジンを持つブラウザ。クロスプラットフォーム対応。

### Vivaldi

```zsh
brew install vivaldi
```

カスタマイズや機能が豊富なChromium系ブラウザ。クロスプラットフォーム対応。

## 開発用

### VSCode

```zsh
brew install visual-studio-code
```

クロスプラットフォームのプログラミング用エディタ。ファイラー、ターミナル、git管理、markdownのプレビュー等豊富な機能を持つ。

### Hyper

```zsh
brew install hyper
```

カスタマイズ性が高くMacOS標準のターミナルよりも安定しているターミナル。

### XCode

brewからのインストールはできないため、インストールは `App Store` から行う必要がある。

MacOS専用。特に、付属しているシミュレーターで実機に限りなく近いiPhoneやiPadのSafariでWebサイトの動作確認ができる。

## セキュリティ

### ClamAV

```zsh
brew install clamav
```

GUIアプリケーションではないが、重要なソフトなので記載。
クロスプラットフォーム、ターミナル上で使用するウイルススキャンソフト。ダウンロードしたファイルを開いたり、実行する前に確認するために使用する。

### keepassXC

```zsh
brew install keepassxc
```

クロスプラットフォームのパスワード管理ソフト。パスワードを暗号化して保管する。メモ機能があり、接続情報などの保管にも適している。

## その他

### Keka

```zsh
brew install keka
```

圧縮・解凍ソフト。暗号化だけでなく、WindowsやLinuxユーザーと圧縮ファイルをやり取りする際のファイル名の文字化けや不要な__MACOSXファイルを同梱せずに圧縮ができる。


### Libreoffice

```zsh
brew install libreoffice
brew install libreoffice-language-pack --language=ja
```

クロスプラットフォーム。文書作成、表計算など。主にExcelやWordのファイルを表示・編集するのに使用する。

### iina

```zsh
brew install iina
```

MacOS専用の動画プレイヤー。WebP(VP9)など幅広い動画形式に対応している。再生確認や、動画ファイル情報の確認用。

### VLC

`brew install vlc` でインストールできるが、肝心のインストーラーがダウンロードできない場合が多い。

そのため、ミラーサイトからミラーのファイルをダウンロードが推奨される。下記コマンドは一例（もちろん、ブラウザからダウンロードしてもOK）。

```zsh
curl -OL https://cdimage.debian.org/mirror/videolan.org/vlc/3.0.21/macosx/vlc-3.0.21-arm64.dmg
echo -e "15dd65bf6489da9ec6a67f5585c74c40a58993acff41a82958a916dd74178044  vlc-3.0.21-arm64.dmg" | shasum -a 256 -c -
# vlc-3.0.21-arm64.dmg: OK
# 上記のように表示されたら正しいファイル
```

ダウンロードしたら、下記コマンドでインストールするか、dmgファイルを直接クリックしてインストール。

```zsh
hdiutil mount vlc-3.0.21-arm64.dmg
cd "/Volumes/VLC media player/"
cp -r "/Volumes/VLC media player/VLC.app" /Applications
cd
hdiutil unmount "/Volumes/VLC media player/"
```

クロスプラットフォームの動画プレイヤー。幅広い動画形式に対応している。
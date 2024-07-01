# tools




## ブラウザ

### Google Chrome

```zsh
brew install google-chrome
```

PCにおける最小限の動作確認ブラウザその1。
Chromeとも呼ばれ、Chromium系ブラウザの代表的存在。Edgeとはレンダリングエンジンが同じBlinkであり、Chromeで問題がなければ基本Edgeも問題ない。

### Safari

初期状態でインストールされている。MacOS専用。

PCにおける最小限の動作確認ブラウザその2。
SafariのバージョンはMacOSのバージョンに依存するため、コーディングにおいてはある程度古いバージョンでも問題ないような実装が推奨される。
レンダリングエンジンはWebkit。MacOS以外でもWebkitを使用したブラウザで確認することは一応可能。

### Firefox

```zsh
brew install firefox
```

PCにおいて、追加の動作確認候補となるブラウザ。
Blink(Chrome、Edgeなど)でも、Webkit(Safariなど)でもない独自のレンダリングエンジンを持つブラウザ。

### Vivaldi

```zsh
brew install vivaldi
```

カスタマイズや機能が豊富なChromium系ブラウザ。

## 開発用

### VSCode

```zsh
brew install visual-studio-code
```

ファイラー、ターミナル、エディタ、git管理、markdownのプレビュー等豊富な機能を持つ。

### Hyper

```zsh
brew install hyper
```

カスタマイズ性が高くMacOS標準のターミナルよりも安定しているターミナル。

### XCode

インストールはApp Storeから。

付属しているシミュレーターで実機に限りなく近いiPhoneやiPadでの動作確認が可能。


## セキュリティ

### ClamAV

```zsh
brew install clamav
```

ターミナル上で使用するウイルススキャンソフト。ダウンロードしたファイルを開いたり、実行する前に確認するために使用する。

### keepassXC

```zsh
brew install keepassxc
```

パスワード管理ソフト。パスワードを暗号化して保管する。メモ機能があり、接続情報などの保管にも適している。

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

文書作成、表計算など。主にExcelやWordのファイルを表示・編集するのに使用する。

### iina

```zsh
brew install iina
```

MacOS専用の動画プレイヤー。WebP(VP9)など幅広い動画形式に対応している。再生確認や、動画ファイル情報の確認用。
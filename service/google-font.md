# Google Font

https://fonts.google.com

## 概要

無料かつ商用利用可能なサービス。
SIL Open Font License でライセンスされたフォントがダウンロードできるほか、Google Fontにあるフォントはwebフォントとしても利用可能。

## CSSでフォントをインポートする

https://fonts.google.com/noto/specimen/Noto+Serif+JP?query=Noto+sans&noto.query=Noto+Serif+JP

1. 上記URLのような、インポートしたいフォントのページにアクセス。

2. `Get Font`　ボタンをクリック

3. `Get embed Code` ボタンをクリック

4. 右側のボックスにある `@import` のラジオボックスをクリック。

5. `Embed code in the <head> of your html` の下にあるソースコードの中の下記部分を任意のcssファイルの中で読み込む。

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+JP:wght@200..900&display=swap');
```

## フォントをダウンロードする

https://fonts.google.com/noto/specimen/Noto+Serif+JP?query=Noto+sans&noto.query=Noto+Serif+JP

1. 上記URLのようなダウンロードしたいフォントのページにアクセス。

2. `Get Font`　ボタンをクリック

3. `Get embed Code` ボタンをクリック

4. `Download All` ボタンを押す。しばらく待つと、フォントファイルの入ったzipファイルがダウンロードできる。

## 関連URL
https://developers.google.com/fonts/faq?hl=ja
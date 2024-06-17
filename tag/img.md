# imgタグ

画像 > img

## 概要

imgタグは画像を表示させるためのタグ。最小限のタグ構成は次の通り。

```html
<img src="asset/img/img.webp" width="256" height="256" alt="">
```

divタグなどに入れる。

```html
<div class="wrapper">
  <img src="asset/img/img.webp" width="256" height="256" alt="">
</div>
```

## width/height属性について

width属性とheight属性はCLS対策のために必須。
XDに記載された幅・高さを入力する。

## alt属性について

alt属性は画像の中身に関わらず必須。

###  `alt=""` のままでOKなケース

- 前後に隣接する何らかのテキスト要素で説明されている場合

```HTML

<img src="asset/img/img.webp" width="256" height="256" alt="">
<p>上の画像は、海の画像です</p>

```

```HTML
<figure>
  <img src="asset/img/img.webp" width="256" height="256" alt="">
  <figcaption>海の画像</figcaption>
</figure>
```

- 意味を持たない画像である場合。
  - 背景として使用される場合
  - 区切り線として使用される場合
  - 単に外部リンクであることを示すような小さなアイコン 

### `alt=""` は必須

- 視覚障害者向けのスクリーンリーダーでは、`alt=""` のタグはスキップされる。そのため、意味を持たない画像はスキップするのがユーザーにとってやさしい。

### alt属性に何らかの文字列を記入する場合

基本的には `alt=""` で問題ないが、以下の場合には入力する。

- 文字をアウトライン化した画像の場合は、その文字列を入力する。（画像が表示できない環境や読み上げに対応）

```html
<img src="asset/img/text.webp" width="256" height="256" alt="Hello, World!">
```

- 何らかの指定がある場合はその文字列を入力する。

## redefine CSS

imgタグで余白を生じるのを防ぐには、以下のどちらかで調整する必要があります。

(a) imgタグをブロック要素にする。

```css
:where(img){
  display:block;
  width:100%;
  height:100%;
}
```

(b) vertical-aliginを設定する。

```css
:where(img){
  vertical-align:top;
  width:100%;
  height:100%;
}
```
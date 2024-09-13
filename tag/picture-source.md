# pictureタグにおけるsourceタグ

画像 > picture > source

## 概要

sourceタグは画像を出し分けるタグ。最小限のタグ構成は次の通り。

```html
<picture>
  <source media="(max-width:768px)" srcset="sp.webp" width="320" height="240">
  <img src="pc.webp" width="640" height="480" alt="">
</picture>
```

上記の場合、画面の幅が `768px` までは `sp.webp` が表示され、`769px` 以上は `pc.webp` が表示される。

sourceタグもimgタグと同様、width属性とheight属性はCLS対策に入力が推奨されます。
width/height属性にはXDのスマートフォン版の画像の幅・高さを入力します。

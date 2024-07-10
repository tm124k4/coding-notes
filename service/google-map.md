# Google マップ

https://www.google.com/maps

## 概要

所在地をWebサイトで示す際に、Google Mapをiframeタグで表示可能。


## カスタマイズ

### マイマップを埋め込む

埋め込んだ要素の左側にマイマップのリストを表示したい場合、発行されたiframeタグのsrc属性内のURLクエリパラメーターに `legend=1` または `legend=true` を追加する。

```html
<iframe src="...legend=1"></iframe>
```

`noprof=1` を追加するとマイマップを作成したユーザー名を非表示にすることができる。デザイン上の理由で少しでもマイマップの上部に表記されている文字を減らしたい場合に有効と思われる。

ただし、埋め込みのURLから `noprof=1` を削除して別タブでアクセスすればユーザー名を見ることができるため、ユーザー名は非公開にする事はできない。

```html
<iframe src="...noprof=1"></iframe>
```

### マップをクリックするまではスクロールを止めない

そのままiframeタグによって埋め込みを行うと、マップのiframeの上にマウスカーソルがある場合、ズームイン・ズームアウトされてしまう。幅いっぱいに広げた時にページスクロールしづらくなるため、下記のように対策することが推奨される。

```html
<style>
.iframe-container{
  width:100%;
  height:500px;
  margin:100px auto;
}

.iframe-map{
  pointer-events:none;
  width:100%;
  height:100%;
}

.iframe-map.is-active{
  pointer-events:unset;
}
</style>

<div class="iframe-container">
  <iframe class="iframe-map" src="...">
</div>

<script>
  document.querySelector('.iframe-container').addEventListener('click',()=>{
    document.querySelector('.iframe-container>.iframe-map').classList.add('is-active')
    setTimeout(()=>{
      document.querySelector('.iframe-container>.iframe-map').classList.remove('is-active')
    },3000)
  })

  document.querySelector('.iframe-container').addEventListener('mouseleave',()=>{
    document.querySelector('.iframe-container>.iframe-map').classList.remove('is-active')
  })
</script>
```

地図のiframeタグが入った `.iframe-container` がクリックされるまでは、地図のiframeタグ自体に `pointer-events:none` を設定しておく。

下記のどちらかの条件を満たした場合に、`pointer-events:none` の指定を解除する。

- 地図をクリックして一定時間経過する
- `.iframe-container` の領域からマウスカーソルが出た場合

これによってページがスクロールしづらくなる問題がある程度軽減される。
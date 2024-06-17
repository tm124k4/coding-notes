# radio

## 概要

`<input type="radio">` は、同じname同士の中で択一のラジオボタンを表示するinputタグです。

```HTML
<label>
  <input type="radio" name="example" value="ラジオボタン1">
  <span>ラジオボタン1</span>
</label>
<label>
  <input type="radio" name="example" value="ラジオボタン2">
  <span>ラジオボタン2</span>
</label>
```

## 入力必須ではないラジオボタングループの作成

基本的にはラジオボタンは必須扱いですが、
必須でないラジオボタンのグループも作成することができます。
予め `未入力` のvalue属性を持ったラジオボタンをnameに1つずつ用意しておき、かつ非表示としておきます。
さらに、`未入力` のラジオボタンにはchecked属性を設定しておけば、
最初からvalue属性に `未入力` が選択されているため、
結果的には入力必須ではないラジオボタングループを作成することが可能です。

```HTML
<input style="display:none" type="radio" name="example" value="未入力" checked>
<label>
  <input type="radio" name="example" value="ラジオボタン1">
  <span>ラジオボタン1</span>
</label>
<label>
  <input type="radio" name="example" value="ラジオボタン2">
  <span>ラジオボタン2</span>
</label>
```

ただし、ラジオボタングループを事実上の入力必須としない場合、以下の値が送信されることによって、サーバーサイド側のバリデーションでエラーとなる可能性があります。

- `value=""` 入力なし
- `value=" "` 半角スペース1文字

以下は、下に進んでいくにつれてバリデーションのエラーになりにくいと思われる文字の候補です。

- `value="　"` 全角スペース1文字
- `value="-"` 半角ハイフン
- `value="ー"` 全角ハイフン
- `value="未選択"` 任意の文字列

サーバーサイドのPHPなどで動作するメールフォームの自動返信メールでは、`未入力` の場合に文字列の存在しない空白にしたい場合には別途実装する必要があります。

## CSSによるカスタマイズ

ラジオボタンがオンの場合は、CSSでは該当の要素を `:checked` で選ぶことができます。
さらに、`:after` を追加すれば、

```HTML
<style>
/* オフの場合 */
input[type="radio"]{
  appearance:none;
  margin:0;
  margin-right:6px;
  width:20px;
  height:20px;
  border-radius:45%;
  border:1px solid #000;
  position:relative;
}

/* オンの場合 */
input[type="radio"]:checked:after{
  position:absolute;
  content:'';
  width:8px;
  height:8px;
  border-radius:25%;
  background:#000;
  left:50%;
  top:50%;
  transform:translate(-50%,-50%);
}
</style>

<label>
  <input type="radio" name="radio1" value="test1">
  <span>test1</span>
</label>
<label>
  <input type="radio" name="radio1" value="test2">
  <span>test2</span>
</label>
```

## redefine CSS

ブラウザごとに独特の見た目とmarginが設定されており、
カスタマイズしたい場合は `margin:0` と `appearance:none;` は必須になります。

```CSS
where:(input[type="radio"]){
  margin:0;
  appearance:none;
}
```
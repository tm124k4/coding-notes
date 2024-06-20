# Safari

## <= 16.3

### border-radiusを設定した要素のoutlineが円形にならない。

Safari 16.3以前（2023年3月頃までのバージョン）で `border-radius` を用いて丸（円）を表現したい場合、`outline` ではなく `border` の使用が必要です。この場合、あわせて `width` や `height` の調整が必要になるケースがあります。

```css
/* NG: <= Safari 16.3 */
.before{
  width:32px;
  height:32px;
  border-radius:50%;
  outline:1px solid red;
}

/* OK: >= Safari 16.4 */
.after{
  width:34px;
  height:34px;
  border-radius:50%;
  border:1px solid red;
}
```

Safari のリリースノートによれば、Safari 16.4以降で `outline` に対して `border-radius` が適応されるようになるため、ユーザー数を考慮すると `outline` ではなく `border` を使用する必要があると考えられます。


https://developer.apple.com/documentation/safari-release-notes/safari-16_4-release-notes


### (<= 16.3?) inputタグのsubmitボタンの中の文字にjustify-content:centerが効かない

やや古いバージョンのSafariでは、inputタグのボタンの中に表示される文字（value属性）を中央寄せにしたい場合は、`.after` のようにする必要があります。

```css
/* NG: <= Safari 16.3? */
.before{
  width:100px;
  height:24px;
  font-size:12px;
  display:flex;
  justify-content:center;
}

/* OK: >= Safari 16.4? */
.after{
  width:100px;
  height:24px;
  font-size:12px;
  display:block;
  text-align:center;
}
```

Safari 16.4 のリリースノートによれば  `Fixed text selection on flex and grid box items.` とあるので、Safari 16.3以前で発生する模様？
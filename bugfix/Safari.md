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

Safari のリリースノートによれば、Safari 16.4以降で `outline` に対して `border-radius` が適応されるようになります。

https://developer.apple.com/documentation/safari-release-notes/safari-16_4-release-notes

Safari のユーザー数を考慮すると `border-radius` を使用して角丸もしくは円形を表現する際、`outline` ではなく `border` を使用する必要があると考えられます。
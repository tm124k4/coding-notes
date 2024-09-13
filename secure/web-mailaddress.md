# Webサイト上のメールアドレスの表示について

### 最善はメールアドレス自体を記載しない

今日、Webサイト上で受信用メールアドレスの文字列を公開すること（`mailto:` リンクを含む）はスパムメールや標的型攻撃メールなど、多大なセキュリティリスクがあるため、**原則としてメールフォームなど、メールアドレスを公開しないようなサービスの使用が前提となります**。

メールアドレスの提示が必要な場合、文字列を画像にするか、QRコードに変換した画像の表示でbotによるメールアドレス収集・送信のリスクを少し軽減することができますが、メールフォームを使用することが推奨されます。

### bot対策

メールアドレスのリンクを公開する必要がある場合、静的なHTMLタグ内に直接記載するのではなくアドレス自体を難読化します。

あるいは、動的なDOM生成を行うことで、**確実ではありませんが** botによるメールアドレス収集のリスクをわずかながら緩和できる可能性があります。botが取りうるメールアドレス収集方法は以下のようなものが考えられます。

- ソースコードからのメールアドレス文字列の収集
- ヘッドレスブラウザを利用し、aタグからのhref属性を自動取得
- アクセスしたサイトのURLのドメインを参考に、`contact亞example.com` のように定番のアドレスに対してメール送信を試みる
- OCRによって、画像化されたメールアドレス文字列を自働認識

リンクとしてmailto:リンクを設置する事が必要な場合、下記のような文字列の生成方法があります。
テキスト内の `亞` は半角の `@` として読み替えてください。

なお、人力でのメールアドレスの収集に対しては、bot対策用のメールリンクを通常のユーザーと同じように開けば良いため効果はほとんどなく、その観点からもメールフォームの使用が推奨されます。

#### base64デコード

base64文字列をデコードする方法は簡単でシンプルですが、暗号化はされていないのでいくつかに分ける事が推奨されます。

```JavaScript
let A=btoa('mailto:exampl')
let B=btoa('e亞example.com')

console.log(atob(A)+atob(B))
```

#### String.fromCharCode

任意の整数から任意の文字を生成します。他の方法と組み合わせて使用することが推奨されます。

```JavaScript
let $m=String.fromCharCode(109) // m

console.log($m+'ailto:exa'+$m+'ple亞exa'+$m+'ple.com')
```

#### 記号化

JavaScriptの言語仕様を利用して文字列を得る方法です。例えば、下記は `i` を出力します。

```javaScript
let $example_i=[[]+[][+[]]][+[]][[[+[]==[]][+[]]+[+[]==[]][+[]]+[+[]==[]][+[]]+[+[]==[]][+[]]+[+[]==[]][+[]]]]
console.log($example_i)
```

JavaScriptは6種類の記号だけでプログラムを書くことができます。それを利用した難読化も可能ですが、1文字あたりのソースコードが長くなるため、使用する場合は部分的な使用が推奨されます。

下記は冒頭部以外を変数化した擬似コードの参考例です。

```JavaScript
// 
let $undefined = [[][+[]]+[]]+[]
let $false = ([]==[])+[]
let $true = (+[]==[])+[]
let $NaN = [+[[]==[]]]+[]
let $0 = +[]
let $1 = +[(+[]==[])+(+[])]
let $2 = (+[]==[])+(+[]==[])

// 最初に入手可能な文字を取得
let $3 = $1 + $2
let $4 = $2 + $2
let $5 = $1 + $2 + $2
let $6 = $2 + $2 + $2
let $7 = $1 + $2 + $2 + $2
let $8 = $2 + $2 + $2 + $2
let $9 = $1 + $2 + $2 + $2 + $2
let $a = $false[$1]
let $d = $undefined[$2]
let $e = $true[$3]
let $f = $false[$0]
let $i = $undefined[$5]
let $l = $false[$2]
let $n = $undefined[$1]
let $N = $NaN[$0]
let $r = $true[$1]
let $s = $false[$3]
let $t = $true[$0]
let $u = $undefined[$0]

// "async" のために "c" と入手可能な文字を取得する
let $find = $f+$i+$n+$d
let $function = [$find][$find]+[]
let $c = $function[$3]
let $o = $function[$6]
let $v = $function[+[$2+[]+$3]] // 23
let $lkb = $function[+[$1+[]+$6]] // 16 ({)
let $rkb = $function[+[$3+[]+$2]] // 32 (})
let $lp = $function[+[$1+[]+$3]] // 13 (()
let $rp = $function[+[$1+[]+$4]] // 14 ())
let $SPACE = $function[$8] // ( )

// "async" 等のために "y" と入手可能な文字を取得する
let $values = $v+$a+$l+$u+$e+$s
let $objectArrayIterator = [$find][$values]()+[]
let $A = $objectArrayIterator[$8]
let $b = $objectArrayIterator[$2]
let $I = $objectArrayIterator[+[$1+[]+$4]] // 14
let $j = $objectArrayIterator[$3]
let $y = $objectArrayIterator[+[$1+[]+$2]] // 12

// "String" のために "S" と入手可能な文字を取得する
let $constructor = $c+$o+$n+$s+$t+$r+$u+$c+$t+$o+$r
let $String = $a[$constructor]
let $Boolean = ([]==[])[$constructor]
let $S = ($String+[])[$9]
let $B = ($Boolean+[])[$9]
let $g = ($String+[])[+[$1+[]+$4]] // 14

// "getOwnPropertyNames" のために "O" を取得する
// あわせて入手可能な文字を取得する
let $exec = [][$find][$constructor]
let $return = $r+$e+$t+$u+$r+$n
let $Object = $exec($return+$SPACE+$lkb+$rkb)()
let $F = ($exec+[])[$9] // 9
let $O = ($Object+[])[$8] 
let $m = ($exec()+[])[+[$1+[]+$4]] // 14

// "getOwnPropertyNames" のために "p" を取得する
// あわせて入手可能な文字を取得する
let $toString = $t+$o+$S+$t+$r+$i+$n+$g
let $36 =  +[$3+[]+$6]
let $h = [+[$1+[]+$7]][$0][$toString]($36) //17
let $k = [+[$2+[]+$0]][$0][$toString]($36) //20
let $p = [+[$2+[]+$5]][$0][$toString]($36) //25
let $q = [+[$2+[]+$6]][$0][$toString]($36) //26
let $w = [+[$3+[]+$2]][$0][$toString]($36) //32
let $x = [+[$3+[]+$3]][$0][$toString]($36) //33
let $z = [+[$3+[]+$5]][$0][$toString]($36) //35

// "getOwnPropertyNames" のために 大文字 "P" を取得する
let $async = $a+$s+$y+$n+$c
let $Promise = $exec($return+$SPACE+$async+$SPACE+$exec())()()
let $P = ($Promise+[])[$8]

// "getOwnPropertyNames" 関数を作成し実行し、
// "fromCharCode" と "fromCharPoint" のための大文字 "C" を入手する。
let $getOwnPropertyNames = $exec($return+$SPACE+$O+$b+$j+$e+$c+$t)()[$g+$e+$t+$O+$w+$n+$P+$r+$o+$p+$e+$r+$t+$y+$N+$a+$m+$e+$s]
let $gOPNString = $getOwnPropertyNames($String)
let $join = $j+$o+$i+$n
let $split = $s+$p+$l+$i+$t
let $C = ($gOPNString+[])[$split]($r+$o+$m)[$1][$split]($h+$a+$r)[$0]

// "fromCharCode" 関数と "fromCharPoint" 関数を入手する
let $fromCharCode = $String[$f+$r+$o+$m+$C+$h+$a+$r+$C+$o+$d+$e]
let $fromCharPoint = $String[$f+$r+$o+$m+$C+$h+$a+$r+$P+$o+$i+$n+$t]

// "fromCharCode" 関数から アットマーク "@" と ドット "." を入手する
let $atMark = $fromCharCode(+[$6+[]+$4]) // 64
let $dot = $fromCharCode(+[$4+[]+$6]) //46

// メールアドレスを出力する
console.log($e+$x+$a+$m+$p+$l+$e+$atMark+$e+$x+$a+$m+$p+$l+$e+$dot+$c+$o+$m)
```

#### 置き換える

`replace` 関数で文字列を置き換える方法。例えば、下記の例では最初の `.` だけがアットマークに置き換えられるので、メールアドレスを出力することができます。

```JavaScript
console.log('mailto:example.example.com'.replace('.','亞'))
```

#### 区切る

`split` 関数で文字列を区切る方法。例えば、下記のようにいったん `.` で区切ってから、不要な最後の `com` を除去する方法があります。

```JavaScript
console.log('mailto:example亞example.com.com'.split('.').slice(0,-1).join('.'))
```

####  文字エスケープの使用

1文字ずつUnicode コードポイントに変換する方法もあります。下記のように、`\x75` は実際には `u` として出力されます。

```javascript
"\u0075" === "u" // true
"\x75" === "u" // true

console.log("\x75")
```

#### 正規化

置き換える方法の別バージョン。`normailize` 関数で、非ASCII文字からASCII文字に変換できる文字を利用する方法。

```JavaScript
console.log('e\u24CDample亞e\u24CDample.com'.normalize('NFKD').toLowerCase())
```

#### `ı` と `toLocaleUpper(Lower)Case` を使う

トルコ語では、英語のアルファベット `I` の小文字に相当する文字は `ı` として表現されます。アメリカ英語 `en-US` で小文字→大文字→小文字と変換することで、`ı` → `I` → `i` として変換されます。

```javaScript
console.log(`maılto:maıl+example亞example.com`.toLocaleUpperCase('en-US').toLocaleLowerCase('en-US'))
```

#### 指数標記の `e` を取り出す

巨大な数は指数標記され、それを文字列化することによって `e` を取り出すことができます。

```javascript
let $e = [(2**70)+[]][0][18]
```

#### 浮動小数から `.` を取り出す

指数標記と同じように、小数点も文字列化できます。そこから、ドットを取り出すことができます。

```javascript
// "0.5" の "." を取り出す
let $dot = ([1/2]+[])[1]
```

#### 換字による難読化

特定の文字や文字列を関連性のない別の文字列で置き換えたペアのリストを作成し`replaceAll` 関数を使うなどして置き換える方法です。

```JavaScript
const List={
  "Jan":"e",
  "Feb":"x",
  "Mar":"a",
  "Apr":"m",
  "May":"p",
  "Jun":"l",
  "Jul":"@",
  "Aug":"c",
  "Sep":"o",
  "Oct":"j",
  "Nov":"-",
  "Dec":".",
}

console.log(List["Jan"]+List["Feb"]+List["Mar"]+"...")

```

例えば、`example亞example.com` は、`JanFebMarAprMayJunJanJulJanFebMarAprMayJunJanDecAugSepApr` に変換することができます。

#### 日付から `2` や `1` を得る

西暦2999年まではDateオブジェクトの`getFullYear` 関数の返り値を文字列化した際、その0番目の位置からから `2` の文字列を取得可能です。コンピューターの時刻設定に依存しますが、1999年以前または3000年以降ではエラーが表示されWebサイトに接続できないため、西暦2999年までは `2` が確実に取得できる事になります。

同様に `0` も1番目の位置から取得可能ですが、西暦2099年まで（残り76年ほど）となります。

2030年以降、2番目の位置から `3` などの数値が最大9年間使用可能です。1〜2年程度の公開のサイトに利用可能です。

```JavaScript
[new Date().getFullYear()+[]][0][0] // 2
```

また、月の数値を利用することは基本的に使用期限が短いために推奨されませんが、例外的に11〜12月の2ヶ月は0番目にある `1` を最大2ヶ月間使用可能です。

```JavaScript
const Nov = [new Date(new Date().setMonth(10)).getMonth()+[]][0][0] //11月
const Dec = [new Date(new Date().setMonth(11)).getMonth()+[]][0][0] //12月

console.log(Nov)
// 1

console.log(Nvo === Dec)
// true

console.log([new Date().getMonth()+[]][0][0])
```

#### `location.href`

現在のURLが格納されている `location.href` から `http://` までの間の文字列から `h` `t` `p` の文字をほぼ確実に取得する事ができます。また、Webサイトとメールアドレスのドメインが同じであれば、URLからドメイン部分の文字列を構成する事も可能です。

#### ランダム生成とハッシュの組み合わせ

メールアドレスの文字列をSHA256などのハッシュ値で保持しておき、ランダムな文字列を生成するコードから出力された文字列と照合する方法です。

xorshiftなどで乱数を実装すれば、シード値は固定可能であり、１回もしくは現実的な回数で任意の文字列が生成されるような、いわば鍵となるシード値を用意しておくことで、コードを実行するまではメールアドレスとして収集されにくくします。

---

### DOM操作と組み合わせる

JavaScriptのDOM操作と組み合わせることによって、botによるアドレス収集の対抗策になる可能性がありますが、メールアドレスが公開となる事に変わりがないため、可能であればメールフォームを利用する事が推奨されます。

- href属性ではなく別の属性から読み取る
- マウスイベントに応じて処理
- 画面にメールアドレスのリンクが表示された際に処理
- 時間経過によりメールアドレスを設定する

---

### その他の対策

#### 文字を画像として表示する

現在の文字認識ツール（OCR）は高速かつ高精度であり、画像で表示する事を想定したbotに対しては耐性はありませんが、そのような文字認識ツールを使用しない簡易的な収集プログラムには有効です。

#### アドレスをCSSによる擬似要素のcontentで表示

OCRに対しては画像で表示するのと同様に耐性がありませんが、CSSの擬似要素によるcontentでメールアドレスを表示する方法もあります。
テキスト画像の方法よりもファイルサイズを節約可能で、アドレスの変更時の対応もしやすいです。 `:after` と `:before` がありますので、分けて表記することが推奨されます。

#### QRコードで表示する
　
画像認識処理があるbotには耐性がありませんが、メールアドレスをQRコード化する事でスマートフォンを利用してメールを取得するのがよいでしょう。

#### 推測可能な受信用メールアドレスを使用しない

例えば、メールフォームからのメールを受け取るメールアドレスとして以下のようなシンプルな一般名詞のメールアドレスがあるとします。

```
contact亞example.com
form亞example.com
```

botは必ずしもWebページの内容を読む必要はなく、よく使用されるアドレスの辞書リストとドメインの組み合わせからメールを送信するケースも考えられます。上記のようなメールアドレスは真っ先に送信を試行される可能性があります。

そのため、アドレスを以下のように長くするか、ランダムな文字列をつけるなどしてbotにとって予測しにくい受信用メールアドレスを作成することがスパムメールの数を減らす上で推奨されます。

```
sub-green-mailbox-contact亞example.com
form-1a2b3c亞example.com
```

また、送信専用のメールアドレスは別に用意する事が推奨されます。
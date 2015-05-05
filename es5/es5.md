# ECMAScript 5 Specメモ

[azu/annotation-memo](https://github.com/azu/annotation-memo/ "azu/annotation-memo")にソースがあります。
(間違ってたらPull RequestやIssueとかお願いします)

参考文献: [【完全日本語訳＋解説】ECMA-262 Edition 5.1を読む](http://ecma262.info/ "【完全日本語訳＋解説】ECMA-262 Edition 5.1を読む")

## [Page 15](./Ecma-262_5.1.pdf#page=15)

> ECMAScript does not use classes such as those in C++, Smalltalk, 
> or Java.

ECMAScriptはクラスではない。ES6でも同様の記述

## [Page 15](./Ecma-262_5.1.pdf#page=15)

> prototype-based inheritance and shared properties.

代わりにプロトタイプベースである


## [Page 17](./Ecma-262_5.1.pdf#page=17)

> 4.3.6 native object object in an ECMAScript implementation whose 
> semantics are fully defined by this specification rather than by 
> the host environment NOTE Standard native objects are defined in 
> this specification. Some native objects are built-in; others may 
> be constructed during the course of execution of an ECMAScript 
> program. 4.3.7 built-in object object supplied by an ECMAScript 
> implementation, independent of the host environment, that is 
> present at the start of the execution of an ECMAScript program 
> NOTE Standard built-in objects are defined in this specification, 
> and an ECMAScript implementation may specify and define others. 
> Every built-in object is a native object. A built-in constructor 
> is a built-in object that is also a constructor. 4.3.8 host 
> object object supplied by the host environment to complete the 
> execution environment of ECMAScript NOTE Any object that is not 
> native is a host object.

- ネイティブオブジェクト
- ビルトインオブジェクト
- ホストオブジェクト

ネイティブはECMAScriptの仕様に書かれてるオブジェクトの事。
ホストオブジェクトはDOM APIとかブラウザが提供してるもの。
ビルトインオブジェクトも一種のネイティブオブジェクトだが、
実行時に提供される?

***

## [Page 20](./Ecma-262_5.1.pdf#page=20)
> Productions  of  the  lexical  and RegExp grammars are distinguished by having two colons ―::‖ as separating punctuation. The lexical and RegExp grammars share some productions.

字句文法と正規表現文法の区切り文字は`::`


## [Page 20](./Ecma-262_5.1.pdf#page=20)
> Productions of the numeric string grammar are distinguished by having three colons ―:::‖ aspunctuation.

数値文字列の区切り文字は`:::`


## [Page 20](./Ecma-262_5.1.pdf#page=20)
> It defines a set of productions, starting from  the  goal  symbol Program,  that  describe  how  sequences  of  tokens  can  form  syntactically  correct ECMAScript programs.

字句文法を繰り返し適応していって、
これが目標記号まで辿りつけない場合がプログラムの構文エラーがある。 = Syntax Errorとなる

字句文法を繰り返す => 構文解析を一回 => 構文文法が生成される

## [Page 20](./Ecma-262_5.1.pdf#page=20)
> Starting  from  a  sentence  consisting  of  a  single  distinguished  nonterminal,  called  the goal  symbol,  a  given context-free  grammar  specifies  a language,  namely,  the  (perhaps  infinite)  set  of  possible  sequences  of terminal symbols that can result from repeatedly replacing any nonterminal in the sequence with a right-hand side of a production for which the nonterminal is the left-hand side

目標記号 = 非終端記号

非終端記号は_斜体_で表現される via P22


## [Page 20](./Ecma-262_5.1.pdf#page=20)
> Productions of the syntactic grammar are distinguished by having just one colon ―:‖ as punctuation.

構文文法の区切り文字は`:`



## [Page 21](./Ecma-262_5.1.pdf#page=21)
> Productions  of  the  JSON  lexical  grammar  are  distinguished  by  having  two  colons  `::` as  separating punctuation

JSONの字句文法の区切り文字は`::`
JSONの構文文法の区切り文字はECMAScriptの構文文法を流用するので`:`となる

## [Page 21](./Ecma-262_5.1.pdf#page=21)

```
ArgumentList:
	AssignmentExpression
    ArgumentList , AssignmentExpression 
```

これはArgumentListが単体のAssignmentExpression **または** ArgumentList , AssignmentExpression となることを表現してる。

----

これを短縮したopt記号を使った

```
VariableDeclaration:
	Identifier Initialiser(opt) 
```

というのは以下の短縮形

```
VariableDeclaration:
	Identifier
    Identifier Initialiser
```

であるとか。
## [Page 22](./Ecma-262_5.1.pdf#page=22)
> [lookahead set]

![先読み](http://monosnap.com/image/OHO2tj2OlblNoIXxsWdfe7wSxmjJ1y.png)

というのは 先読み setで指定された文字列は、直後の入力トークンでは含まれてないということを示す。

つまり

```
LookaheadExample::
	n [ lookahead ∉ {1,3,5,7,9} ] DecimalDigits
```

というのは `n{0,2,4,6,8}` という感じになって、nの後に奇数含まない10進数の数字となる。




## [Page 24](./Ecma-262_5.1.pdf#page=24)
> 12© Ecma International 2011In order to facilitate their use in multiple parts of this specification,some algorithms, called abstractoperations, are named and written in parameterised functional form so that they may be referenced by name from within other algorithms.

ECMAScriptでは抽象演算と言われるアルゴリズムが定義されていて、色々なアルゴリズムが互いに参照してる。
ただし、ここで書かれるアルゴリズムより効率的なものはもちろんあり、このアルゴリズムをそのまま使う必要は必ずしもない。
アルゴリズムの再利用をしたいという目的。



## [Page 24](./Ecma-262_5.1.pdf#page=24)
> such  a  floating-point  number  must  be finite, and if it is +0or 0then the corresponding mathematical value is simply 0

ES5では+-0は数学的な値は単に0とする
ES6でも同じ記述。



## [Page 24](./Ecma-262_5.1.pdf#page=24)
> If  an algorithm is defined to ―throw an exception‖, execution of the algorithm is terminated and no result is returned.  

アルゴリズムが例外を投げるとき

- アルゴリズムは終了
- 結果は返さない
- "if an exception was thrown..." と表現されるところまで飛ぶ
	- そこから続ける
- 例外キャッチする処理がアルゴリズムにないならそこで終わり



## [Page 25](./Ecma-262_5.1.pdf#page=25)
>  If an actual source text is encoded in a form other than 16-bit code units it must be processed as if it was first converted to UTF-16

かならず最初にUTF-16にしてから始める

## [Page 25](./Ecma-262_5.1.pdf#page=25)
> Throughout the rest of this document, the phrase ―code unit‖ and the word ―character‖ will be used to refer to a 16-bit  unsigned  value  used  to  represent  a  single  16-bit unit of text. 

ES5だとSourceCharacter:: any Unicode code unitだけど
ES6だとSourceCharacter:: any Unicode code pointで、
10.1.1 Static Semantics: UTF16Encoding ( cp )でcode pointが決めてある。
## [Page 27](./Ecma-262_5.1.pdf#page=27)
> Line Terminator Characters

JSONがJSのサブセットじゃなくなってる問題の`\u2028`とかはES5だとどういう関係になってるんだろ?

---
## [Page 28](./Ecma-262_5.1.pdf#page=28)
> Syntax


グラマーは[ECMAScript Syntax Grammar 6th Edition / Draft](http://teramako.github.io/ECMAScript/ecma6th_syntax.html "ECMAScript Syntax Grammar 6th Edition / Draft")を使うと移動できるので見やすい




## [Page 29](./Ecma-262_5.1.pdf#page=29)
> Unicode escape sequences are also permitted in an IdentifierName, where they contribute a single character to the IdentifierName,  as  computed  by  the  CV  of  the UnicodeEscapeSequence(see  7.8.4). 

`\u0061 = 100` は `a= 100` と変換されてから解釈される。
## [Page 31](./Ecma-262_5.1.pdf#page=31)
> FutureReservedWord

ES6で代替ここにある将来の予約語は消化されて、ES6だとawait、asyncが代わりある。



## [Page 31](./Ecma-262_5.1.pdf#page=31)
> DivPunctuator ::one of

正規表現と区別するために
`DivPunctuator`というふうに除算演算子は分けてる = 目標記号


## [Page 36](./Ecma-262_5.1.pdf#page=36)
> A regular expression literal is an input element that is converted to a RegExp object (see 15.10) each time the literal  is  evaluated.  Two  regular  expression  literals  in  a  program  evaluate  to  regular  expression  objects  that never compare as ===to each other even if the two literals' contents are identical.

ES5から`/ /` は常に新しい正規表現オブジェクトを作るようになった。

[正規表現リテラルのes3からes5の間での変化 - ぶれすとつーる](http://nazomikan.hateblo.jp/entry/2014/03/12/020734 "正規表現リテラルのes3からes5の間での変化 - ぶれすとつーる")


## [Page 37](./Ecma-262_5.1.pdf#page=37)
> An  implementation  may extend  the  regular  expression  constructor's  grammar,

実装は正規表現コンストラクタのグラマーを拡張していいのか。

## [Page 42](./Ecma-262_5.1.pdf#page=42)
> This  procedurecorresponds exactly to the behaviour of the IEEE 754 ―round to nearest‖ mode

基本はIEEE 754互換の丸めモード。

1. 0.5未満
	- 切り下げ
2. 0.5より大きい
	- 切り上げ
3. 0.5の時
	- 偶数となる方へ丸め込み


0.5が1となるのをボウシするための、再近接偶数丸めモード(RNモード)という方法らしい
## [Page 42](./Ecma-262_5.1.pdf#page=42)
> An  Object  is  a  collection  of  properties.Each  property  is  either  a  named  data  property,  a  named  accessor property, or an internal property

- 名前付きデータプロパティ
- 名前付きアクセサプロパティ
- 内部プロパティ

の3つ

ES6だと

- データプロパティ
- アクセサプロパティ

になってる。

そして、OrdinaryオブジェクトとExoticオブジェクトという概念がでてくる。

"内部プロパティ"という言い方がES6ではなくなっていて、internal slotsが代わりっぽい。

## [Page 44](./Ecma-262_5.1.pdf#page=44)
>  its [[Prototype]] depends on the implementation. Every [[Prototype]] chain must have finite length

prototypeチェーンは有限の長さである。

## [Page 44](./Ecma-262_5.1.pdf#page=44)
> This  specification  defines  no  ECMAScript  language  operators  or  built-in  functions  that  permit  a  program  to modify an object‘s [[Class]] or [[Prototype]] internal properties or to change the value of [[Extensible]] from falseto true. Implementation  specific  extensions  that  modify  [[Class]],  [[Prototype]]  or  [[Extensible]]  must  not  violate  the  invariants defined in the preceding paragraph


`[[Extensible]]`をfalseからtrueにする物自体が仕様には存在していない。
これは不変性を保つためである。

この辺はES6だとSymbolやProxyHandlerなどによって大きく変わってる。
## [Page 53](./Ecma-262_5.1.pdf#page=53)
> n  the  following  algorithm,  the term ―Reject‖ means ―If Throwis true,  then  throw  a TypeErrorexception, otherwise return false‖.The algorithm contains steps that test various fields of the Property Descriptor Descfor specific  values.  

"Reject"は例外フラグが立ってるならthrow TypeError、そうじゃないならfalseを返すという意味
## [Page 54](./Ecma-262_5.1.pdf#page=54)
> Type Conversion and Testing

JavaScriptの型変換の定義

## [Page 59](./Ecma-262_5.1.pdf#page=59)
> The ToInt32 abstract operation is idempotent: if applied to a result that it produced, the second application leaves that value unchanged

ToUnit16/32には同じ値を二度適応しても、同じになる冪等性がある

## [Page 62](./Ecma-262_5.1.pdf#page=62)
> The SameValue Algorithm

値が同じかのチェックアルゴリズム

`SameValue(x, y)`

x == null なら trueになる

## [Page 62](Ecma-262_5.1.pdf#page=62&zoom=auto,-13,439)
> There are three types of ECMAScript executable code:

ES5だと

- global
- eval
- Function

の3つの実行可能なコードがある。


## [Page 63](Ecma-262_5.1.pdf#page=62&zoom=auto,-13,110)
> Strict Mode Code

strict modeも上の3つがそれぞれ対応がある。

- global
- eval
- Function


## [Page 63](Ecma-262_5.1.pdf#page=63&zoom=auto,-13,558)
> A Lexical Environment consists of an  Environment  Record  and  a  possibly  null  reference  to  an outerLexical  Environment.  Usually  a  Lexical Environment   is   associated   with   some   specific   syntactic   structure   of   ECMAScript   code   such   as   a FunctionDeclaration,  a WithStatement,  ora Catch clause  of  a TryStatementand  a  new  Lexical  Environment  is created each time such code is evaluated.

レキシカル環境。
ES5だといわゆるFunctionスコープとか、catchで生まれるスコープのこと。

レキシカル環境は内から外へとつながっていく感じ。
## [Page 63](Ecma-262_5.1.pdf#page=63&zoom=auto,-13,305)
> 10.2.1 Environment Records

と

> 10.2.1.1Declarative Environment Records

の違いは宣言的なEnvironment Recordsはimmutableなバインディングを提供する点。
## [Page 65](Ecma-262_5.1.pdf#page=65&zoom=auto,-13,813)
> The  behaviour  of  the  concrete  specification  methods  for  Declarative  Environment  Records  is  defined  by  the following algorithms.


基本的にバインディングとはそのメソッドが呼び出された箇所のEnvironment  Recordsを参照して、そこに対してバインディングを作ったり、消したり、そこから取得したりする操作。

## [Page 69](Ecma-262_5.1.pdf#page=69&zoom=auto,-13,454)
> 10.3.1Identifier Resolution

での識別子の解決がまさにそのLexicalEnviromentを使って、identifierの解決をしている。

## [Page 66](Ecma-262_5.1.pdf#page=66&zoom=auto,-13,487)
> 10.2.1.2Object Environment Records

`with`専用のバインディング環境

ES6だとこれらに加えて、
"8.1.1.5 Module Environment Records"がる


## [Page 72](Ecma-262_5.1.pdf#page=72&zoom=auto,-13,721)
> Set the [[Class]] internal property of objto "Arguments"

argumentsは`[[Class]]`の内部プロパティに保存されている。
## [Page 73](Ecma-262_5.1.pdf#page=72&zoom=auto,-13,82)
> 14.Else, strictis true so

strict modeではarguments.calleeとかが使えないのは、argument.cllee.callerに対して`thrower`という関数を設定しているため。


## [Page 75](Ecma-262_5.1.pdf#page=75&zoom=auto,-13,832)
> Expressions
> 11.1Primary Expressions

基本式！


## [Page 75](Ecma-262_5.1.pdf#page=75&zoom=auto,-13,832)
> 11.1.1The thisKeyword
> The thiskeyword evaluates to the value of the ThisBinding of the current execution context.

`this`はその実行コンテキストの`ThisBinding`の値を見ている
## [Page 79](Ecma-262_5.1.pdf#page=79&zoom=auto,-13,399)
> Properties are accessed by name, using either the dot notation:

dot notationとbracket notationはMDNじゃなくて仕様にも乗ってたのか

## [Page 85](Ecma-262_5.1.pdf#page=85&zoom=auto,-13,423)
> The  result  of  a  floating-point  multiplication  is  governed  by  the  rules  of  IEEE  754  binary  double-precision arithmetic:

NaNの場合どうなるかは書く演算子のところに書いてある。

## [Page 90](Ecma-262_5.1.pdf#page=90&zoom=auto,-13,372)
> The comparison x< y, where xandyare values, produces true, false, or undefined(which indicates that at least  one  operand  is NaN).

比較の結果はtrue, false, undefinedがあるのか

## 疑問

(normal, empty, empty)

というそれぞれが何なのかってどこに書いていてあるだろ?

(関数, 戻り値, 関数の引数) みたいな感じだけど

(type, value, args)

=> 8.9 The Completion Specification Type に書いてある

## [Page 113](Ecma-262_5.1.pdf#page=113&zoom=auto,-13,375)
> NOTEThe processes for initiating the evaluation of a Programand for dealing with the result of such an evaluation are defined by an ECMAScript implementation and not by this specification

`Program`の評価過程は実装依存?

## [Page 114](Ecma-262_5.1.pdf#page=114&zoom=auto,-13,553)
> 15Standard Built-in ECMAScript Objects

ECMAScriptオブジェクトについての定義


## [Page 114](Ecma-262_5.1.pdf#page=114&zoom=auto,-13,575)
> 15Standard Built-in ECMAScript Objects

いわゆるglobal

- `[[Call]]`を持っている組み込みオブジェクトはFunction
	- この組み込みオブジェクトの`[[Prototype]]`はFunction.prototype
`[[Call]]`を持っていない組み込みオブジェクトはObject
	- この組み込みオブジェクトの`[[Prototype]]`はObject.prototype
`


## [Page 114](Ecma-262_5.1.pdf#page=114&zoom=auto,-13,464)
> Many  built-in  objects  are  functions:  they  can  be  invoked  with  arguments.  Some  of  them  furthermore  are constructors

組み込み関数の呼び出しはnewとfunction callが存在する

簡単にまとめると

- 関数での呼び出し
	- `[[Call]]` の呼び出しと同じ
- new式での呼び出し
	- `[[Construct]]` の呼び出しと同じ

という分け方になる。

## [Page 115](Ecma-262_5.1.pdf#page=115&zoom=auto,-13,650)
> 15.1The Global ObjectThe unique global objectis created before control enters any execution context. 

グローバルオブジェクトは一意。
ウェブサイトだとwindowがこれに当たる

## [Page 116](Ecma-262_5.1.pdf#page=116&zoom=auto,-13,689)
> 1.If Type(x)is not String, return x

evalってstring以外はそのままの値を返すのか。

## [Page 117](Ecma-262_5.1.pdf#page=117&zoom=auto,-13,501)
> A reliable way for ECMAScript code to test if avalue Xis a NaNis an expression of the form X !== X. The result will be trueif and only if Xis a NaN

NaNかどうかを確実に判定する場合は`X !== X`を推奨。
`isNaN`は`ToNumber`を行うため確実ではないということかな。

ES6でもどうようの記述。
20.1.2.4 Number.isNaNは`ToNumber`しないからこっちでもどうような感じがするけど、Number.isNaN ( number )はstep 1でnumberだったらfalseがあるからかな。
## [Page 120](Ecma-262_5.1.pdf#page=120&zoom=auto,-13,439)
> Thissyntax  of  Uniform  Resource  Identifiers  is based  uponRFC  2396and  does  not  reflect  the  more  recent RFC 3986 which replaces RFC 2396

[URIに使ってよい文字の話 - RFC2396 と RFC3986 - 本当は怖い情報科学](http://freak-da.hatenablog.com/entry/20080321/p1 "URIに使ってよい文字の話 - RFC2396 と RFC3986 - 本当は怖い情報科学")

ES6でも同じ。
## [Page 125](Ecma-262_5.1.pdf#page=125&zoom=auto,-13,644)
> 4.If the argument Propertiesis present and not undefined, add own properties to obj as if by calling the standard built-in function Object.defineProperties with arguments obj and Properties

`Object.create`がnew Objectしたものへ`Object.defineProperties`で設定するという記述。
ES5だとのas ifだけど、ES6だとはっきり`Object.defineProperties`を呼ぶと変わってる。

## [Page 126](Ecma-262_5.1.pdf#page=126&zoom=auto,-13,777)
> If Type(O) is not Object throw a TypeError exception.


ES5だと基本的にseal(nonObject)だと例外を投げていたのに、
ES6だと

> 1. If Type(O) is not Object, return true.

という記述に変わって例外を投げなくなってる。

- [New ES6 draft now available, Rev 16](https://esdiscuss.org/topic/new-es6-draft-now-available-rev-16 "New ES6 draft now available, Rev 16")
- [tc39-notes/may-21.md at master · rwaldron/tc39-notes](https://github.com/rwaldron/tc39-notes/blob/master/es6/2013-05/may-21.md#41-objectfreeze "tc39-notes/may-21.md at master · rwaldron/tc39-notes")


該当の変更はRev 16で行われている

## [Page 127](Ecma-262_5.1.pdf#page=126&zoom=auto,-13,4)
> Object.keys ( O )

特にObject.keysは

> 1. If the Type(O) is not Object, throw a TypeErrorexception.

が

> 1. Let obj be ToObject(O).

となっていて、例外どころか処理が継続するようになってる。

これ元が例外投げてたので、それ前提のassetぐらいしかこの変更で壊れないから、そういう仕様変更入ったのかな?

- [Break the Web: Object staticメソッドがES6で仕様変更になった件について](https://gist.github.com/teppeis/c50743a60832560aa1df "Break the Web: Object staticメソッドがES6で仕様変更になった件について")


## [Page 130](Ecma-262_5.1.pdf#page=129&zoom=auto,-101,86)

```
new Function("a", "b", "c", "return a+b+c")
new Function("a,b, c", "return a+b+c")
new Function("a,b", "c", "return a+b+c")
```

は全部同じ。

## [Page 129](Ecma-262_5.1.pdf#page=129&zoom=auto,-101,555)
> Let Pbe the result of concatenating the previous value of P, the String","(a comma), and ToString(nextArg).

`,`で文字列を区切ってる。


## [Page 131](Ecma-262_5.1.pdf#page=130&zoom=auto,-101,27)
> The toStringfunction  is  not  generic;  it  throws  a TypeErrorexception  if  its thisvalue  is  not  a  Function object. Therefore, it cannot be transferred to other kinds of objects for use as a method

`Funcion.prototype.toString`はFunctionがthisじゃないと例外
## [Page 131](Ecma-262_5.1.pdf#page=130&zoom=auto,-101,27)
> An implementation-dependent representation of the function is returned. 

関数のtoStringはimplementation-dependent つまり実装DependencyなtoString

## [Page 131](Ecma-262_5.1.pdf#page=131&zoom=auto,-101,382)
> Function.prototype.bind (thisArg [, arg1 [, arg2, ...]])

`bind`について。
bindは新しいECMAScriptオブジェクトを作成して`this`とthisArgなどを移譲してあげる。
このECMAScriptオブジェクトはprototype,`[[Code]]`aをもたない。

- [Function.prototype.bindは何がいいのか - 枕を欹てて聴く](http://constellation.hatenablog.com/entry/20110113/1294846327 "Function.prototype.bindは何がいいのか - 枕を欹てて聴く")

bind作ったオブジェクトは、以下の内部プロパティが専用のモノを使う

- `[[Call]]`
- `[[Construct]]`
- `[[HasInstance]]`
## [Page 134](Ecma-262_5.1.pdf#page=134&zoom=auto,-101,842)
> 15.3.5.4[[Get]] (P)

Functionの`[[Get]]`はオブジェクトのものとは異なるロジックになる。

> Function  objects  use  a  variation  of  the  [[Get]]  internal  method  used  for  other  native ECMAScript  objects (8.12.3). 

これstrict modeのcallerチェックのためのステップがあるんだ。

ES6だとここにない感じがするけど、どっかにあるのかな。



## [Page 134](Ecma-262_5.1.pdf#page=134&zoom=auto,-101,642)
> An object, O,  is said to be sparseif the following algorithm returns true

配列の中で一つでもundefinedがあると疎の配列と言われる(定義)



## [Page 136](Ecma-262_5.1.pdf#page=136&zoom=auto,-101,699)
> Let funcbe the result of calling the [[Get]] internal method of arraywith argument "join".

`[].toString()` は joinを参照。
`[].toLocaleString()` は異なるので以下の様なことができる。

```
Array.prototype.join = function(){ return "ｼﾞｮｲﾝｼﾞｮｲﾝ"; };
[1,2,3].toString() == [1,2,3].toLocaleString(); // false
```
## [Page 141](Ecma-262_5.1.pdf#page=141&zoom=auto,-101,759)
> Array.prototype.sort (comparefn)

配列が疎だとsortは実装定義になる。。
## [Page 152](Ecma-262_5.1.pdf#page=152&zoom=auto,-101,733)
> 15.4.5.1[[DefineOwnProperty]] ( P, Desc, Throw )


## [Page 153](Ecma-262_5.1.pdf#page=153&zoom=auto,-101,420)
> The lengthproperty  of this Array object is  a  data property  whose  value is  always numerically  greater than the name of every deletable property whose name is an array index

`length`はいくら小さくしても、中にある要素数以上には必ずなる。
それを前提とした`[[DefineOwnProperty]]`などが存在しているため。
  

## [Page 160](Ecma-262_5.1.pdf#page=160&zoom=auto,-101,785)
> String.prototype.split (separator, limit)

splitのseparatorは正規表現でもglobalオプションを無視する。
## [Page 163](Ecma-262_5.1.pdf#page=163&zoom=auto,-101,838)
> The toLocaleUpperCasefunction is intentionally generic; it does not require that its thisvalue be a String object. Therefore, it can be transferred to other kinds of objects for use as a method

トルコの例外…    

## [Page 170](Ecma-262_5.1.pdf#page=170&zoom=auto,-101,842)
> 2.If precisionis undefined, return ToString(x).3.Let pbe ToInteger(precision).4.If xis NaN, return the String"NaN".

ToIntegerした結果がNaNだった時は"NaN"を返すという
何かアルゴリズム的に無駄がありそうな感じがある。

## [Page 172](Ecma-262_5.1.pdf#page=172&zoom=auto,-101,507)
> 15.8.2Function Properties of the Math Object

Noteの正確にアルゴリズムを定義しないのは、既存のCで書かれたものを使えるようにするためって話面白い。

## [Page 177](Ecma-262_5.1.pdf#page=177&zoom=auto,-101,735)
> A Date object contains a Number indicating a particular instant in time to within a millisecond. Such a Number is  called  a time  value.  A  time  value  may  also  be NaN,  indicating  that  the  Date  object  does  not  represent  a specific instant of time.

DateにはNumberはmsの精度で入ってて、時間値という。
## [Page 178](Ecma-262_5.1.pdf#page=177&zoom=auto,-101,8)
> Months are identified by an integer in the range 0to 11, inclusive. The mapping MonthFromTime(t) from a time value tto a month number is defined by:

0 スタートのmonth。特に説明はないけど。
## [Page 183](Ecma-262_5.1.pdf#page=182&zoom=auto,-101,93)
> 15.9.3.2new Date (value)

`Date.parse` を使ってる。

## [Page 184](Ecma-262_5.1.pdf#page=184&zoom=auto,-101,727)
> the value  produced  by Date.parseis  implementation-dependent  when  given  any  String  value  that  does  not conform to the Date Time String Format (15.9.1.15) and that could not be produced in that implementation by the toStringor toUTCStringmethod

`Data.parse`は実装依存

## [Page 191](Ecma-262_5.1.pdf#page=191&zoom=auto,-101,307)
> 15.9.5.44Date.prototype.toJSON ( key )

keyは使わないけど、汎用関数なのでとりあえずあるだけ
## [Page 192](Ecma-262_5.1.pdf#page=191&zoom=auto,-101,6)
> 15.10RegExp (Regular Expression) Objects

なぜかC++からも参照されてる正規表現の仕様

- [本の虫: C++の正規表現ライブラリ: std::regex](http://cpplover.blogspot.jp/2015/01/c-stdregex.html "本の虫: C++の正規表現ライブラリ: std::regex")b
## [Page 211](Ecma-262_5.1.pdf#page=211&zoom=auto,-101,534)
> Native Error Types Used in This Standard

JavaScriptのSyntaxErrorとかどこで起きてるか一覧がまとまってる。逆引きErrortype

ネイティブエラーの違いはnameとmessageぐらいで後はおなじ


## [Page 213](Ecma-262_5.1.pdf#page=213&zoom=auto,-101,422)
> The JSONobject  is  a  single  object  that  contains  two  functions, parse and stringify,  that  are  used  to  parse and    construct    JSON    texts.    The    JSON    Data    Interchange    Format    is    described    in    RFC    4627 <http://www.ietf.org/rfc/rfc4627.txt>. 


## [Page 214](Ecma-262_5.1.pdf#page=213&zoom=auto,-101,14)
> 202© Ecma International 2011The top level JSONTextproduction of the ECMAScript JSON grammar may consist of any JSONValuerather than being restricted to being  a JSONObjector a JSONArrayas specified by RFC 4627.

JSONはRFC 4627だけど、例外的に`[]`と`{}`以外のrootを認めている。

- [RFC 準拠的な JSON 形式について - Qiita](http://qiita.com/voluntas/items/48ec1b9dc781a1571545 "RFC 準拠的な JSON 形式について - Qiita")

なので実質的にRFC 7159と同じような感じ?
ES6だと[Standard ECMA-404](http://www.ecma-international.org/publications/standards/Ecma-404.htm "Standard ECMA-404")を参照してる。

ECMA 404もrootはarrayとobject以外でもよい。
## [Page 220](Ecma-262_5.1.pdf#page=220&zoom=auto,-101,708)
> JSON structures are allowed to be nested to any depth, but they must be acyclic. If valueis or contains a cyclic structure,  then  the  stringify  function  must  throw  a TypeErrorexception.  T


`JSON.stringify`で循環参照は例外を投げる。
## [Page 220](Ecma-262_5.1.pdf#page=220&zoom=auto,-101,546)
> An early erroris an error that can be detected and reported prior to the evaluation of any construct in the Programcontaining theerror.

early error以外は実行時エラーである。

strict modeのエラー、
## [Page 221](Ecma-262_5.1.pdf#page=220&zoom=auto,-101,36)
> An implementation shall report all errors as specified, except for the following:

実行環境、ユーザが拡張可能な領域など結構細かい部分がここに書かれてる。
SyntaxErrorを投げていい時の話とか。
## [Page 246](Ecma-262_5.1.pdf#page=246&zoom=auto,-101,842)
> Date.prototype.getYear ( )

2000年問題のためdeprecated
## [Page 247](Ecma-262_5.1.pdf#page=246&zoom=auto,-101,27)
> The Strict Mode of ECMAScript

Strict modeでエラーになるするべきところがまとまってる
## [Page 249](Ecma-262_5.1.pdf#page=248&zoom=auto,-101,53)
> Throughout:  In  the  Edition 3 specification  the  meaning  of  phrases  such as ―as if by the expression new Array()‖ are subject to misinterpretation. 

〜のようにという表現は控える方針。
ES6で`Object.create`がはっきりしたのはコレの方針を引き継いでるからかな?

## [Page 249](Ecma-262_5.1.pdf#page=248&zoom=auto,-101,53)
> AnnexD(informative)Correctionsand Clarifications in the 5thEditionwith Possible 3rdEdition Compatibility Impac

仕様の評価をする際にはAnnex Dを参考にするのが良さそう。

## [Page 251](Ecma-262_5.1.pdf#page=251&zoom=auto,-101,499)
> 15.4.4: In  Edition 5 all methods of Array.prototypeare intentionally  generic. In Edition 3 toStringand toLocaleStringwere not generic and would throw a TypeErrorexception if applied to objects that were not instances of Array

ES3では汎用的じゃなかったものがES5では意図的に汎用的になってる
## [Page 255](Ecma-262_5.1.pdf#page=255&zoom=auto,-101,475)
> 15.1.3:  Added notes clarifying that ECMAScript‘s URI syntax is based upon RFC 2396and not the newer RFC 3986. In the algorithm for Decode, a step wasremovedthat immediatelypreceded the current step 4.d.vii.10.a because it tested for a condition that cannot occur.

URI parse
## [Page 255](Ecma-262_5.1.pdf#page=255&zoom=auto,-101,475)
> 15.2.4.2: Edition 5 handling of undefinedand nullas thisvalue caused existing code to fail.  Specification modified to maintain compatibility with such code. New steps 1 and 2 added to the algorithm

`Object.prototype.toString` で 

- thisがundefinedの場合は`[object Undefined]`
- thisがnullの場合は`[object Null]`

を返すというステップの追加(互換性のために追加された)

```
Object.prototype.toString.call(null);
"[object Null]"
Object.prototype.toString.call(undefined);
"[object Undefined]"
```


## [Page 127](Ecma-262_5.1.pdf#page=127&zoom=auto,-101,413)
> 5.Return the Stringvalue that is the result of concatenating the three Strings"[object ", class, and "]"

`Object.prototype.toString.call([]) === "[object Array]"`

という感じで唯一?`[[Class]`を外に出せる定義。
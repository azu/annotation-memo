# ES6 Final Draft

[Final Draft](http://wiki.ecmascript.org/doku.php?id=harmony:specification_drafts#april_14_2015_rev_38_final_draft "Final Draft")を読んでのメモ

参考

- [ECMAScript 6 草案を斜め読みしていくメモ](https://gist.github.com/nanto/e8a6e9e02d04df615927 "ECMAScript 6 草案を斜め読みしていくメモ")
- [Taso.compute(more);](http://compute-taso.blogspot.jp/ "Taso.compute(more);")

----


## [Page 19](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=19&zoom=auto,-101,280)
> The  fifth  edition  of  ECMAScript  (published  as  ECMA-262  5thedition)  codifiedde  facto  interpretations  of  the language  specification  that have  become  common  among  browser  implementations  and  addedsupport  for new  features  that hademerged  since  the  publication  of  the  third  edition.

ES5はデフォルトスタンダートの文章化と新しい機能の追加に注視された。
またJSONの追加もここ。
## [Page 21](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=21&zoom=auto,-101,750)
> A conforming implementation of ECMAScript that provides anapplication programming interface that supportsprograms that need to adapt to the linguistic and cultural conventions used by different human languages and countriesmust  implement  the  interface  defined  by  the  most  recent  edition  of  ECMA-402  that  is  compatible with this specification. 

ECMA i18n APIとこの仕様は互換性あるよという話

- [Standard ECMA-402](http://www.ecma-international.org/publications/standards/Ecma-402.htm "Standard ECMA-402")

## [Page 27](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=27&zoom=auto,-101,655)
> 4.3.25symbolvalueprimitive value that represents a unique, non-String Object property key

Symbolが増えた。

## [Page 29](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=29&zoom=auto,-101,606)
> When  a  stream  of code  pointsis  to  be  parsed  as  an  ECMAScript ScriptorModule, 


ES5だとECMAScriptプログラムって表記だった所が、ES6だとscriptとmoduleになってる。

後JSON定義が5.1.5にあったけど、ECMA 404に移ったので消えてる。　　
## [Page 37](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=37&zoom=auto,-101,652)
> Some  operations  interpret  String  contents  as  UTF-16  encoded  Unicode  code  points.  In  that  case  the interpretation is

UTF-16とは何か、具体的なコードポイントについて書かれてる

## [Page 37](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=37&zoom=auto,-101,523)
> 6.1.5 The Symbol Type
> The Symboltype is the set of all non-Stringvalues that may be used as the key of an Object property (6.1.7).

SymbolはStringではないが、Objectのkeyとして使える。


## [Page 38](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=37&zoom=auto,-101,51)
> Well-Known Symbols

仕様のアルゴリズムから参照されるビルトインなSymbol。

`@@hasInstance` というSymbolの、
`[[Description]]`は"Symbol.hasInstance"という値を持つ。
また、それぞれのSymbolは値かメソッドとなってる。

## [Page 42](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=41&zoom=auto,-101,16)
> The “Signature” column


## [Page 43](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=42&zoom=auto,-101,148)
> Table 5—Essential Internal Methods

このシグネチャーの読み方

```
// method 
[[SetPrototypeOf]]
// signature
(Object|Null)→ Boolean
```

これは

```
SetPrototypeOf(Object or Null) : Boolean
```

なので、Object or Nullを渡す関数で、返り値はBooleanという感じ。

ES5だと**Signature**じゃなくて**Value Type Domain**という表現だった。


> azu_re: #ES読書 ES5だとValue Type Domainで、ES6だとSignatureに表現が変わった。表現を簡易化するためにこうなったのかな? http://t.co/n5V3MWcH3X
> https://twitter.com/azu_re/status/595234567369326594


## [Page 44](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=44&zoom=auto,-101,729)
>  If  any  specified  use  of  an internal  method  of  an exotic  object  is  not  supported  by  an implementation, that usage must throw a TypeErrorexception when attempted.


## [Page 25](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=25&zoom=auto,-101,294)
> ordinary object exotic object



- ordinary object
	- 
- exotic object
- 4.3.8 standard object
	- ECMAScriptによって完全にセマンティクスが決まるもの
	- ES5だとネイティブオブジェクト
- 4.3.9 built-in object
	- 組み込みオブジェクト

参考:

- [Meta Object Protocol, aka. MOP](https://github.com/rwaldron/tc39-notes/blob/c61f48cea5f2339a1ec65ca89827c8cff170779b/es6/2012-11/nov-27.md#meta-object-protocol-aka-mop "Meta Object Protocol, aka. MOP")


`ReturnIfAbrupt`というのは今まで暗黙的に例外を投げてた所を、明示的に投げられるようにするためのアルゴリズム
## [Page 44](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=44&zoom=auto,-101,677)
> Invariants of the Essential Internal Methods

Internal methodの不変性
invariants = 不変性


## [Page 44](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=44&zoom=auto,-101,633)
> Ordinary ECMAScript Objects as well as all standard exotic objects in this specification maintain these invariants. ECMAScript Proxy objects maintain these invariants by means of runtime checks on the result of traps invoked on the [[ProxyHandler]] object.

"ordinary object" as "standard exotic objects"...
Proxy objectもこの不変性は維持する。

## [Page 46](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=46&zoom=auto,-101,811)
> Well-Known Intrinsic Objects6.1.7.4


Well-Known Symbolsみたいな感じで、ビルトインオブジェクト版。
同じくアルゴリズムから`%Array%`みたいな感じで参照する。
`%Array`はArrayとおなじでArrayコンストラクタを意味する。

- Intrinsic Name : `%Array%`
- Global Name: Array

本質的な名前が`%`

## [Page 50](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=49&zoom=auto,-101,259)
> The List and Record Specification Type6.2.1



## [Page 50](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=50&zoom=auto,-101,842)
> The CompletionRecordSpecification Type 6.2.2

ECMAScriptの仕様書型を定義してて、ステートメントをとかを評価してる時に出てくる、Record。

![completion record fields](http://monosnap.com/image/hZLQ7kMfeTMHuSch1hVunyFDTfFaOP.png)

`[[type]]`がnormalだと正常に終わって、throwだったら例外を投げる終わり方。
ES5だと"8.9 The Completion Specification Type"に定義されたけど分かりやすくなった。

アルゴリズムのステップでいきなり `(normal, empty, empty)`とかでてきたらこれのことだった。

`([[type]], [[value]], [[target]])`

`[[target]]`はコントロールを渡す先?


## [Page 50](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=50&zoom=auto,-101,507)
> The term “abrupt completion” refers to any completion with a [[type]]value other than normal.

abrupt completion(中途完了)という用語は`[[type]]`の値が**normal以外**であることを言ってる。

いろんな所で出てくる`ReturnIfAbrupt`はこれをチェックしてる。

`ReturnIfAbrupt`は今まで暗黙的に例外を投げていたのを、明示的に例外投げれるようにチェックするために導入された?

- [tc39-notes/nov-27.md at c61f48cea5f2339a1ec65ca89827c8cff170779b · rwaldron/tc39-notes](https://github.com/rwaldron/tc39-notes/blob/c61f48cea5f2339a1ec65ca89827c8cff170779b/es6/2012-11/nov-27.md#meta-object-protocol-aka-mop "tc39-notes/nov-27.md at c61f48cea5f2339a1ec65ca89827c8cff170779b · rwaldron/tc39-notes")

ReturnIfAbrupt(argument). 

1. argumentがabrupt completionならば、return arguments.
2. else if `arguments.[[value]]`を返す

abrupt completionはメッチャ参照されてる用語なのに、定義がさらっと書きすぎてる。


## [Page 52](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=51&zoom=auto,-101,258)
> The Reference Specification Type

- base
- referenced name
- strictg reference

の3つから構成される。
`base`の値はundefined,Object,Boolean,Symbol,Number と Envrioment Recordが可能

Super Referenceの時は`base`がEnvrioment Recordにはならない。(代わりに`thisValue`をSuper Referenceが持っている。
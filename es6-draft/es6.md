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

**Completion Record**という名前

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
2. else if `argument.[[value]]`を返す

abrupt completionはメッチャ参照されてる用語なのに、定義がさらっと書きすぎてる。


## [Page 52](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=51&zoom=auto,-101,258)
> The Reference Specification Type

- base
- referenced name
- strictg reference

の3つから構成される。
`base`の値はundefined,Object,Boolean,Symbol,Number と Envrioment Recordが可能

Super Referenceの時は`base`がEnvrioment Recordにはならない。(代わりに`thisValue`をSuper Referenceが持っている。
## [Page 53](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=53&zoom=auto,-101,586)
> IsAccessorDescriptor ( Desc )

Property Descriptor のAccessorが使えるかの判定をする。
`Desc.[[Get]` や `Desc.[[Set]`が実装されているかが判定に使われている。

## [Page 54](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=53&zoom=auto,-101,37)
> FromPropertyDescriptor ( Desc )


## [Page 54](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=53&zoom=auto,-101,37)
> ToPropertyDescriptor ( Obj )

これはObject <-> Property Descriptorを行うabstract operation.

新しいObjectを作るのは`ObjectCreate(%ObjectPrototype%)`で作ったオブジェクトにPropertyDescriptorを設定していく感じ。
abstrct operationでは基本的にWell-Known Intrinsic Objectsで操作を行っている。
## [Page 55](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=55&zoom=auto,-101,624)
> The Lexical Environment and Environment Record types are used to explain the behaviour of name resolution in nested functions and blocks. 

Lexical Environmentは関数スコープでの名前解決とかに使われるよ。詳しくは8.1で
## [Page 56](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=56&zoom=auto,-101,750)
> ToPrimitive( input [, PreferredType] )

Primitiveへの変換。
Objectへの変換がES5とは違う。(`[[DefaultValue]]`を呼ぶという記述が無くなってる)

- `PreferredType`がある場合は、OrdinaryToPrimitiveのhintにそれを使う
- inputが`@@toPrimitive`を持ってるならそっちを使う

という感じになってる。

`OrdinaryToPrimitive(input, hint)`

`OrdinaryToPrimitive`はhintがstringならtoString、numberならvalueOfを使うみたいなのを決めて呼ぶ仕組み



## [Page 57](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=57&zoom=auto,-101,757)
> When ToPrimitiveis  called  with  no  hint,  then  it generally behaves  as  if  the  hint were  Number.  However, objects may over-ride this behaviour by defining a @@toPrimitive method. Of the objects defined in this specification onlyDate objects(see 20.3.4.45)and Symbol objects (see 19.4.3.4) over-ride the default ToPrimitive behaviour.Date objects treat no hintas if the hint were String

デフォルトだと大体Numberになるけど、オブジェクトは`@@toPrimitive`をoverwriteしてたらそっちが使われるので、例えばDateオブジェクトはhintなしでもstringになって、toStringになるという話。

参考: ES5以下の話

- [valueOfとtoStringとToPrimitive - os0x.blog](http://os0x.hatenablog.com/entry/20100916/1284650917 "valueOfとtoStringとToPrimitive - os0x.blog")
## [Page 59](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=59&zoom=auto,-101,582)
> Runtime Semantics: MV’s

MVとは "mathematical value (MV)"
## [Page 63](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=63&zoom=auto,-101,751)
> Throw a TypeErrorexception.

SymbolはToStringすると例外を投げる?

`Symbol("desc").toString()`は例外を投げない。
// Symbol("desc") という文字列を返す

別途Symbol#toStringの定義があって`SymbolDescriptiveString`に文字列で変換されるだけなので、ToStringとは別のアルゴリズムを辿る。

一方、`Symbol("desc") + ""` は例外を投げる => `ToString(symbol)`を呼ぶため。

これは

```js
var s = Symbol("ooo");
var newSymbol = s + "name";
```

みたいのを防止するための仕組みと理解。
つまり暗黙的な変換に頼ったものをできるだけ排除している。


> If x is an object, x + '' performs ToString(ToPrimitive(x, no hint)), whereas String(x) performs ToString(ToPrimitive(x, hint String)). So both expressions are not always interchangeable.


- ["types & grammar": explain Symbol coercion in ch4 · Issue #274 · getify/You-Dont-Know-JS](https://github.com/getify/You-Dont-Know-JS/issues/274)
- [String(symbol)](https://esdiscuss.org/topic/string-symbol#content-11)


## [Page 65](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=65&zoom=auto,-101,664)
> IsArray ( argument )

`IsArray` は Array exotic オブジェクトなら trueを返す。
また、Proxy exoticオブジェクトでそのオブジェクトの`[[ProxyTraget]]`がArrayであってもtrueを返す。

## [Page 67](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=67&zoom=auto,-101,832)
> SameValueZero(x, y)


## [Page 69](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=69&zoom=auto,-101,564)
> GetV (V, P)

primitive?
## [Page 71](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=71&zoom=auto,-101,349)
> HasProperty

prototype辿る版のHasOwnProperty 
## [Page 72](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=71&zoom=auto,-101,45)
> Call(F, V, [argumentsList])

`[[Call]]` のやつ

FはFunction object
VはValue
argumentsListはargs

## [Page 72](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=72&zoom=auto,-101,679)
> Construct (F, [argumentsList], [newTarget])

こっちは`[[Construct]]`の実体。

ES5だと[Page 114](http://azu.github.io/annotation-memo/es5/ "Page 114") で書いてたように、通常の関数呼び出しはCall、newでの呼び出しがConstructになる。


## [Page 72](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=72&zoom=auto,-101,566)
> NOTEIf newTargetis not passed, this operation is equivalent to: new F(...argumentsList)

`new F()`は代入されてないので、newTargetが存在しない。
## [Page 74](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=74&zoom=auto,-101,788)
> OrdinaryHasInstance (C, O)

prototypeをたどって、CはOのインスタンスなのかを判定する。
instanceofみたいな感じだけど

## [Page 74](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=74&zoom=auto,-101,603)
> SpeciesConstructor ( O, defaultConstructor )

`@@species` はConstuctorが入るとこみたいな。
サブクラスで`Symbol.species`を定義しておくと、instanceofの判定でそこが使われる?

- [Classes in ECMAScript 6 (final semantics)](http://www.2ality.com/2015/02/es6-classes-final.html "Classes in ECMAScript 6 (final semantics)")

## [Page 66](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=66&zoom=auto,-101,393)
> SameValue(x, y)

`Object.is( value1, value2)`がこれそのままなので、ユーザランドで使える。


## [Page 77](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=77&zoom=auto,-101,661)
> Executable Code and Execution Contexts


## [Page 78](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=77&zoom=auto,-101,73)
> A module environmentis a Lexical Environment that contains the bindings for the top level declarations of a Module.  It  also  contains  the  bindings  that  are  explicitly  imported  by  the Module.  The  outer  environment  of  a module environment is a global environment

ES6ではmodule envが追加された。
このLexical EnvにはModuleの宣言のbindingsが定義されている。
bindingとはどのmodule**から**importされてるか。

module env -> global env
## [Page 79](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=79&zoom=auto,-101,732)
> HasSuperBinding()

`super`についてのbindingを持ってるかが追加


## [Page 79](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=79&zoom=auto,-101,732)
> WithBaseObject()

`with` 専用のものが追加。

_Declarative Environment Records_では、`WithBaseObject()`は常に`undefiened`を返す。

逆にObject Environment Records、つまりwith専用のenv recordsではtrueを返すことがある。

## [Page 81](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=81&zoom=auto,-101,442)
> Object Environment Records


## [Page 83](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=83&zoom=auto,-101,371)
> 8.1.1.2.10 WithBaseObject()

`withEnvironment`というフラグを見てtrueかfalseを返す。

> 13.11.7 Runtime Semantics: Evaluation

`withEnvironment`をtrueにしてくれるのはwith構文のアルゴリズムで定義されている。つまり`with()`を使うと、新しいObject Environmentが作られて、Object Environment Recordsの`withEnvironment`がtrueに変更される。


## [Page 84](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=84&zoom=auto,-101,824)
> [[HomeObject]]

Function Environment Recordsは`[[HomeObject]]`というフィールドを持っていて、これは`super`プロパティが指す先(つまりParent?)になる。

ArrowFunctionはこれがない。

## [Page 91](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=91&zoom=auto,-101,844)
> 8.1.1.5 Module Environment Records

Module Enviroment Recordはdeclarative Environment Recordの一種。
+ immutable import  bindingsを記憶するRecordを持ってる

## [Page 91](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=91&zoom=auto,-101,495)
> NOTEBecause a Moduleis always strict mode code, calls to GetBindingValue should always pass trueasthe value ofS.

Moduleは常にstrict modeである。
## [Page 91](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=91&zoom=auto,-101,370)
> The concrete Environment Record method DeleteBinding for moduleEnvironment Records refuses to delete bindings.

Moduleは immutableではあるけど、bindingの削除はできない。

## [Page 92](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=92&zoom=auto,-101,837)
> 8.1.1.5.4 GetThisBinding

> 8.1.1.5.3 HasThisBinding()

常にtrueを返す

> > 8.1.1.5.4 GetThisBinding()
常にundefinedを返す

- [Babelで top level this が undefinedになって困った件 - console.lealog();](http://lealog.hateblo.jp/entry/2015/04/27/203147 "Babelで top level this が undefinedになって困った件 - console.lealog();")
- https://twitter.com/azu_re/status/592995278715650048

BabelはコードをModuleとして扱うという前提があるので、Moduleのtop levelの8.1.1.5.4 GetThisBindingがundefinedを返すとなり仕様

## [Page 93](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=93&zoom=auto,-101,298)
> NewModuleEnvironment(E)

呼び出す時は`NewModuleEnvironment(realm.[[globalEnv]]`しかないので、module envのouterはglobalとなる。

> 8.3.2 GetThisEnvironment ( )

でModule Envの`HasThisBinding()`はtrueを返すので、module envの`GetThisBinding()`を参照する。
`GetThisBinding()`は常にundefinedを返すので、moduleのtop levelにある`this`はundefinedを返すといえる。


まとめ:

- [ES6 moduleのtop levelにある`this`の値は何になるのか? | Web Scratch](http://efcl.info/2015/05/06/this-is-es6-module/ "ES6 moduleのtop levelにある`this`の値は何になるのか? | Web Scratch")
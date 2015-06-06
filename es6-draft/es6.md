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

要は[especially/intrinsics.js at master · domenic/especially](https://github.com/domenic/especially/blob/master/intrinsics.js "especially/intrinsics.js at master · domenic/especially")を見る感じ

```
exports["%Object%"] = Object;
exports["%ObjectPrototype%"] = Object.prototype;
exports["%ObjProto_toString%"] = Object.prototype.toString;
exports["%Function%"] = Function;
exports["%FunctionPrototype%"] = Function.prototype;
exports["%Array%"] = Array;
exports["%ArrayPrototype%"] = Array.prototype;
exports["%String"] = String;
exports["%StringPrototype%"] = String.prototype;
exports["%Boolean%"] = Boolean;
exports["%BooleanPrototype%"] = Boolean.prototype;
```

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


## [Page 94](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=94&zoom=auto,-101,842)
> 8.2CodeRealms

コードは評価される前にRealmに関連付けられる。
Realmは、その関数がどのコンテキストで実行されてるのかを表現するために使われたりする感じ 

Realmはintrinsic objectsで構成される。
(  intrinsic は Intrinsic Name : `%Array%` みたいなところででてきた )

Realm Record

- `[[intrinsic]]`
- `[[globalThis]]`
- `[[globalEnv]]`
- `[[templateMap]]`

を持っている。


## [Page 94](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=93&zoom=auto,-101,117)
> [[templateMap]]

<del>Template objectは`[[templateMap]]`によって正規化されたもの?</del>

2015-05-17追記

(Symbolと[[templateMap]]はJSCだとWeakMapで実装されてる。)
Template tagの第一引数に来るtemplate objectは一意なオブジェクトなので、realm recordに[[templateMap]]に保存して利用している。そのために`[[templateMap]]`という保存場所が仕様に定義されている。

SymbolもSymbol.forで一意のものを取得できるので、同じような保存場所がグローバルに存在してる


## [Page 95](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=95&zoom=auto,-101,603)
> Execution Contexts

実行コンテキストの話。
コードは実行コンテキストをスタック的にもっていて、pushしたりpopしてる。
つまり、この論理的なスタックの一番上にあるのが現在の実行コンテキストになる。

で、実行コンテキストはどんな状態を保存していたりしているかについて。


## [Page 96](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=95&zoom=auto,-101,28)
> State Components for All Execution Contexts

実行コンテキストが持つ状態要素

- code evalution state
- Function
- Realm

先ほど書いてたように実行コンテキストがRealmを持っている。

ES5だと`ThisBinding`という状態要素が存在していて、
これによりThisの値を見たりしていたが、　ES6ではEnviroment Recordに定義された`HasThisBinding()`をみてチェーンしていくので実行コンテキストが`this`の値を持つことはない。

これは、Arrow Functionなど`this`を持たないやつが存在しているからだと思う。

また現在の実行コンテキストの状態要素をそれぞれ

- Function = active function object
- Realm = current Realm

と言ったりする。


## [Page 96](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=96&zoom=auto,-101,532)
> Additional State Componentsfor ECMAScript Code Execution Contexts

Table 22—State Components for All Execution Contexts
にLexicalEnvとかなくて、Table23でAdditionalになってるのはLexicalEnvを持たない実行コンテキストがあるのかな?

このLexicalEnvironmentとVariableEvnromentはES5の時にもあって、その実行コンテキストに紐づく識別子(変数)とかをまとめるRecordを持ってる。



## [Page 96](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=96&zoom=auto,-101,532)
> Additional State Components for GeneratorExecution Contexts

Generatorはさらに追加で`Generator`という状態要素を持っている
## [Page 97](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=97&zoom=auto,-101,781)
> GetThisEnvironment ( )

ES5だと実行コンテキストの`ThisValue`を見るだけだったけど、
現在の実行コンテキストのLexicalEnvironmentのRecordをみて、そのRecordが`HasThisBinding()`がtrueを返すなら`GetThisBinding()`でthisの値が撮れるという感じになってる。

これによりそれぞれのLexicalEnvironmentであるmodule Environment Records特有の`this`の解決方法などが定義できるような感じになった。


## [Page 98](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=97&zoom=auto,-101,111)
> Jobs and Job Queues


## [Page 98](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=98&zoom=auto,-101,794)
> Execution of a Job can be initiated only when there is no running execution context and the execution context stack  is  empty.  

Jobは実行コンテキストのスタック

## [Page 98](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=98&zoom=auto,-101,655)
> PendingJob Record Fields

PendingJobというのがJobの抽象的なオブジェクト

- `[[Job]]` Jobの名前
- `[[Arguments]]`
- `[[Realm]]`
- `[[HostDefined]]` - 追加情報

このPendingJobを貯めるところがJob Queue


## [Page 98](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=98&zoom=auto,-101,655)
> Required Job Queues

Job Queues Recordのfiledは

- ScriptJobs - ECMAScritp _Script_ や _Module_ のソーステキストが入ってる
- PromiseJobs - Promise

の2種類

Queueから一番うえを取り出して使っていく。
FIFO order.


## [Page 98](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=98&zoom=auto,-101,291)
> EnqueueJob (queueName, job, arguments)8.4.1

PendingJobの追加



## [Page 99](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=99&zoom=auto,-101,271)
> ECMAScript Initialization() 

Jobsやコードを実行するときの初期化処理について

1. Realmを作る
2. 実行コンテキストの作成
3. 実行コンテキストの`Function`はnull
4. 作ったRealmを実行コンテキストに設定
5. 作った実行コンテキストを実行コンテキストのスタックへ追加
6. ...



## [Page 100](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=100&zoom=auto,-101,666)
> Ordinary and Exotic Objects Behaviours 


## [Page 100](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=100&zoom=auto,-101,666)
> All ordinary objects have an internal slotcalled [[Prototype]].

ordinary objectsは`[[Prototype]`という内部スロットをもっている。また`[[Exantensible]]`というスロットも持ってるよ。


- `[[Prototype]]`
- `[[Exantensible]]`

## [Page 105](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=105&zoom=auto,-101,444)
> OrdinaryCreateFromConstructor(constructor, intrinsicDefaultProto, internalSlotsList )

ordinary objectsというのはこの抽象操作によって作成される。
## [Page 106](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=106&zoom=auto,-101,568)
> ECMAScript Function Objects

Function objectというのはコードとLexicalEnvironmentをカプセル化したもので、ダイナミックなコード実行を行うためのもの。

## [Page 107](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=107&zoom=auto,-101,725)
> All ECMAScript function objects have the [[Call]] internal method defined here. 

ECMAScript function objectsは`[[Call]]`を持つ


## [Page 107](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=107&zoom=auto,-101,477)
> [[Call]]( thisArgument,argumentsList)


`.call(this, args)`
## [Page 109](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=109&zoom=auto,-101,843)
> Assert: If functionKindis present, its value is either "normal", "non-constructor"or"generator"

Table 27 — Internal Slots of ECMAScript Function Objectsによると、ECMAScript Function Objectsは`[[FunctionKind]]`というスロットにFunctionの種類を持ってる。

normal , calssConstructor, generator
の3つ


## [Page 114](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=114&zoom=auto,-101,654)
> Built-in Function Objects


## [Page 114](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=114&zoom=auto,-101,654)
>  ECMAScript function objects  (9.2)  whose  behaviour  is  provided  using  ECMAScript  code  or  as  implementation  provided  exotic function objects whose behaviour is provided in some other manner.

`Function.prototype`の事っぽい

exotic function objectsとして提供される。
exotic function objectsというのは9.2で定義されたordinary objectsの挙動に加えて、`[[Prototype]]`、`[[Extensible]]`、`[[Realm]]`を持っている。

で、`[[Prototype]]`の初期値はきまっていて`%FunctionPrototype%`が初期値となる。

## [Page 115](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=114&zoom=auto,-101,73)
> The  [[Call]]  internal  method  forabuilt-in  functionobject Fis called  with parametersthisArgumentand argumentsList, a List of ECMAScript language values.The following steps are taken

 ECMAScript function objectsも`[[Call]]`が定義されている。
 
`9.2.1 [[Call]] ( thisArgument, argumentsList)` とはOrdinaryCall 的なのがなくなって、Realmについてが増えたりしてる所が違う。
## [Page 115](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=115&zoom=auto,-101,270)
> Bound Function Exotic Objects

`bind`によって作られたFunctionもexotic objects。

```js
var boundFn = fn.bind(this);
```

みたいなので、Bound Function Exotic Objectsももちろん`[[Call]]`を持っているためCallable.



## [Page 116](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=116&zoom=auto,-101,831)
> 9.4.1.1 [[Call]]( thisArgument,argumentsList)
> 9.4.1.2 [[Construct]](argumentsList, newTarget)

こっちもまた異なる`[[Call]]`などを定義してる。
つまり関数をbindしてできた関数は通常のものとはまた別のアルゴリズムで動いてるという事。

- http://constellation.hatenablog.com/entry/20110113/1294846327

## [Page 117](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=117&zoom=auto,-101,748)
> Array exotic objects always have a non-configurable property named "length".

Arrayのexotic objectsは`.length`というものをもっている。
また`[[DefineOwnProperty]]`も独自にもっていて、オブジェクトとは`hasOwnProtperty`のアルゴリズムが異なる
## [Page 118](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=118&zoom=auto,-101,681)
> ArraySpeciesCreate(originalArray, length)

`@@species`を参照してる。
## [Page 119](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=119&zoom=auto,-101,441)
> String Exotic Objects

SringもArrayと似た感じでlengthや`[[DefineOwnProperty]]`の定義がある。
また`[[StringData]]`というordinary objectsのスロットがある。


## [Page 121](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=121&zoom=auto,-101,786)
> Arguments Exotic Objects

Arguments。
`[[ParameterMap]]`というスロットにパラメータのバインディングをもっているが、このスロットは`Object.prototype.toString`でしか使われない。
## [Page 125](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=125&zoom=auto,-101,771)
> Integer Indexed Exotic Objects

TypedArrayとか

## [Page 128](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=128&zoom=auto,-101,786)
> A module  namespace  objectis  an  exotic  object  that  exposes  the  bindings  exported  from  an  ECMAScript Module

Moduleの名前空間について。

## [Page 128](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=128&zoom=auto,-101,786)
> [[Exports]]


## [Page 128](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=128&zoom=auto,-101,786)
> The list is ordered as if an Array of those string values had been sorted using Array.prototype.sortusing SortCompare as comparefn

Internal Slotsof Module Namespace Exotic Objects
Module名前空間の`[[Exports]]`はsortされている。

## [Page 130](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=130&zoom=auto,-101,741)
> ModuleNamespaceCreate (module, exports)

Module Recordとexports(文字列の配列)を受け取る。
exportsは`[[Exports]]`になる。
## [Page 130](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=130&zoom=auto,-101,511)
> 9.5ProxyObject Internal Methodsand Internal Slots


## [Page 130](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=130&zoom=auto,-101,432)
> very   proxy objects hasan internal   slotcalled   [[ProxyHandler]].   The   value   of [[ProxyHandler]] is anobject, called the proxy’s handler object, or null. Methods

proxyオブジェクトは`[[ProxyHandler]]`というinternal slotを持っている。
`[[ProxyHandler]].Call(proxy | null, args);`という感じで使う。



## [Page 131](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=131&zoom=auto,-101,791)
> A proxy’s handler object does not necessarily have  a  method  corresponding  to  every  essential  internal  method. 

proxy handler objectは必ずしもそれぞれ内部メソッドと関連付けたメソッドを持っている必要はない。
## [Page 131](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=131&zoom=auto,-101,590)
> The [[ProxyHandler]] and [[ProxyTarget]] internal slots of a proxy object are always initialized when the object is created and typically may not be modified.

`[ProxyHandler]]`と`[[ProxyTarget]]`は初期化したら変更はできなくて、revokedしかできないデザイン。
revokeするとnullになる。


## [Page 131](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=131&zoom=auto,-101,527)
> Because proxy objects permit the implementation of internal methodsto be provided by arbitrary ECMAScript code, it is possible to define a proxy object whose handler methods violates the invariants defined in 6.1.7.3.


内部的な不変性を崩してしまう可能性が出てくるから



## [Page 136](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=136&zoom=auto,-101,429)
> When the [[Delete]] internal method ofa Proxy exotic objectOis called with property keyPthe following steps are taken

Proxyオブジェクトにdeleteをカマしたおき、。
普通に`[[ProxyTraget]].[[Delete]]`を呼ぶだけ
## [Page 138](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=137&zoom=auto,-101,24)
> [[Call]](thisArgument, argumentsList) 9.5.13

Proxyの基本的な流れ

`[[Call]](thisArgument, argumentsList)｀ケース

1. `[[ProxyHandler]]` is handler
2. handlerをチェック
3. `[[ProxyTarget]` is target
4. `GetMethod(handler, "apply")`という感じで`handler`からメソッドを取り出す。この時**trap**という変数に入れる。
5. `trap`のチェック
6. `Call(trap, handler, <<target, thisArguments, argmentsList>>)` 呼ぶ


## [Page 140](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=139&zoom=auto,-101,244)
> Static Semantics:  

噂通り、コードポイント的な解説が増えている。
## [Page 140](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=140&zoom=auto,-101,680)
> 10.2　Types of SourceCode

ECMAScriptコードは4種類ある

- Globalコード = ECMAScript _Script_として扱う
- Evalコード = ECMAScript _Script_として扱う
- Functionコード = パースに制約がある
- Moduleコード = これはModuleBodyを提供する。モジュールが初期化されるときに実行される。
## [Page 140](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=140&zoom=auto,-101,516)
> Strict Mode Code

ES6ではデフォルトがstrict modeとなるコードがある。
strict modeとなるものを列挙すると

- ディレクティププロローグで"use strict"したコード
- Moduleコード
- Class宣言、式
- Evalコードで"use strict"
- Functionコードで"use strict"


## [Page 141](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=140&zoom=auto,-101,187)
> ECMAScript code that is not strict mode code is called non-strict code

strict modeではないコード non-strict という

[tc39-notes/jan-29.md at master · rwaldron/tc39-notes](https://github.com/rwaldron/tc39-notes/blob/master/es6/2015-01/jan-29.md#const-in-sloppy-mode "tc39-notes/jan-29.md at master · rwaldron/tc39-notes")


## [Page 141](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=140&zoom=auto,-101,39)
> 10.2.2 Non-ECMAScript Functions

そんな概念あるのか

## [Page 141](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=141&zoom=auto,-101,641)
> ECMAScript Language: Lexical Grammar

InputElementRegExpOrTemplateTailを例にグラマーの解説。
　
## [Page 146](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=146&zoom=auto,-101,819)
> Identifier Names


変数名は\ UnicodeEscapeSequenceで表現されて、"$", or "_" または UTF16Encodingにマッチするものという感じなのか 


## [Page 146](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=146&zoom=auto,-101,511)
> Reserved Words

ReservedWordとはKeyword、FutureReservedWord、NullLiteral、BooleanLiteral

## [Page 147](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=147&zoom=auto,-101,522)
> FutureReservedWord

awaitとenumだけ(awaitはModuleの時だけ)
## [Page 152](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=152&zoom=auto,-14,614)
> It is a Syntax Error if the MV of HexDigits> 1114111.

`u{HexDigits}` 

`u{1114111}`までがセーフ

## [Page 153](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=153&zoom=auto,-14,376)
> String value (SV) 


## [Page 155](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=155&zoom=auto,-14,640)
> 11.8.6 Template LiteralLexical Components

Template Literalの${}は
TemplateHead、TemplateMiddle、TemplateTailからなる
## [Page 160](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=159&zoom=auto,-14,96)
> 12 ECMAScript Language: Expressions

ついにyieldきた

## ES６で増えた文法表示

- `[?in]`
- `[+parameter]`
- `[~parameter]`

これらはいずれもただの短縮記号なので、別の形に展開できる


## [Page 32](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=32&zoom=auto,-14,581)
> Prefixing  a parameter  name  with “?”on  a  right-hand  side  nonterminal  reference makes  that  parameter value dependent upon the occurrence of the parameter name on the reference to the current production’s left-hand side symbol.


`[?in]`の展開はES5でinを除くみたいなものが大量出てきたのを短縮するため

```
VariableDeclaration[In] :
	BindingIdentifier Initializer[?In]

=>

VariableDeclaration : 				
	BindingIdentifier Initializer
VariableDeclaration_In : 	
	BindingIdentifier Initializer_In
```


## [Page 32](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=32&zoom=auto,-14,500)
> If  a  right-hand  side  alternative  is  prefixed  with “[+parameter]”that  alternative  is  only  available  if  the  named parameter was used in referencing the production’s nonterminal symbol

+ と ~は対になる感じ


+ は+がついてる右側のsymbolを追加したものを加える。

```
StatementList[Return] :
[+Return] ReturnStatement
ExpressionStatement

=>

StatementList :
	ExpressionStatement
StatementList_Return :
	ReturnStatement
ExpressionStatement
```

~ は~がついてる右側のsymbolを除いたものを作る


```
StatementList[Return] :
[~Return] ReturnStatement
ExpressionStatement

=>

StatementList :
	ReturnStatement
	ExpressionStatement
StatementList_Return :
	ExpressionStatement
```

話を戻して

## [Page 160](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=159&zoom=auto,-13,31)
> 12.1　Identifiers

IdentifierRefernaceは次のように定義されている。

```
IdentifierReference[Yield] : 
	Identifier
	[~Yield] yield
```

これはつまりいかのように展開できる

```
IdentifierReference : 
	Identifier
	yield
IdentifierReference_Yeild : 
	Identifier
```


## [Page 164](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=164&zoom=auto,-13,757)
> PrimaryExpression:  this

`this`のステップは

1. Return `ResolveThisBinding()`

となるだけなので、thisの値は`ResolveThisBinding()`のアルゴリズムで決まっている。


## [Page 165](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=165&zoom=auto,-13,604)
> Elision

Arrayの, Elision 末尾のこと


## [Page 170](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=170&zoom=auto,-13,785)
> Return ObjectCreate(%ObjectPrototype%).

`{}`は`Object.create(Object.prototype)`と一緒
## [Page 173](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=173&zoom=auto,-13,685)
> 12.2.9.3 Runtime Semantics: GetTemplateObject( templateLiteral )

`realm.[[templateMap]]`からtemplate objectを取る所
## [Page 173](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=173&zoom=auto,-13,383)
> 12.Perform SetIntegrityLevel(rawObj, "frozen").

`raw`プロパティに入れるまでにオブジェクトをfreezeしてる
## [Page 174](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=173&zoom=auto,-13,200)
> Future editions of this specification may define additional non-enumerable properties of template objects.

何だろ?


## [Page 174](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=174&zoom=auto,-13,372)
>  TV

TV = Template Value
## [Page 176](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=176&zoom=auto,-13,745)
> 12.3Left-Hand-Side Expressions

new.targetってそれだけを定義してるMetaPropertyというのが構文にいるのか

## [Page 176](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=176&zoom=auto,-13,414)
> ArgumentList

`(ArgumentList[?Yield])`
となっている、ArgmentListには`... AssigmentExpression`というspreadがある

## [Page 182](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=182&zoom=auto,-13,728)
> SuperProperty:super.IdentifierName

実態は`MakeSuperPropertyReference(propertyKey, strict)`になる
## [Page 182](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=182&zoom=auto,-13,571)
> Runtime Semantics: GetSuperConstructor ( )

super(args)で使う

## [Page 184](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=184&zoom=auto,-13,652)
> 12.3.8 Meta Properties

`new.target`は`GetNewTarget()`の内部メソッドを呼ぶだけ

## [Page 185](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=185&zoom=auto,-13,458)
> Unary Operators

operator + Expressionな感じ
## [Page 186](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=186&zoom=auto,-14,476)
> 12.5.4.1 Static Semantics:  Early Errors1

```
delete ((foo))
```
がエラーになるように読めるんだけどどうなんだろ?

- https://twitter.com/azu_re/status/601946554765811713


## [Page 186](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=186&zoom=auto,-14,393)
> Runtime Semantics: Evaluation

delete演算子のアルゴリズム思ったより長い

## [Page 187](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=186&zoom=auto,-14,15)
> Let deleteStatusbebaseObj.[[Delete]](GetReferencedName(ref)).

strict modeだとconfigurable:false だとここででfalseが帰ってきてTypeErrorにが次で投げられるのかな?

## [Page 187](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=187&zoom=auto,-14,622)
> voidUnaryExpression

```
void a
```

aの値は使わないけど、副作用のためaを評価する

## [Page 187](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=187&zoom=auto,-14,424)
> 12.5.6

typeof演算子はまず、その変数が解決できるかをチェックしてできなかったら`"undefined"`を返す。

## [Page 188](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=187&zoom=auto,-14,74)
> Table 35—typeof Operator Results

後は、Table35にしたがった値を返す。
ES6では`"symbol"`が追加された。
またNullは継続して`"object"`を返す。
## [Page 188](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=188&zoom=auto,-14,757)
> Object (non-standard exotic and does not implement [[Call]])

Object (non-standard exotic and does not implement [[Call]])である場合はtypeofで返すものは実装依存だけど、”object”以外のどれかにしろってことらしい
## [Page 191](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=191&zoom=auto,-14,605)
> In C and C++, the remainder operator accepts only integral operands; in ECMAScript, it also accepts floating-point operands.

ECMAScriptはfloatだから %できるよ
## [Page 217](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=217&zoom=auto,-14,631)
> eval("1;{}")

```
eval("1;{}") ;// 1
```

1 と {} という順でStatementListが評価されて、StatementListの値は最後の評価された値なので、{}は評価値がなく、1が最後の評価値となる
## [Page 217](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=217&zoom=auto,-14,406)
> 13.2.14 Runtime Semantics: BlockDeclarationInstantiation( code, env )

_Block_ or _CodeBlock_ は新しいEnv Recordを作成して、そのスコープの変数や関数などをbindingしていく。

```
BlockDeclarationInstantiation (code ,env)
```

というのは上記のことを行う内部関数。


## [Page 218](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=218&zoom=auto,-14,808)
> 13.3.1 Let and Const Declarations

`let`や`const`はLexical Envのスコープで定義され、実行される。

## [Page 220](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=219&zoom=auto,-14,36)
> 13.3.2 Variable Statement

`ver`は実行コンテキストのVariableEnvriomentを対象にする。

## [Page 221](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=221&zoom=auto,-14,463)
> Destructuring Binding Patterns


## [Page 229](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=229&zoom=auto,-14,691)
> The ifStatement

ifの定義
## [Page 230](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=230&zoom=auto,-14,832)
> Static Semantics: ContainsUndefinedContinueTarget

```
if( Expression ) Statement else Statement
```

`ContainsUndefinedBreakTarget`というアルゴリズムでは、ifとかの中にStatementをチェックする仕組みなのかな?

else if という構文自体は定義されてなかったのでifとelseからelse ifができてる。

## [Page 229](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=228&zoom=auto,-14,7)
> Expression Statement

ExpressionStatementの定義

```
[lookahead {{,function,class,let [}]Expression[In, ?Yield]
```

function classキーワードではスタートできない。
## [Page 229](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=229&zoom=auto,-14,776)
> 13.5Expression Statement

Expression Statementはfunction,class,let以外から始まるExpression
また、U+007B(LEFT  CURLY  BRACKET)から始まることもできない。


## [Page 240](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=240&zoom=auto,-14,507)
> undefinedis  passed  for environmentto  indicate  that  a  PutValue  operation  should  be  used  to  assign  the initialization  value. This  is  the  case  for varstatements  and  the  formal  parameter  lists  of  some  non-strict  functions  (see 9.2.12). In those cases a lexical binding is hoisted and preinitialized prior to evaluation of its initializer.


## [Page 241](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=241&zoom=page-width,-14,366)
> ForIn/OfHeadEvaluation( TDZnames, expr, iterationKind, labelSet

TDZという名前が出てきてる



## [Page 243](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=243&zoom=page-width,-14,623)
> Static Semantics:  Early Errors

continueにもearly errorがある
## [Page 244](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=244&zoom=page-width,-14,307)
> A returnstatement  causes  a  function  to  cease  execution  and  return  a  value  to  the  caller.  If Expressionis omitted, the return value is undefined. Otherwise, the return value is the value of Expression

```
return fn() 
```

の時に値を返す仕組み



## [Page 247](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=247&zoom=page-width,-14,731)
> CaseBlock:{}
> 1.Return false


switch `{ }` この部分がfalseを返すのか


## [Page 250](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=250&zoom=page-width,-14,472)
> CaseClause

case Expression : StatementList

のこと
## [Page 253](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=253&zoom=page-width,-14,616)
> A Statementmay  be  prefixed  by  a  label.  Labelled  statements  are  only  used  in  conjunction  with  labelled breakand continuestatements.  ECMAScript  has  no gotostatement. 

breke labelとgoto
## [Page 257](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=256&zoom=page-width,-14,26)
> 13.14The throwStatement

throw と try

throwとは`Completion{[[type]]: throw, [[value]]: exprValue, [[target]]: empty}`というCompletionを返す処理のことをいう。
Completion 型 は仕様型の一種

## [Page 260](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=260&zoom=page-width,-14,398)
> TryStatement : try Block Catch

Blockの実行結果をみて、`B.[[type]]`がthrowとなっているなら、Catchの`C.[[vaue]]`にその値をいれてあげる。
## [Page 261](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=261&zoom=page-width,-14,628)
> The debuggerstatement

debuggerステートメントは実装が定義したdebbugging actionを実行して、その結果をCompletion valueに入れる。
## [Page 262](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=262&zoom=page-width,-14,579)
> Directive Prologues and the Use Strict Directive

ディレクティブプロローグ！
"use strict"か'use strict'に限定されてる。
## [Page 269](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=269&zoom=page-width,-14,832)
> 14.2Arrow Function Definitions

=>
## [Page 269](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=269&zoom=page-width,-14,526)
> Static Semantics:  Early Errors


```
var fn = (arg) => { var arg; }
```

はearly errorになる
## [Page 270](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=270&zoom=page-width,-14,675)
> Static Semantics:  Contains

this, superが含まれているかどうかというアルゴリズムが定義されている。
## [Page 273](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=273&zoom=page-width,-14,485)
> get PropertyName

method定義で `get name(){}`となって引数は必ずないけど、ここはearly errorではないんだ
## [Page 275](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=275&zoom=page-width,-14,658)
> 14.3.9 Runtime Semantics: PropertyDefinitionEvaluation

With parametersobjectandenumerable.

オブジェクトのプロパティ定義はenumerableを受け取る(trueだけど)
## [Page 276](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=276&zoom=page-width,-14,794)
> 14.4GeneratorFunction Definitions


## [Page 276](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=276&zoom=page-width,-14,747)
> yield [no LineTerminatorhere]AssignmentExpression[?In, Yield]

yeildのright-handはassignmneexpression

## [Page 276](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=276&zoom=page-width,-14,657)
> It is a Syntax Error ifHasDirectSuper of GeneratorMethod is true

Generator Methodがsuperを持ってるとearly error?

`HasDirectSuper`が要

## [Page 277](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=277&zoom=page-width,-14,667)
> Static Semantics:  ComputedPropertyContains

ComputedPropertyを含んでいるかの判定あるんだ
## [Page 277](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=277&zoom=page-width,-14,633)
> Static Semantics:  Contains

super含んじゃだめだし、常にfalseを返してる。

## [Page 277](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=277&zoom=page-width,-14,293)
> HasDirectSuper

Generator methodのparameter, bodyにsuperがあったらtrueを返す。
これの結果を使ってearly errorを見つける
## [Page 279](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=279&zoom=page-width,-14,363)
> Runtime Semantics: Evaluation

generator の実行ステップ
## [Page 280](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=280&zoom=page-width,-14,639)
> YieldExpression: yield

yeildというのは

ReturnGeneratorYield(CreateIterResultObject(value, false))

を返すということをしてる。

## [Page 280](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=280&zoom=page-width,-14,396)
> NOTE:  Exceptions from the inner iterator throwmethod are propagated.Normal completions from an inner throwmethod are processed similarly to an inner next


アルゴリズムのステップにNoteが入ってるのおかしくない?
これって仕様バグなのかな http://t.co/MftImQzB7e

doc版も同じ
ここではステップにNOTEを多用してるしわざとっぽい
## [Page 281](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=281&zoom=page-width,-14,564)
> 14.5ClassDefinitions

クラスの構文

## [Page 282](ecma-262_6th_edition_final_draft_-04-14-15.pdf#page=282&zoom=page-width,-14,576)
> ClassElement:staticMethodDefinitionIt is a Syntax Error if HasDirectSuper of MethodDefinitionistrue.It is a Syntax Error if PropNameof MethodDefinitionis"prototype"

staticなのに、method definitionみたいにsuperとかprototypeをearly errorにするのは良いね
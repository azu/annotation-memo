
## [Page 311](Ecma-262.pdf#page=311&zoom=page-width,-14,842)
> 16 ErrorHandling and Language Extensions

ScriptEvaluationJob 

> An  implementation  must report  as  an  early  error any occurrence  of  a  condition  that  is  listed  in  a  “Static Semantics: Early Errors”subclause of this specification

early errorは必ず取り扱いの必要がある。


## [Page 311](Ecma-262.pdf#page=311&zoom=page-width,-14,606)
> An  implementation  shall  not  treat  other  kinds  of  errors  as  early  errors  even  if  the  compiler  can  prove  that  a construct cannot execute without error under any circumstances. An implementation may issue an early warning in such a case, but it should not report the error until the relevant construct is actually executed.

逆に仕様でStatic Semantics:  Early Errorsとして決めてる物以外を勝手にEarly Errorにしてはいけない。警告はOKとする。

なので、警告じゃなくてearly errorを増やしてる[Strong Mode Proposal](https://docs.google.com/document/d/1Qk0qC4s_XNCLemj42FqfsRLp49nDQMZ1y7fwf5YjaI4/view "Strong Mode Proposal - Google ドキュメント")はES6の範疇ではなさそう。
(いくつかある例外の規定の範疇だったりするのかな? 実装は構文を拡張してるかもしれないという規定が)
## [Page 311](Ecma-262.pdf#page=311&zoom=page-width,-14,315)
> 16.1Forbidden Extensions

実装は拡張していい箇所もあるけど、逆に拡張してはいけない部分がある。


`arguments`、`caller`などstrict modeの部分、ECMA-402で決められてるi18N的なAPI、RegExpなど
## [Page 312](Ecma-262.pdf#page=312&zoom=page-width,-14,595)
> 17 ECMAScript Standard Built-in Objects


## [Page 314](Ecma-262.pdf#page=314&zoom=page-width,-14,768)
> The  value  of undefinedis undefined

`undefined`は `[[Writable]]: false`
## [Page 314](Ecma-262.pdf#page=314&zoom=page-width,-14,495)
> Runtime Semantics: PerformEval( x, evalRealm, strictCaller, direct)

evalの動作



## [Page 317](Ecma-262.pdf#page=316&zoom=page-width,-14,164)
> The isNaN function  is the  %isNaN%  intrinsic  object. 

`isNaN`はNaNかどうかを見て終わり
## [Page 318](Ecma-262.pdf#page=318&zoom=page-width,-14,502)
> 18.2.6.1 URI Syntax and Semantics

encodeURIComponentやdecodeURIComponentなどもECMAScript
## [Page 325](Ecma-262.pdf#page=325&zoom=page-width,-14,788)
> 19FundamentalObjects 

いよいよ、ObjectやArrayなどの話。
## [Page 325](Ecma-262.pdf#page=325&zoom=page-width,-14,675)
> Object ( [ value ] )

実態はObjectCreateで`Object.create`を使って実現できる
## [Page 326](Ecma-262.pdf#page=326&zoom=page-width,-14,792)
> Object.create ( O [, Properties] 

ただし、Object.createはOがnullだと例外を投げるという違いがある
## [Page 326](Ecma-262.pdf#page=326&zoom=page-width,-14,281)
> Object.freeze ( O )

`SetIntegrityLevel(O,"frozen")`というのが実態

Object.getOwnPropertyNames => GetOwnPropertyKeys 

getOwnPropertySymbols => GetOwnPropertyKeys 
## [Page 327](Ecma-262.pdf#page=327&zoom=page-width,-14,310)
> Object.is( value1, value2)

Object.isは`SameValue`のアルゴリズムをそのまま使う

## [Page 330](Ecma-262.pdf#page=329&zoom=page-width,-14,2)
> Object.prototype.toLocaleString ([ reserved1 [ , reserved2 ] ])

この予約された余分な引数はECMA-402で使うかもしれない
## [Page 330](Ecma-262.pdf#page=330&zoom=page-width,-14,593)
> 19.1.3.6 Object.prototype.toString ( )

@@toStringTagによる定義があると、既存の判定結果を上書きして"[object tag]"を返す

本質 intrinsic objectは%ObjProto_toString%である


## [Page 330](Ecma-262.pdf#page=330&zoom=page-width,-14,255)
> Object.prototype.valueOf 

valueOfはToObject(this value)したものを返す

----

FunctionはES5と同じなので

----
## [Page 337](Ecma-262.pdf#page=337&zoom=page-width,-14,545)
> 19.4Symbol Objects

%Symbol%  intrinsic  object
## [Page 338](Ecma-262.pdf#page=338&zoom=page-width,-14,746)
> GlobalSymbolRegistry

SymbolはGlobalSymbolRegistry Recordに保存される。

このRecordは

- [[key]]
- [[symbol]]

を持ってる。

well known symbolは基本的に `{ [[Writable]]: false, [[Enumerable]]: false, [[Configurable]]: false}`


## [Page 339](Ecma-262.pdf#page=339&zoom=page-width,-14,741)
> 19.4.2.10 Symbol.species

イチオシの@@species
## [Page 340](Ecma-262.pdf#page=340&zoom=page-width,-14,609)
> 19.4.3.4 Symbol.prototype[ @@toPrimitive ]( hint)

`hint`を設定できる
## [Page 341](Ecma-262.pdf#page=341&zoom=page-width,-14,730)
>  the function callError(...)is equivalent to the object creation expression new Error(...)with the same arguments


## [Page 341](Ecma-262.pdf#page=341&zoom=page-width,-14,730)
>  Errorconstructor to create and initialize subclass instanceswith a [[ErrorData]] internal slot

Errorはsubclassingが可能で[[ErrorData]]というinternal slotで満たせる
## [Page 341](Ecma-262.pdf#page=341&zoom=page-width,-14,523)
> The Errorprototype  object  is the  intrinsic  object%ErrorPrototype%. The  Error  prototype  object  is  an  ordinaryobject

ordinary objectは[[ErrorData]]を持ってない

## [Page 342](Ecma-262.pdf#page=342&zoom=page-width,-14,329)
> NativeErrorObject Structure

_NativeError_ について
## [Page 345](Ecma-262.pdf#page=345&zoom=page-width,-14,511)
> Number.isSafeInteger (number)

桁溢れてないかの判定が簡単にできる
## [Page 361](Ecma-262.pdf#page=361&zoom=page-width,-9,842)
> Date Number

MakeTimeとか結構細かいのも定義されてる。

## [Page 386](Ecma-262.pdf#page=386&zoom=page-width,-9,811)
> Replacement Text Symbol SubstitutionsCode

"string".replace(/(ing)/, `-$\``);

ES6でもコメントと除算の判定みたいなパターンありそう。
$`とか使ってるの見たことないけど

Tempale Stringと$`で被る
## [Page 392](Ecma-262.pdf#page=392&zoom=page-width,-9,515)
> 21.1.5 tring Iterator Objects 

Stringはiterableであるという話

## [Page 414](Ecma-262.pdf#page=414&zoom=page-width,-9,424)
> RegExp.prototype[ @@match ] (string 

Symbol match
## [Page 420](Ecma-262.pdf#page=420&zoom=page-width,-9,577)
> 22Indexed Collections

Array 
## [Page 421](Ecma-262.pdf#page=421&zoom=page-width,-9,327)
> 22.1.2.1 Array.from( items [ , mapfn [ , thisArg ] ])

Array.fromはmapもできる

## [Page 423](Ecma-262.pdf#page=423&zoom=page-width,-9,751)
> 22.1.2.3 Array.of( ...items)

Array.ofはarray likeをarrayにして返してくれる。
ひらすたらwhileて回してarrayを返す

## [Page 444](Ecma-262.pdf#page=444&zoom=page-width,-9,432)
> 22.1.3.31  Array.prototype[ @@unscopables ]

1 Perform CreateDataProperty(blackList, "copyWithin", true)

まさかのベタ書き
## [Page 446](Ecma-262.pdf#page=446&zoom=page-width,-9,458)
> 22.2 TypedArrayObjects 

TypedArray
## [Page 469](Ecma-262.pdf#page=468&zoom=page-width,-9,163)
> 23.1.5 Map Iterator Objects


## [Page 469](Ecma-262.pdf#page=469&zoom=page-width,-9,524)
> itemKind is "key+value"

itemKindでkey+valueがある。
この種類の場合はmap.iterator.next()で`CreateArrayFromList(«e.[[key]],e.[[value]]»)`を返す。

つまり、言語レベルで `[key, value]` というものが存在してる。

## [Page 470](Ecma-262.pdf#page=469&zoom=page-width,-9,123)
> Table 50—Internal Slots of Map Iterator Instances

`[[MapIterationKind]]` に "key", "value", "key+value" という3パターンがある。
## [Page 475](Ecma-262.pdf#page=475&zoom=page-width,-9,821)
> 23.3 WeakMap Objects

実装者はキーを監視する機能は提供しなくて良い。
observableではない。
## [Page 489](Ecma-262.pdf#page=489&zoom=page-width,-10,289)
> 24.3The JSON Object

%JSON% intrinsic object これはECMA404で定義されてる
## [Page 496](Ecma-262.pdf#page=495&zoom=page-width,-10,164)
> 25 Control Abstraction Objects

IterableとかIterator、IteratorResultとかのInterfaceを定義してる。(なんでいきなりinterfaceなんだろ?)

あるオブジェクトは複数のinterfaceを実装してても良い

## [Page 496](Ecma-262.pdf#page=496&zoom=page-width,-10,804)
> An  interface is  a  set  of  property  keys  whose  associated values  match  a  specific  specification. 

interfaceとはpropertyの集合を定義してもの

## [Page 496](Ecma-262.pdf#page=496&zoom=page-width,-10,629)
> Iterable Interface Required Properties

`Iterable` interfaceは`@@iterator`を持ってるオブジェクト
(`@@iterator`はiteratorオブジェクトを返す関数)


## [Page 496](Ecma-262.pdf#page=496&zoom=page-width,-10,629)
> Iterator Interface Required Properties

`Iterator` interfaceは`next`、`return`、`throw`を持つオブジェクト


## [Page 497](Ecma-262.pdf#page=497&zoom=page-width,-10,704)
> IteratorResult Interface Properties

`IteratorResult` interfaceは`done`と`value`を持つオブジェクト
## [Page 498](Ecma-262.pdf#page=498&zoom=page-width,-9,214)
> The GeneratorFunctionconstructor is  the  %GeneratorFunction% intrinsic.


## [Page 499](Ecma-262.pdf#page=498&zoom=page-width,-9,44)
> GeneratorFunction is designed to be subclassable

Generator はサブクラス可能　
## [Page 497](Ecma-262.pdf#page=497&zoom=page-width,-9,220)
> Object.getPrototypeOf(Object.getPrototypeOf([][Symbol.iterator]()))

`%IteratorPrototype%`を取る方法

## [Page 500](Ecma-262.pdf#page=500&zoom=page-width,-9,772)
> 25.2.4 GeneratorFunction Instances


## [Page 500](Ecma-262.pdf#page=500&zoom=page-width,-9,772)
> The value of the [[FunctionKind]] internal slot for all such instances is "generator"

generatorのインスタンス=generator objectは"generator"という種類になる。


## [Page 500](Ecma-262.pdf#page=500&zoom=page-width,-9,346)
> A  Generator  object  is  an  instance  of  a  generatorfunction  and  conforms  to  both  the Iterator and Iterable interfaces

GeneratorオブジェクトはIteratorとIterable interfaceを持つ。
Generator objectはgenerator functionのインスタンス



## [Page 501](Ecma-262.pdf#page=500&zoom=page-width,-9,46)
> The  Generator  prototypeisan  ordinary  object.  It  is  not  a  Generator  instance  and  does  not  havea [[GeneratorState]] internal slot.

ordinary objectはinternal slotを持ってない

## [Page 501](Ecma-262.pdf#page=501&zoom=page-width,-9,740)
> Let CbeCompletion{[[type]]: return, [[value]]: value, [[target]]: empty}

`Generator.prototype.return ( value )`はCompletion型を渡してる
## [Page 501](Ecma-262.pdf#page=501&zoom=page-width,-9,593)
> Let CbeCompletion{[[type]]: throw, [[value]]: exception, [[target]]: empty}

Generator.prototype.throw ( exception )は`type:throw`
## [Page 501](Ecma-262.pdf#page=501&zoom=page-width,-9,400)
> 25.3.2 Properties of Generator Instances

Generator Instanceは以下のinternal slotを持つ

- [[GeneratorState]]
	- yieldによって"susupededYield"や"executing"などの状態を遷移して"completed"となる
- [[GeneratorContext]]

Generatorはexecution context stackからgeneratorContextをremoveしたり(complete)、pushしたりする(resume)
## [Page 503](Ecma-262.pdf#page=503&zoom=page-width,-9,463)
> GeneratorYield ( iterNextObj )

yeildはGeneratorYield ( iterNextObj )を実行することで、[[GeneratorState]]を"suspendedYield"にしてくれる

> Remove genContextfrom the execution context stack and restorethe execution context that is at the top of the execution context stack as the runningexecution context

supendと同時にexecution context stackからgenCtxを取り除いている。=つまり処理されなくなってる。
　
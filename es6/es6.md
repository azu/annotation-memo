
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
　
## [Page 503](Ecma-262.pdf#page=503&zoom=page-width,-14,401)
> 25.4Promise Objects

Promise

pending -> fulfilled, rejefted

pendingではないことを _settled_ と呼ぶ

promiseがsettledとなったことを_resolved_とよび、そうでないことを_unresolved_と呼ぶ。

unresolved == pending
つまり、rejectでもあってもresolved。


## [Page 504](Ecma-262.pdf#page=504&zoom=page-width,-14,715)
> PromiseCapabilityRecords

Promiseの情報はPromiseCapablity Record Fieldに入る。
## [Page 504](Ecma-262.pdf#page=504&zoom=page-width,-14,436)
> PromiseReaction Records

thenした時にどうするかの情報を保持するRecord


## [Page 505](Ecma-262.pdf#page=505&zoom=page-width,-14,764)
> CreateResolvingFunctions( promise )

CreateResolvingFunctionsが25.4.1.3.1Promise RejectFunctionsと25.4.1.3.2Promise Resolve Functionsを使って、
Promiseに対してresolveとrejectの関数を追加する。

resolveとrejectは[[AlreadyResolved]]を見て、挙動が違ったりする。


## [Page 506](Ecma-262.pdf#page=505&zoom=page-width,-14,178)
> FulfillPromise ( promise, value)

resultとstateを埋めて、PromiseFulfillReactionsとPromiseRejectReactionsをundefinedにする。


## [Page 506](Ecma-262.pdf#page=506&zoom=page-width,-14,797)
> NewPromiseCapability( C )

CはConstructorのC
IsConstructor(C)でチェックする。

- 新しいPromiseCapabilityRecordsを作る
- excutorをGetCapabilitiesExecutorでで作る
- exctutor.[[Capability]] = promiseCapability 
- `Construct(C, «executor»)`を行う。

> 7.3.13 Construct (F, [argumentsList], [newTarget])

を見ると `C.[[Constructor]](executor)` を行うということになる。

- `promise = C.[[Constructor]](executor)`
	- この時にexturor.[[Capability]].[[Resolve]]とexturor.[[Capability]].[[Reject]]がcallableな値が代入されることを前提としてる
- promiseCapability.[[Promise]] = promise
- return promiseCapability 

という感じでNewPromiseCapability( C )により新しいpromsieCapabilityが帰ってくる
## [Page 506](Ecma-262.pdf#page=506&zoom=page-width,-14,410)
> 25.4.1.5.1GetCapabilitiesExecutorFunctions

ここがややこしい、
逆にこっちはpromise.Capability.[[Resolve]]がundefinedであることをチェックする。


## [Page 506](Ecma-262.pdf#page=506&zoom=page-width,-14,410)
> 25.4.1.6 IsPromise ( x )

[[PromiseState]]を持ってるかどうかで判定する。

## [Page 507](Ecma-262.pdf#page=507&zoom=page-width,-14,743)
> 25.4.1.8 TriggerPromiseReactions ( reactions, argument )

reactionは追加した順にPromiseJobs queueに追加される。

- [What is correct execution sequence when attach multiple handlers to the same promise. · Issue #34 · getify/native-promise-only](https://github.com/getify/native-promise-only/issues/34 "What is correct execution sequence when attach multiple handlers to the same promise. · Issue #34 · getify/native-promise-only")
- http://trac.webkit.org/browser/trunk/Source/JavaScriptCore/builtins/Operations.Promise.js?rev=186298#L88
- [promises-unwrapping/testable-implementation.js at 2a942729249c2490507a1ae6c9a24f8fa11a98e4 · domenic/promises-unwrapping](https://github.com/domenic/promises-unwrapping/blob/2a942729249c2490507a1ae6c9a24f8fa11a98e4/reference-implementation/lib/testable-implementation.js#L212-L218 "promises-unwrapping/testable-implementation.js at 2a942729249c2490507a1ae6c9a24f8fa11a98e4 · domenic/promises-unwrapping")



がPromise/A+では書いてなかった部分。

## [Page 507](Ecma-262.pdf#page=507&zoom=page-width,-14,589)
> 25.4.2 Promise Jobs


## [Page 507](Ecma-262.pdf#page=507&zoom=page-width,-14,504)
> PromiseReactionJob ( reaction, argument 


## [Page 507](Ecma-262.pdf#page=507&zoom=page-width,-14,504)
> PromiseResolveThenableJob ( promiseToResolve, thenable, then)

2種類のjobをもってる
## [Page 508](Ecma-262.pdf#page=508&zoom=page-width,-14,847)
> 25.4.3 The Promise Constructor

new Promise((resolve, reject) => {})



## [Page 509](Ecma-262.pdf#page=509&zoom=page-width,-14,773)
> 25.4.4.1.1Runtime Semantics: PerformPromiseAll( iteratorRecord, constructor, resultCapability)

`Promise.all`の実態

iterableを引数ととして受けるので、それをrepeatして処理していく。

## [Page 510](Ecma-262.pdf#page=510&zoom=page-width,-14,256)
> 25.4.4.3.1Runtime Semantics:  PerformPromiseRace ( iteratorRecord, promiseCapability, C )


Promise.raceは意外とシンプル。
新しいpromiseCapabilityを作って、

promises.forEach(promise => promise.then(promise.Capability.resolve, promise.Capability.reject)

するだけという。

基本投げっぱなし。

## [Page 511](Ecma-262.pdf#page=511&zoom=page-width,-14,617)
> Promise.reject ( r )


## [Page 511](Ecma-262.pdf#page=511&zoom=page-width,-14,571)
> Promise.resolve ( x )

ドラフトと違ってリリース版で入ったもの

- [Fixing `Promise.resolve()`](https://esdiscuss.org/topic/fixing-promise-resolve "Fixing `Promise.resolve()`")

ドラフトでは@@speciesを参照していたので、

```
p = Promise.resolve(weakPromise);
p = Promise.resolve(timeoutPromise);
```

とやってもそれぞれWeakPromiseやtimoutPromiseのPromiseが帰ってきてた。

それが欲しければ、以下のように書くほうがよいので、それを治すために@@speciesじゃなくて常にthis Constructorを参照するように変わった

```
pp = WeakPromise.resolve(p);
pp = TimeoutPromise.resolve(p);
```


## [Page 513](Ecma-262.pdf#page=513&zoom=page-width,-14,788)
> Properties of Promise Instances

promiseのインスタンスは[[PromiseFulfillReactions]]と[[PromiseRejectReactions]]のfieldを持っていて、stateが変わった時に呼ばれるreactionのリスト

## [Page 513](Ecma-262.pdf#page=513&zoom=page-width,-9,606)
> 26Reflection

Reflection API

- [harmony-reflect/api.md at master · tvcutsem/harmony-reflect](https://github.com/tvcutsem/harmony-reflect/blob/master/doc/api.md "harmony-reflect/api.md at master · tvcutsem/harmony-reflect")
- [Home · tvcutsem/harmony-reflect Wiki](https://github.com/tvcutsem/harmony-reflect/wiki "Home · tvcutsem/harmony-reflect Wiki")

## [Page 514](Ecma-262.pdf#page=513&zoom=page-width,-9,149)
> Reflect.defineProperty ( target,propertyKey, attributes )

Object.definePropertyと同じに見える


## [Page 514](Ecma-262.pdf#page=514&zoom=page-width,-9,842)
> Reflect.deleteProperty ( target, propertyKey )

delete演算子
## [Page 514](Ecma-262.pdf#page=514&zoom=page-width,-9,625)
> Reflect.enumerate( target )

```js

var iterator = Reflect.enumerate(target);
var nxt = iterator.next();
```

iteratorを取れる
## [Page 514](Ecma-262.pdf#page=514&zoom=page-width,-9,604)
> Reflect.get ( target,propertyKey [ , receiver ])

target[propertyKey] のgetをする。
receiverが`this`?



## [Page 514](Ecma-262.pdf#page=514&zoom=page-width,-9,323)
> Reflect.getPrototypeOf ( target )

`__proto__`の代わりにこっち。
`__proto__`は互換性のために残ってる

## [Page 515](Ecma-262.pdf#page=514&zoom=page-width,-9,99)
> Reflect.has ( target, propertyKey )

```
propertyKey in target
```

内部的には`[[HasProperty]](key)`


## [Page 515](Ecma-262.pdf#page=515&zoom=page-width,-9,808)
> Reflect.ownKeys( target )

`target.[[OwnPropertyKeys]]()`

基本的にReflect  APIは `target.[[internal prop]]` を叩くだけ


## [Page 515](Ecma-262.pdf#page=515&zoom=page-width,-9,632)
> Reflect.set ( target,propertyKey, V [ , receiver ] )

`target[name] = value;`

この辺は [Page 23](Ecma-262.pdf#page=23)あたりのTable 5 — Essential Internal Methodsに載ってる内部メソッド。

`[[]]` は internalのマーク

> Internal methods and internal slots are identified within this specification using names enclosed in double square brackets [[ ]]


## [Page 515](Ecma-262.pdf#page=515&zoom=page-width,-9,358)
> Reflect.setPrototypeOf( target, proto )

`target.__proto__ = proto;`
## [Page 515](Ecma-262.pdf#page=515&zoom=page-width,-9,290)
> 26.2Proxy Objects

Proxyオブジェクト. %Proxy%

## [Page 516](Ecma-262.pdf#page=516&zoom=page-width,-9,809)
> Proxy.revocable( target, handler)

revocable  Proxy  object を作るメソッド

## [Page 516](Ecma-262.pdf#page=516&zoom=page-width,-9,495)
> Each Proxy revocation function has a [[RevocableProxy]] internal slot.

Proxyはそれぞれ`[[RevocableProxy]]` internal slotを持ってる。

```
p = [[RevocableProxy]]
p.[[ProxyHandler]]
p.[[ProxyTarget]]
```

という形でProxyの情報を持っている。


## [Page 516](Ecma-262.pdf#page=516&zoom=page-width,-9,392)
> 26.3Module Namespace Objects


## [Page 516](Ecma-262.pdf#page=516&zoom=page-width,-9,392)
> module  namespace exotic  object

exotic objectである、プロパティベースでモジュールのexportされているバインディングに対してアクセス出来る。

コンストラクタではない。

これらのname space objectは `import`, `import * as`でとってこれる。
これで取ってきたオブジェクトについて


## [Page 516](Ecma-262.pdf#page=516&zoom=page-width,-9,392)
> @@toStringTag

m.toString()は`"Module"`である。
## [Page 543](Ecma-262.pdf#page=542&zoom=page-width,-9,38)
> B.1.3HTML-like Comments

Annex Bで`<!-- -->`がコメントとして認識される仕様が入ってる。
## [Page 548](Ecma-262.pdf#page=548&zoom=page-width,-9,533)
> Object.prototype.__proto__

get/setPrototypeOf
## [Page 549](Ecma-262.pdf#page=548&zoom=page-width,-9,176)
> String.prototype.substr (start, length)

substrも一応残ってる。

## [Page 549](Ecma-262.pdf#page=549&zoom=page-width,-9,775)
> String.prototype.anchor(name)


## [Page 549](Ecma-262.pdf#page=549&zoom=page-width,-9,775)
> Runtime Semantics: CreateHTML( string, tag, attribute, value)

String#big とかは`CreateHTML`を使って作るようになってる。
## [Page 551](Ecma-262.pdf#page=551&zoom=page-width,-9,680)
> Date.prototype.getYear ( )

`date.getYear()`もdeprecated
## [Page 551](Ecma-262.pdf#page=551&zoom=page-width,-9,196)
> RegExp.prototype.compile (pattern, flags )

今はなきcompile
## [Page 552](Ecma-262.pdf#page=552&zoom=page-width,-9,373)
> Labelled Function Declarations

```
labeledItem : function a(){
}
```

こんなのあったの?
strict modeだとSymtax Errorになる。
## [Page 554](Ecma-262.pdf#page=554&zoom=page-width,-9,591)
> FunctionDeclarations in IfStatement Statement Clauses

if内のfunction定義。
一応互換性のためにあるけど


## [Page 554](Ecma-262.pdf#page=554&zoom=page-width,-9,413)
> VariableStatements in Catch blocks

catch内でのvar宣言
## [Page 557](Ecma-262.pdf#page=557&zoom=page-width,-10,799)
> implements, interface, let, package, private, protected, public, static,andyieldare reserved wordswithin strict mode code

strict modeは予約語が増える。


## [Page 559](Ecma-262.pdf#page=558&zoom=page-width,-10,99)
> AnnexD  Corrections and Clarifications in ECMAScript 2015 with Possible Compatibility Impact


## [Page 559](Ecma-262.pdf#page=559&zoom=page-width,-10,697)
> Previous  editions  permitted  the  TimeClip  abstract  operation  to  return  either  +0  or 0as  the representation  of  a  0  time  value

+0 -0どちらかをかえしてたけど、+0に固定された。


## [Page 561](Ecma-262.pdf#page=561&zoom=page-width,-9,586)
> In  ECMAScript  2015,  Automatic  Semicolon  Insertion  adds  a  semicolon  at  the  end  of  a  do-while statement  if  the  semicolon  is  missing.

`do{}while()` で`;`が入ると。実装は
## [Page 562](Ecma-262.pdf#page=562&zoom=page-width,-9,803)
> In ECMAScript 2015, the function objects that are created as the values of the [[Get]] or [[Set]] attribute of accessor  properties  in  an ObjectLiteralare  not  constructor functions  and  they  do  not  have  a prototypeown property. In the previous edition, they were constructors and had a prototypeproperty

method()はnew出来ない話

method definitionの方はfunction expressionのobject.propとは異なる。

- [ECMAScript 2015 Annex E 14.3.9](https://gist.github.com/azu/37e1877da4d991f768f1 "ECMAScript 2015 Annex E 14.3.9")
## [Page 562](Ecma-262.pdf#page=562&zoom=page-width,-9,663)
> In  ECMAScript  2015, if the  argument  to Object.freezeis  not  an  object  it is  treated  as  if it  was  a non-extensible  ordinary  object  with  no  own  properties.  

この辺以前のバージョンでは例外を投げていた部分

- [Break the Web: Object staticメソッドがES6で仕様変更になった件について](https://gist.github.com/teppeis/c50743a60832560aa1df "Break the Web: Object staticメソッドがES6で仕様変更になった件について")
## [Page 563](Ecma-262.pdf#page=563&zoom=page-width,-9,443)
> In  ECMAScript  2015,  the String.prototype.trimmethod  is  defined  to  recognize  white  space code  points  that may  exists  outside  of the  Unicode  BMP.

code pointの厳密化に伴ってtrimがちょっと違うのか
## [Page 563](Ecma-262.pdf#page=563&zoom=page-width,-9,337)
> In ECMAScript 2015, source, global, ignoreCase, and multilineare accessor properties defined on the RegExp prototype object. In previous editions they were data properties defined on RegExp instances

インスタンスにあったsourceなどのプロパティがRegExp.prototype.sourceに移動した。
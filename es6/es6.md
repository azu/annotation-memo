
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


---
title: Objects.md
repository: underscore
branch: 'master'
layout: default
---

+ 元文書 [underscore/index.html at a5ea59ad16d478a3643f6440ea94ac19ae86f0d4 · documentcloud/underscore · GitHub](https://github.com/documentcloud/underscore/blob/a5ea59ad16d478a3643f6440ea94ac19ae86f0d4/index.html "underscore/index.html at a5ea59ad16d478a3643f6440ea94ac19ae86f0d4 · documentcloud/underscore · GitHub")

## オブジェクト関数 [原文](http://underscorejs.org/#objects)

### keys `_.keys(object)` [原文](http://underscorejs.org/#keys)

Retrieve all the names of the **object**'s properties.

**object** のプロパティ名を全て探索する。

<pre class="javascript"><code>_.keys({one : 1, two : 2, three : 3});
=&gt; [&quot;one&quot;, &quot;two&quot;, &quot;three&quot;]
</code></pre>

### values `_.values(object)` [原文](http://underscorejs.org/#values)

Return all of the values of the **object**'s properties.

**object** のプロパティの値を全て返す。

<pre class="javascript"><code>_.values({one : 1, two : 2, three : 3});
=&gt; [1, 2, 3]
</code></pre>

### pairs `_.pairs(object)` [原文](http://underscorejs.org/#pairs)

Convert an object into a list of `[key, value]` pairs.

objectを `[key, value]` のペアになっているリストに変換する。

<pre class="javascript"><code>_.pairs({one: 1, two: 2, three: 3});
=&gt; [[&quot;one&quot;, 1], [&quot;two&quot;, 2], [&quot;three&quot;, 3]]
</code></pre>

### invert `_.invert(object)` [原文](http://underscorejs.org/#invert)

Returns a copy of the **object** where the keys have become the values and the values the keys.
For this to work, all of your object's values should be unique and string serializable.

キーを値に、値をキーにした **object** のコピーを返す。
この関数が機能するためには、オブジェクトのすべての値がユニークでシリアライズ可能な文字列である必要があります。

<pre class="javascript"><code>_.invert({Moe: &quot;Moses&quot;, Larry: &quot;Louis&quot;, Curly: &quot;Jerome&quot;});
=&gt; {Moses: &quot;Moe&quot;, Louis: &quot;Larry&quot;, Jerome: &quot;Curly&quot;};
</code></pre>

### functions `_.functions(object)` _Alias: methods_ [原文](http://underscorejs.org/#object-functions)

Returns a sorted list of the names of every method in an object — that is to say, the
name of every function property of the object.

オブジェクトの全てのメソッド名のソートされたリストを返します。
すなわち、オブジェクトの全ての関数のプロパティ名のことです。

<pre class="javascript"><code>_.functions(_);
=&gt; [&quot;all&quot;, &quot;any&quot;, &quot;bind&quot;, &quot;bindAll&quot;, &quot;clone&quot;, &quot;compact&quot;, &quot;compose&quot; ...
</code></pre>

### extend `_.extend(destination, *sources)` [原文](http://underscorejs.org/#extend)

Copy all of the properties in the **source** objects over to the **destination** object, and
return the **destination** object. It's in-order, so the last source will override properties
of the same name in previous arguments.

**source** オブジェクトの全プロパティを **destination** オブジェクトにコピーして、 **destination** オブジェクトを返します。
整理すると、二つめの引数の source は一つめの引数にある同じ名前のプロパティを上書きします。

<pre class="javascript"><code>_.extend({name : 'moe'}, {age : 50});
=&gt; {name : 'moe', age : 50}
</code></pre>

### pick `_.pick(object, *keys)` [原文](http://underscorejs.org/#pick)

Return a copy of the **object**, filtered to only have values for the whitelisted **keys** (or array of valid keys).

ホワイトリストとして指定したキー(もしくは有効にするキーの配列)の値だけ持つようにフィルタリングした **object** のコピーを返します。

<pre class="javascript"><code>_.pick({name : 'moe', age: 50, userid : 'moe1'}, 'name', 'age');
=&gt; {name : 'moe', age : 50}
</code></pre>

### omit `_.omit(object, *keys)` [原文](http://underscorejs.org/#omit)

Return a copy of the **object**, filtered to omit the blacklisted **keys** (or array of keys).

ブラックリストとして指定したキー(もしくはキーの配列)を省略するようにフィルタリングした **object** のコピーを返します。

<pre class="javascript"><code>_.omit({name : 'moe', age : 50, userid : 'moe1'}, 'userid');
=&gt; {name : 'moe', age : 50}
</code></pre>

### defaults `_.defaults(object, *defaults)` [原文](http://underscorejs.org/#defaults)

Fill in null and undefined properties in **object** with values from the **defaults** objects,
and return the **object**. As soon as the property is filled, further defaults will have no effect.

**defaults** オブジェクトにある値を **object** のnullとundefinedのプロパティに挿入し、その **object** を返します。
プロパティが挿入される際は、 defaults は影響を受けません。

<pre class="javascript"><code>var iceCream = {flavor : &quot;chocolate&quot;};
_.defaults(iceCream, {flavor : &quot;vanilla&quot;, sprinkles : &quot;lots&quot;});
=&gt; {flavor : &quot;chocolate&quot;, sprinkles : &quot;lots&quot;}
</code></pre>

### clone `_.clone(object)` [原文](http://underscorejs.org/#clone)

Create a shallow-copied clone of the **object**.
Any nested objects or arrays will be copied by reference, not duplicated.

**object** の浅いコピーをしたクローンを作成します。
ネストされたオブジェクトや配列は参照によるコピーで、複製されたものではありません。

<pre class="javascript"><code>_.clone({name : 'moe'});
=&gt; {name : 'moe'};
</code></pre>

### tap `_.tap(object, interceptor)` [原文](http://underscorejs.org/#tap)

Invokes **interceptor** with the **object**, and then returns **object**.
The primary purpose of this method is to "tap into" a method chain, in order to perform operations on intermediate results within the chain.

**object** に **割り込み処理** を差し込んでから **object** を返します。
このメソッドの主な目的は、チェーン内の途中の結果を操作するためにメソッドチェーンを利用することです。

<pre class="javascript"><code>_.chain([1,2,3,200])
  .filter(function(num) { return num % 2 == 0; })
  .tap(alert)
  .map(function(num) { return num * num })
  .value();
=&gt; // [2, 200] (alerted)
=&gt; [4, 40000]
</code></pre>

### has `_.has(object, key)` [原文](http://underscorejs.org/#has)

Does the object contain the given key?
Identical to `object.hasOwnProperty(key)`, but uses a safe reference to the `hasOwnProperty` function, in case it's been [overridden accidentally](http://www.devthought.com/2012/01/18/an-object-is-not-a-hash/).

objectに渡されたキーが含まれているかチェックします。
`object.hasOwnProperty(key)` と同じですが、[誤って上書きされる](http://www.devthought.com/2012/01/18/an-object-is-not-a-hash/) 場合がある `hasOwnProperty` 関数への参照を安全に行えます。

<pre class="javascript"><code>_.has({a: 1, b: 2, c: 3}, &quot;b&quot;);
=&gt; true
</code></pre>

### isEqual `_.isEqual(object, other)` [原文](http://underscorejs.org/#isEqual)

Performs an optimized deep comparison between the two objects, to determine if they
should be considered equal.

等しいものとするべきかどうか判断するために、2つのオブジェクト間で最適化された深い比較を行います。

<pre class="javascript"><code>var moe   = {name : 'moe', luckyNumbers : [13, 27, 34]};
var clone = {name : 'moe', luckyNumbers : [13, 27, 34]};
moe == clone;
=&gt; false
_.isEqual(moe, clone);
=&gt; true
</code></pre>

### isEmpty `_.isEmpty(object)` [原文](http://underscorejs.org/#isEmpty)

Returns _true_ if **object** contains no values.

**object** に値が含まれていない場合、 _true_ を返します。

<pre class="javascript"><code>_.isEmpty([1, 2, 3]);
=&gt; false
_.isEmpty({});
=&gt; true
</code></pre>

### isElement `_.isElement(object)` [原文](http://underscorejs.org/#isElement)

Returns _true_ if **object** is a DOM element.

**object** がDOM要素の場合、 _true_ を返します。

<pre class="javascript"><code>_.isElement(jQuery('body')[0]);
=&gt; true
</code></pre>

### isArray `_.isArray(object)` [原文](http://underscorejs.org/#isArray)

Returns _true_ if **object** is an Array.

**object** が配列の場合、 _true_ を返します。

<pre class="javascript"><code>(function(){ return _.isArray(arguments); })();
=&gt; false
_.isArray([1,2,3]);
=&gt; true
</code></pre>

### isObject `_.isObject(value)` [原文](http://underscorejs.org/#isObject)

Returns _true_ if **value** is an Object.
Note that JavaScript arrays and functions are objects, while (normal) strings and numbers are not.

**value** がオブジェクトの場合、 _true_ を返します。
注：JavaScriptの配列と関数はオブジェクトで、(普通の)文字列や整数はオブジェクトではありません。

<pre class="javascript"><code>_.isObject({});
=&gt; true
_.isObject(1);
=&gt; false
</code></pre>

### isArguments `_.isArguments(object)` [原文](http://underscorejs.org/#isArguments)

Returns _true_ if **object** is an Arguments object.

**object** がArgumentsオブジェクトの場合、 _true_ を返します。

<pre class="javascript"><code>(function(){ return _.isArguments(arguments); })(1, 2, 3);
=&gt; true
_.isArguments([1,2,3]);
=&gt; false
</code></pre>

### isFunction `_.isFunction(object)` [原文](http://underscorejs.org/#isFunction)

Returns _true_ if **object** is a Function.

**object** が関数の場合、 _true_ を返します。

<pre class="javascript"><code>_.isFunction(alert);
=&gt; true
</code></pre>

### isString `_.isString(object)` [原文](http://underscorejs.org/#isString)

Returns _true_ if **object** is a String.

**object** が文字列の場合、 _true_ を返します。

<pre class="javascript"><code>_.isString(&quot;moe&quot;);
=&gt; true
</code></pre>

### isNumber `_.isNumber(object)` [原文](http://underscorejs.org/#isNumber)

Returns _true_ if **object** is a Number (including `NaN`).

**object** が整数(`NaN` を含む)の場合、 _true_ を返します。

<pre class="javascript"><code>_.isNumber(8.4 * 5);
=&gt; true
</code></pre>

### isFinite `_.isFinite(object)` [原文](http://underscorejs.org/#isFinite)

Returns _true_ if **object** is a finite Number.

**object** が有限数の場合、 _true_ を返します。

<pre class="javascript"><code>_.isFinite(-101);
=&gt; true

_.isFinite(-Infinity);
=&gt; false
</code></pre>

### isBoolean `_.isBoolean(object)` [原文](http://underscorejs.org/#isBoolean)

Returns _true_ if **object** is either _true_ or _false_.

**object** が _true_ か _false_ のどちらかの場合、 _true_ を返します。

<pre class="javascript"><code>_.isBoolean(null);
=&gt; false
</code></pre>

### isDate `_.isDate(object)` [原文](http://underscorejs.org/#isDate)

Returns _true_ if **object** is a Date.

**object** が日付オブジェクトの場合、 _true_ を返します。

<pre class="javascript"><code>_.isDate(new Date());
=&gt; true
</code></pre>

### isRegExp `_.isRegExp(object)` [原文](http://underscorejs.org/#isRegExp)

Returns _true_ if **object** is a RegExp.

**object** が正規表現オブジェクトの場合、 _true_ を返します。

<pre class="javascript"><code>_.isRegExp(/moe/);
=&gt; true
</code></pre>

### isNaN `_.isNaN(object)` [原文](http://underscorejs.org/#isNaN)

Returns _true_ if **object** is _NaN_.
Note: this is not the same as the native **isNaN** function, which will also return true if 
the variable is _undefined_.

**object** が _NaN_ の場合、 _true_ を返します。
注：この関数は、変数が _undefined_ の時に true が返される組み込みの **isNaN** 関数と同じではありません。

<pre class="javascript"><code>_.isNaN(NaN);
=&gt; true
isNaN(undefined);
=&gt; true
_.isNaN(undefined);
=&gt; false
</code></pre>

### isNull `_.isNull(object)` [原文](http://underscorejs.org/#isNull)

Returns _true_ if the **value** of object is _null_.

objectの **値** が _null_ の場合、 _true_ を返します。

<pre class="javascript"><code>_.isNull(null);
=&gt; true
_.isNull(undefined);
=&gt; false
</code></pre>

### isUndefined `_.isUndefined(value)` [原文](http://underscorejs.org/#isUndefined)

Returns _true_ if **value** is _undefined_.

**value** が _undefined_ の場合、 _true_ を返します。

<pre class="javascript"><code>_.isUndefined(window.missingVariable);
=&gt; true
</code></pre>

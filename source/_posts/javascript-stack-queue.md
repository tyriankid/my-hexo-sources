title: 随便说说JS数组中的栈与队列
date: 2012-08-24 16:31:29
tags: [栈, 队列, javascript]
category: javascript
---

###1. 数组的栈操作
使用javascript给数组提供的<code>push()</code>和<code>pop()</code>方法，可以实现类似栈的操作:

```javascript
var words=['a', 'b', 'c'];       //创建一个数组；

var count = words.push('d');   //  push方法推入新项，会放在数组的最后，并返回数组的长度。

alert(count);   // 4

var item = words.pop();   //取出数组中最后一项，在数组中删除这一项，并返回取出的这一项。

alert(item);           // 'd'

alert(words.length);   //  3
```
<!-- more -->
###2. 数组的队列操作
使用以上介绍的<code>push()</code>并配合<code>shift()</code>可以实现数组队列的操作，因为<code>shift()</code>与<code>pop()</code>相反，是取出数组中的第一项并返回值。

```javascript
var words = ['a', 'b', 'c'];       //创建一个数组；

var count = words.push('d');  // push方法推入新项，会放在数组的最后，并返回数组的长度。

alert(count);   // 4，此时words顺序为['a', 'b', 'c', 'd']

var item = words.shift();   // 取得第一项，在数组中移除，并返回取出的这一项。

alert(item);   // 'a' 此时words顺序为'b', 'c', 'd']

alert(words.length);  //3
```
如果想进行反向队列的操作，则相应地使用<code>unshift()</code>与<code>pop()</code>即可。依上述类推，很容易知道<code>unshift()</code>就是给数组从头部添加新项，并返回数组长度，这里就不写代码啦。

    

###3. **细节**，关于同时给栈/队列新添两项的顺序问题
如果在以上的方法里给出两个参数或两个以上参数，他们的栈和队列放入和取出的顺序又是如何的呢？

```javascript
	var words = ['a', 'b', 'c'];

	words.push('d', 'e');  // ['a', 'b', 'c', 'd', 'e']

	words.unshift('i', 'j'); // ['i', 'j', 'a', 'b', 'c', 'd', 'e']

```

以上代码的意思是，要注意，就算是<code>unshift('i', 'j')</code>会在words数组头部像栈/队列一样放入数据，其也依然会将两个参数相对整体地一次插入进去，而不是如前文所说的将两个参数分开插入。否则'i'和'j'的顺序就不是参数里的顺序了。
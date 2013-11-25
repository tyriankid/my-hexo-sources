title: 从JS数组中看栈与队列
date: 2012-08-24 16:31:29
tags: [栈, 队列, javascript]
category: javascript
---

###1. 数组的栈操作
使用javascript给数组提供的```push()```和```pop()```方法，可以实现类似栈的操作:

    var words=['a', 'b', 'c'];       //创建一个数组；

    var count=words.push('d');   //  push方法推入新项，会放在数组的最后，并返回数组的长度。

    alert(count);   // 4

    var item=words.pop();   //取出数组中最后一项，在数组中删除这一项，并返回取出的这一项。

    alert(item);           // 'd'

    alert(words.length);   //  3


###2. 数组的队列操作
使用以上介绍的```push()```并配合```shift()```可以实现数组队列的操作，因为```shift()```与```pop()```相反，是取出数组中的第一项并返回值。

    var words=['a', 'b', 'c'];       //创建一个数组；

    var count=words.push('d');  // push方法推入新项，会放在数组的最后，并返回数组的长度。

    alert(count);   // 4，此时words顺序为['a', 'b', 'c', 'd']

    var item=words.shift();   // 取得第一项，在数组中移除，并返回取出的这一项。

    alert(item);   // 'a' 此时words顺序为'b', 'c', 'd']

    alert(words.length);  //3

如果想进行反向队列的操作，则相应地使用```unshift()```与```pop()```即可。依上述类推，很容易知道```unshift()```就是给数组从头部添加新项，并返回数组长度，这里就不写代码啦。

    

###3. 细节，关于同时给栈/队列新添两项的顺序问题

    
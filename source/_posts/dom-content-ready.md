title: 谈谈JS开始加载的时机
date: 2012-09-18 00:12:51
tags: [javascript, jQuery, 前端框架]
category: javascript
---
我如大多数人一样，在开始一段JS代码时会习惯性地用一些前端框架的API，譬如jQuery的<code>$(function(){})</code>开头，保证JS会在DOM加载完毕后开始运行，这样保证了JS对DOM操作时不会出错。

简简单单，一劳永逸。

但凡事总得说个明白，探个究竟不是？正如今天，帮公司一位设计师制作一个比较简单的个人主页（作品展示，图片较多），总共也就不超过100行代码。但若我要为这100行代码而加一个jQuery，或者别的，总感觉很别扭。
<!-- more -->

##**那么来谈谈脱离框架的情况吧**

###**为什么不用<code>window.onload</code>**

这个喜闻乐见的事件绑定没有想象中那么智能。<code>window</code>对象的<code>onload</code>事件触发，不仅仅需要DOM加载完毕，还需要将页面中的其他全部资源，譬如图片，加载完毕才会触发。这显然是不可取的。

###**正常一点的办法**

Mozilla首先支持了一个名为<code>DomContentLoaded</code>的事件，震惊世界。随后，Opera以及众webkit党的新版本也紧随脚步支持了这个事件。

```javascript
document.addEventListener("DOMContentLoaded", init, false);
```

顾名思义，这个事件正是在DOM加载完毕后触发的，很完美地解决了JS开始运行的时机问题，但是……

没错，这时候IE杀出来了。对于受众不小的IEx党，这种引领潮流的事件想当然地也不会被其支持。所以必须得用IE特色的路线来做这个事，即：
```javascript
try {

	// http://javascript.nwbox.com/IEContentLoaded/
    document.documentElement.doScroll("left");

} catch( error ) {

    setTimeout( arguments.callee, 1 );

    return;

}   
```
思路是不断地调用<code>document.documentElement.doScroll("left")</code>，直到它可以正确被调用，就说明DOM加载好了。

是否很奇葩？大多数的前端框架，对于这个事情的处理思路，大概也就是上面这两大点。

###**关于细节**

比如低版本的webkit内核浏览器，不支持<code>DomContentLoaded</code>，也没有<code>doScroll("left")</code>，则应该依托于监听<code>readystatechange</code>事件来模拟以上的效果，即当其的值为<code>'4'</code>时说明文档加载完毕。

然而这个事件现在已经出现得比较少，jQuery的实现似乎也已经忽略了它的存在。谁叫IE之外的浏览器都可以自动升级呢。

哦对了，对于这个<code>readystatechange</code>事件，在IE里的效果与<code>window.onload</code>是相似的，不可取不可取。
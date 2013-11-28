title: 总是记不住的垂直居中
date: 2013-06-04 21:20:05
tags: 垂直居中
category: css
---
刚入门前端的时候，就记住了单行文本可以用设置line-height与容器height相同值这个方法来实现垂直居中，但一直在潜意识地忽视多行文本的垂直居中，以至于之后在项目里每次遇到这个问题都会度娘很长时间！

**这次一定要记下来。**

1. 尝试过切一张1*height规格的透明图片放到容器里，让文字`vertical-align:middle;`，失败，后证实这个方法只适用于图片垂直居中。

2. 设置文本父容器`display:table;`，文本的容器`display:table-cell; vertical-align:middle;`即可。

可是这一次为什么失效了呢？

<del>因为bootstrap的默认样式将我现在用的`<li>`默认浮动了，</del>

因为我在`<li>`内部使用了bootstrap的`span*`布局，致使文字接受了`span*`的默认样式`[class*="span"]{float: left;}`所以<del>响应</del>相应地加上`float:none;`就好了！

**这次一定要记住记住记住。**
在编写node程序的时候，经常会遇到的问题是path.resolve或者relative方法返回的结果在linux和windows下不一样。linux返回的路径分隔符是左斜杠（/），而windows返回的路径分隔符是右斜杠（\\）。

大部分情况下，我们不需要做额外的处理，各自维护自己的路径格式即可，程序本身不需要关心返回的路径格式。但是在调用一些其他模块的时候，可能会遇到这样的问题。

分隔符本来也不是什么大问题，但肯定不是简单的字符串替换能解决的。比如，我们需要将windows下拿到的路径转换成linux下的路径。
```
D:\\desktop\\dev\\workspace\\k2\\seed\\seed.js
```
第一反应是使用replace来解决，但比较推荐的方式是使用path.sep来代替正则的匹配，主要作用是保证代码兼容性的同时也增加代码的可读性，不需要考虑系统版本。
```
'D:\\desktop\\dev\\workspace\\k2\\seed\\seed.js'.split(path.sep).join('/');
```
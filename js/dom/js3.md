# 常用js页面跳转方式
工作中会常用到必须用js的页面跳转，刷新，总结了一下常用的js跳转页面的方法和页面刷新及页面自动刷新，js引入js文件的常用技巧，便于查阅。

1.window.location.href方式
```js
window.location.href="target.aspx";  
```
2.window.navigate方式跳转
```js
 window.navigate("target.aspx");
 ```
3.self.location方式实现页面跳转，和下面的top.location有小小区别
```js
self.location='target.aspx';  
```
4.top.location
```js
top.location='target.aspx';  
```
5.不推荐这种方式跳转
```jsd
 alert("返回");  
 window.history.back(-1); 
 ```
6.小技巧(JS引用JS):
```js
if (typeof SWFObject == "undefined") {    
    document.write('<scr' + 'ipt type="text/javascript" src="/scripts/swfobject-1.5.js"></scr' + 'ipt>');  
}    
```
7.Javascript刷新页面的几种方法：
```js
history.go(0)  
location.reload()  
location=location  
location.assign(location)  
document.execCommand('Refresh')  
window.navigate(location)  
location.replace(location)  
document.URL=location.href  
```
8.自动刷新页面的方法:页面自动刷新：把如下代码加入head区域中,其中20指每隔20秒刷新一次页面.
```js
<meta http-equiv="refresh" content="20">  
```
9.页面自动跳转：把如下代码加入head区域中,其中20指隔20秒后跳转到http://www.qianduandu.com页面
```js
<meta http-equiv="refresh" content="20;url=http://www.qianduandu.com">  
```
10.如果想关闭窗口时刷新或者想开窗时刷新的话，在中调用以下语句即可。
```js
<body onload="opener.location.reload()"> 开窗时刷新   
<body onUnload="opener.location.reload()"> 关闭时刷新 
window.opener.document.location.reload()   
```
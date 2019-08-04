---
title: 跨浏览器的javascript中鼠标滚轮事件
tags: javascript
---
# 跨浏览器的javascript中鼠标滚轮事件
参考：
[解析javascript中鼠标滚轮事件](http://www.jb51.net/article/66710.htm)

[JS滚轮事件(mousewheel/DOMMouseScroll)了解](http://www.zhangxinxu.com/wordpress/2013/04/js-mousewheel-dommousescroll-event/)

##### 1.事件绑定
Firefox使用addEventListener添加滚轮事件

```
/*Firefox注册事件*/
if(document.addEventListener){
    document.addEventListener('DOMMouseScroll',scrollFunc,false);
}
```
其中除Firefox外其余均可使用HTML DOM方式添加事件，因此添加事件使用以下方式

```
/*注册事件*/
if(document.addEventListener){
    document.addEventListener('DOMMouseScroll',scrollFunc,false);
}//W3C
window.onmousewheel=document.onmousewheel=scrollFunc;//IE/Opera/Chrome
```
##### detail与wheelDelta
判断滚轮向上或向下的属性值，现在五大浏览器（IE、Opera、Safari、Firefox、Chrome）中Firefox 使用detail，其余四类使用wheelDelta；两者只在取值上不一致，代表含义一致，detail与wheelDelta只各取两个值，detail只取±3，wheelDelta只取±120，其中FireFox浏览器向下滚动是正值，而其他浏览器是负值。

##### 兼容写法

```
/**
 * 简易的判断滚动方向   
 */
 
var scrollFunc=function(e){
     var direct=0;
     e=e || window.event;
    var flag;
     if(e.wheelDelta){//IE/Opera/Chrome
         if(e.wheelDelta>0){
             flag="up";
         }else{
              flag="down";
         }
     }else if(e.detail){//Firefox
        
     }
 }
24 /*注册事件*/
25 if(document.addEventListener){
26     document.addEventListener('DOMMouseScroll',scrollFunc,false);
27 }//W3C
28 window.onmousewheel=document.onmousewheel=scrollFunc;//IE/Opera/Chrome/Safari


```

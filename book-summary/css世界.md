1. 选择器的种类：基础选择器 + 关系型选择器
2. 标签的分类：
- 块级元素和内联元素 （！块级元素并不等于display : block,例如 li 元素的 display 值为 list-item ，table 元素则为 table）;
- 
3. IE 浏览器无法支持 list-item 的原因：无法生成外部防止圆点标记的盒子；
4. 所有盒子都由两种盒子结构组成，块级盒子（负责结构）内联盒子（负责内容）。内联元素（inline-block）即为外层内联盒子内层块级盒子。
5. width: auto 的作用
- 充分利用可用空间；
- 收缩与包裹；
- 收缩到最小；
- 超出容器限制；（只要不指定宽度又没有设置 whit-space:nowrap 是不会超出容器边界的）
> 要充分利用浏览器原生流特性的好处
6. button 按钮和 input 按钮的区别：
- button 按钮标签文字会自动换行，input 标签按钮因为有 white-space:pre 不会自动换行，改值为 normal 则可以换行； 
7. 需求：模块内的文字是动态的，要求文字少的时候居中显示，文字超出一行时居左显示 。

```
.box { text-align: center};// 外部容器盒子
.content { display: inline-block; // 内部文本盒子 text-align:left}
```

8. width 是作用在 content box 上面的（或许是因为 width 是CSS2.1 制定的，而 CSS2.1 是面向内容设计的），而浏览器对于 content box 的尺寸定义不一致（是否包括 padding、border不一样，因而会有宽度计算问题），而 box-sizing 正是调整内部 width 作用细节而定义的方式，box-sizing:border-box,即为IE盒子的计算方式，将 width 作用在 border-box上面。
9. 外部尺寸：
- 正常流宽度（表现为“外部尺寸”的块级元素一旦设置了宽度，流动性就丢失了）
- 格式化宽度（仅出现在绝对定位模型中，默认情况下，绝对定位的宽度表现是“包裹”性的，然而非替换元素，当top/left或 right/bottom 等对立方位的属性值提示存在时，元素宽度表示为“格式化宽度”，宽度大小相对于最近的具有定位特性的祖先元素计算，具有完全的流体性）
10. 内部尺寸与流体特性
- 包裹性（包裹+自适应）。
- 首选最小宽度。
即便外部设置width:0;内部的图片文字宽度也会有一个最小宽度而不是0;
- 最大宽度
，等于设置white-psace设置no-wrap后的宽度。
11. box-sizing 的设计初衷

**解决非替换元素的自适应宽度问题**
- 对于非替换元素，display:block会具有流动性，宽度由外部决定。
- 非替换元素宽度不受display/外部容器影响，因而通过给替换元素设置display:block是无法实现宽度100%自适应的。因而需要显式指定width
> 因而，在重置代码里加上 input, textarea, img, video, object { box-sizing:border-box; }是合理且必要的
有效
12. 为何 height:100%无效，而宽度100%
- 当未指定高度值时默认值为auto
而单位百分比则是：将高度定义为相对包含块高度的百分比。
```
'auto'*100%=NaN
```
- width 默认虽然也是auto，但是只却是有真实值计算而来的
13. 非绝对定位元素的宽高百分比是对应 content box 的，绝对定位元素的则是对应 padding box的；
14. max-*系列的初始值为none, min-*系列的则为auto,理解此点对于动画过渡方面的区别挺大的。
与height\width等的覆盖规则：
- max-width 将会覆盖width,即便是设置了!important的width;
- 在冲突时，min-width 将会覆盖 max-width；
15. 根据是否具有可替换内容，元素可分为可替换元素和非替换元素。
- 替换元素：通过修改某个属性值所呈现的内容就会被改变的元素。

**特性：**

(1)内容元素的外观不受页面的css影响（本质上是web component,内部样式为shadow dom因而不受外界控制）；

(2)有自己的尺寸，通常默认为300*150;

(3)所有替换元素都是内联元素，但是默认的display值却是不一样的。
(4)替换元素的尺寸规则：
css尺寸>html尺寸>固有尺寸（例如img图片自身的大小）>默认尺寸（在没指定内容时）

一个为首屏图片不影响布局处理的css：
img {visibility:hiden}
img[src] {visibility:visible}
没有src不会产生任何请求

**其他知识点：**

(5)firefox的::before微元素的content值设置会被无视，after则有效；

(6)p51一个基于伪元素的图片生成技术，技术支持理论：
去掉src属性，很多替换元素就变成替换元素
- 核心代码

```
img::after {
    /* 生成alt信息 */
    content: attr(alt);
    /* 尺寸和定位 */
    position: absolute;
    bottom: 0;
    width: 100%;
    background-color: rgba(0, 0, 0, .5);
    transform: translateY(100%);
    /* 过渡动画效果 */
    transition: transform .2s;
}
img:hover::after {
    /* alt 信息展示 */
    transform: translateY(0);
}
```
原理：图片未加载时，没有src此时为非替换元素，hover后显示alt提示文本；加载后为替换元素，:after,:before特性失效

(7)在chrome下，所有元素都支持content属性，而其他浏览器仅在:before等伪元素内有效。利用content属性，可以让普通标签变成替换元素。
应用举例：常见网站的标题用h1标签，但通常都使用特殊处理的字体图片而非直接使用字体，为了保证seo的友好，通常会在标签内写上文字内容，然后设置text-indent:-999px;来隐藏文字。利用content的新方法：

```
h1 {
    content:url(logo.svg);
}
```

（8）利用content生成文字的坏处：无法被屏幕阅读设备读取，无法被搜索引擎抓取，对可访问性和seo都不太友好。


- 非替换元素：
16. 关于content内容生成技术
- content辅助元素生成：利用其他css代码来生成辅助元素，或实现图形效果，或实现特定布局，会使HTML代码更加干净简洁。
- content字符内容生成：应用例子（iconfont），可利用该特性实现ie6-ie9的动态加载动画效果
- content图片生成：通过给content赋予url(图片地址)来实现。现实中很少使用该方式，因为这样生成的图片尺寸不好控制
- attr属性值内容生成（使用方式类似函数，指定的属性值名称不要加引号）
- content计数器：应用实例（购物车、书籍目录）
17. padding元素，利用其特性可轻易实现 登录注册中间的“管道符”；
实例代码：
```
a = a:before {
    content:"";
    font-size:0;
    padding:10px 3px 1px;
    margin-left:6px;
    border-left；1px solid gray; 
}
```
18. 内联元素设置padding不会加入行盒高度的计算，也就是不影响布局，但是会实际会发生渲染，可利用此特性给一些内联点击元素扩大点击区域；对于内联元素，padding是会断行的，宽高完全受font-size大小控制、
19. margin\padding百分比值无论是哪个方向的都是基于宽度计算的
20. 由于button元素的内置padding在多浏览器下很难控制，因而通常都使用a模拟按钮居多。
21. 可以利用padding来实现三道杠和双层圆点。
22. 关于内部尺寸与margin\padding的关系：两者都可以改变元素的可视尺寸，对于padding，元素设置了width或者保持其包裹性时，会改变元素尺寸，而margin,只有在元素是“充分利用可用空间”状态（流布局，宽度自适应），才可以改变元素尺寸。可利用此特性，使用负值margin来消除最后一个子元素margin-left。
23. 对于普通的块状元素，在默认的水平流下，margin只能改变左右方向的内部尺寸。但如果使用writing-mode改变流向为垂直流，则水平方向内部尺寸无法改变，垂直方向可以改变。
24. 如果容器可以滚动，在IE和FireBox下是会忽略padding-bottom值的。因而只能使用子元素的margin-bottom来实现滚动容器的底部留白。
25. 使用margin负值可以实现等高布局，但无法满足子元素需要需要定位在父容器之外的布局。
26. margin合并只发生在：（1）垂直方向；（2）块级元素（不包括浮动和绝对定位元素）
27. margin合并的三种场景：（1）相邻兄弟元素的上下margin；（2）父级和第一个/最后一个子元素。阻止该情况margin合并的方式：
对于margin-top的处理方法（满足一个即可）
- 父元素设置为块状格式化上下文元素；
- 父元素设置Border-top;
- 父元素设置padding-top;
- 父元素和第一个子元素之间添加内联元素进行分隔；
对于margin-bottom的处理方法（满足一个）
- 父元素设置为块状格式化上下文元素；
- 父元素设置Border-bottom;
- 父元素设置padding-bottom;
- 父元素设置height\min-height\或max-height；
(3)空块级元素的margin合并
28. 
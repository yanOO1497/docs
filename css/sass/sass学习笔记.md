
# sass学习笔记
[toc]
## 一、入门
#### 1.什么是预编译处理器
通俗的说，“CSS 预处理器用一种专门的编程语言，进行 Web 页面样式设计，然后再编译成正常的 CSS 文件，以供项目使用。CSS 预处理器为 CSS 增加一些编程的特性，无需考虑浏览器的兼容性问题”，例如你可以在 CSS 中使用变量、简单的逻辑程序、函数（如右侧代码编辑器中就使用了变量$color）等等在编程语言中的一些基本特性，可以让你的 CSS 更加简洁、适应性更强、可读性更佳，更易于代码的维护等诸多好处。
##### 其它预处理器
1. Sass（SCSS）
1. LESS
1. Stylus
1. Turbine
1. Swithch CSS
1. CSS Cacheer
1. DT CSS

到目前为止，在众多优秀的 CSS 预处理器语言中就属 Sass、LESS 和 Stylus 最优秀，讨论的也多，对比的也多。
#### 2.什么是 Sass？
Sass 是采用 Ruby 语言编写的一款 CSS 预处理语言，它诞生于2007年，是最大的成熟的 CSS 预处理语言。最初它是为了配合 HAML（一种缩进式 HTML 预编译器）而设计的，因此有着和 HTML 一样的缩进式风格。
#### 3.Sass 和 SCSS 有什么区别？
Sass 和 SCSS 其实是同一种东西，我们平时都称之为 Sass，两者之间不同之处有以下两点：
文件扩展名不同，Sass 是以“.sass”后缀为扩展名，而 SCSS 是以“.scss”后缀为扩展名
语法书写方式不同，Sass 是以严格的缩进式语法规则来书写，不带大括号({})和分号(;)，而 SCSS 的语法书写和我们的 CSS 语法书写方式非常类似。

先来看一个示例

##### Sass 语法

```
$font-stack: Helvetica, sans-serif  //定义变量
$primary-color: #333 //定义变量

body
  font: 100% $font-stack
  color: $primary-color
```
##### Scss 语法

```
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```
##### 编译出来的 CSS

```
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```
#### Sass 和 CSS 写法有差别：
Sass 和 CSS 写法的确存在一定的差异，由于 Sass 是基于 Ruby 写出来，所以其延续了 Ruby 的书写规范。在书写 Sass 时不带有大括号和分号，其主要是依靠严格的缩进方式来控制的。如：
##### Sass写法：

```
body
  color: #fff
  background: #f36
```
##### css写法：

```
body{
  color:#fff;
  background:#f36;
}
```
#### SCSS 和 CSS 写法无差别：
SCSS 和 CSS 写法无差别，这也是 Sass 后来越来越受大众喜欢原因之一。简单点说，把你现有的“.css”文件直接修改成“.scss”即可使用。
## 二、SCSS语法格式

有不少同学使用 Sass 新的语法规则，而文件扩展名依旧使用的是“.sass”，这也就造成血案了，编译时说编译不出来。在此特别提醒新同学：“.sass”只能使用 Sass 老语法规则（缩进规则），“.scss”使用的是 Sass 的新语法规则，也就是 SCSS 语法规则（类似 CSS 语法格式）。

### Sass 编译
#### 命令编译
命令编译是指使用你电脑中的命令终端，通过输入 Sass 指令来编译 Sass。这种编译方式是最直接也是最简单的一种方式。因为只需要在你的命令终端输入：
##### 单文件编译：

```
sass <要编译的Sass文件路径>/style.scss:<要输出CSS文件路径>/style.css
```
这是对一个单文件进行编译，如果想对整个项目所有 Sass 文件编译成 CSS 文件，可以这样操作：
##### 多文件编译：

```
sass sass/:css/
```
##### 缺点及解决方法：
在实际编译过程中，你会发现上面的命令，只能一次性编译。每次个性保存“.scss”文件之后，都得重新执行一次这样的命令。如此操作太麻烦，其实还有一种方法，就是在编译Sass 时，开启“watch”功能，这样只要你的代码进行任保修改，都能自动监测到代码的变化，并且给你直接编译出来：

```
sass --watch <要编译的Sass文件路径>/style.scss:<要输出CSS文件路径>/style.css
```

#### GUI工具编译
我一直讨厌使用命令来做事情，我喜欢那种能看得到的界面操作。那么你可以考虑使用 GUI 界面工具来对 Sass 进行编译。当然不同的 GUI 工具操作方法略有不同。如果在此也一一对编译的界面工具做详细的介绍。我们可能需要写一本书来介绍这些编译工具的操作了。所以我们这里做一下简单介绍，对于 GUI 界面编译工具，目前较为流行的主要有：

Koala (http://koala-app.com/)
Compass.app（http://compass.kkbox.com/）
Scout（http://mhs.github.io/scout-app/）
CodeKit（https://incident57.com/codekit/index.html）
Prepros（https://prepros.io/）

相比之下，我比较推荐使用以下两个：

Koala (http://www.w3cplus.com/preprocessor/sass-gui-tool-koala.html) <br>
CodeKit (http://www.w3cplus.com/preprocessor/sass-gui-tool-codekit.html)
#### 自动化编译
##### 1、Gulp 配置 Sass 编译的示例代码

```
var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('sass', function () {
    gulp.src('./scss/*.scss')
        .pipe(sass())
        .pipe(gulp.dest('./css'));
});

gulp.task('watch', function() {
    gulp.watch('scss/*.scss', ['sass']);
});

gulp.task('default', ['sass','watch']);
```
设置输出风格

```
gulp.task('sass', function () {
 return gulp.src('./sass/**/*.scss')
   .pipe(sass({outputStyle: 'expanded'}).on('error', sass.logError))
   .pipe(gulp.dest('./css'));
});
```

##### 2、Grunt 配置 Sass 编译的示例代码

```
module.exports = function(grunt) {
    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        sass: {
            dist: {
                files: {
                    'style/style.css' : 'sass/style.scss'
                }
            }
        },
        watch: {
            css: {
                files: '**/*.scss',
                tasks: ['sass']
            }
        }
    });
    grunt.loadNpmTasks('grunt-contrib-sass');
    grunt.loadNpmTasks('grunt-contrib-watch');
    grunt.registerTask('default',['watch']);
}
```
想了解 Grunt 同学请单击这里学习[《Grunt-beginner前端自动化工具》](http://www.imooc.com/learn/30)。
### [Sass]常见的编译错误
在编译 Sass 代码时常常会碰到一些错误，让编译失败。这样的错误有系统造成的也有人为造成的，但大部分都是人为过失引起编译失败。<br>

<strong>字符编译:</strong>而最为常见的一个错误就是字符编译引起的。在Sass的编译的过程中，是不是支持“GBK”编码的。所以在创建 Sass 文件时，就需要将文件编码设置为“utf-8”。<br>

<strong>中文字符:</strong>另外一个错误就是路径中的中文字符引起的。建议在项目中文件命名或者文件目录命名不要使用中文字符。而至于人为失误造成的编译失败，在编译过程中都会有具体的说明，大家可以根据编译器提供的错误信息进行对应的修改。

#### [Sass]不同样式风格的输出方法
众所周知，每个人编写的 CSS 样式风格都不一样，有的喜欢将所有样式代码都写在同一行，而有的喜欢将样式分行书写。在 Sass 中编译出来的样式风格也可以按不同的样式风格显示。其主要包括以下几种样式风格：
1. 嵌套输出方式 nested
1. 展开输出方式 expanded  
1. 紧凑输出方式 compact 
1. 压缩输出方式 compressed

##### [Sass]嵌套输出方式 nested
Sass 提供了一种嵌套显示 CSS 文件的方式。

```
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```
在编译的时候带上参数“ --style nested”:

```
sass --watch test.scss:test.css --style nested
```
编译出来的 CSS 样式风格：

```
nav ul {
  margin: 0;
  padding: 0;
  list-style: none; }
nav li {
  display: inline-block; }
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none; }
```
默认是nested，所以加不加--style nested不影响效果。

##### 2、嵌套输出方式 expanded
这个输出的 CSS 样式风格和 nested 类似，只是大括号在另起一行，同样上面的代码，编译出来：

```
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```
##### 3、紧凑输出方式 compact
该方式适合那些喜欢单行 CSS 样式格式的朋友，编译后的代码如下：

```
nav ul { margin: 0; padding: 0; list-style: none; }
nav li { display: inline-block; }
nav a { display: block; padding: 6px 12px; text-decoration: none; }
```
##### 4.压缩输出方式 compressed
压缩输出方式会去掉标准的 Sass 和 CSS 注释及空格。也就是压缩好的 CSS 代码样式风格：

```
nav ul{margin:0;padding:0;list-style:none}nav li{display:inline-block}nav a{display:block;padding:6px 12px;text-decoration:none}
```
编译出来的CSS样式风格的选择完全是个人喜好问题，可以根据自己喜欢的风格选择参数。
一段时间之后，你实际上就不再需要写 CSS 代码了，只用写 Sass 代码。在这种情况下，你只需要设定输出格式为压缩格式，知道输出的 CSS 代码可以直接使用即可。

#### Sass 的调试
Sass 调试一直以来都是一件头痛的事情，使用 Sass 的同学都希望能在浏览器中直接调试 Sass 文件，能找到对应的行数。值得庆幸的是，现在实现并不是一件难事，只要你的浏览器支持“sourcemap”功能即可。早一点的版本，需要在编译的时候添加“--sourcemap”  参数：

```
sass --watch --scss --sourcemap style.scss:style.css
```
在 Sass3.3 版本之上（我测试使用的版本是 3.4.7），不需要添加这个参数也可以：

```
sass --watch style.scss:style.css
```
在命令终端，你将看到一个信息：

```
>>> Change detected to: style.scss
  write style.css
  write style.css.map
```
这时你就可以像展示的 gif 图一样，调试你的 Sass 代码。
![image](http://img.mukewang.com/54f7b71d0001bb0b05050268.jpg)


## sass的基本特性
### 声明变量
在有些编程语言中（如，JavaScript）声明变量都是使用关键词“var”开头，但是在 Sass 不使用这个关键词，而是使用大家都喜欢的美元符号“$”开头。我想用一张图来解释，我一直坚信，一图胜千言万语：
![image](http://img.mukewang.com/551e065c0001435e07870307.jpg)
上图非常清楚告诉了大家，Sass 的变量包括三个部分：
1. 声明变量的符号“$”
1. 变量名称
1. 赋予变量的值

来看一个简单的示例，假设你的按钮颜色可以给其声明几个变量：

```
$brand-primary : darken(#428bca, 6.5%) !default; // #337ab7
$btn-primary-color : #fff !default;
$btn-primary-bg : $brand-primary !default;
$btn-primary-border : darken($btn-primary-bg, 5%) !default;
```
如果值后面加上!default则表示默认值。

注：了解 Bootstrap 的 Sass 版本的同学，就一眼能看出，上面的示例代码是 Bootstrap 定义 primarybutton 的颜色。
### 普通变量与默认变量
#### 普通变量
定义之后可以在全局范围内使用。

```
$fontSize: 12px;
body{
    font-size:$fontSize;
}
```
编译后的css代码：

```
body{
    font-size:12px;
}
```
#### 默认变量
sass 的默认变量仅需要在值后面加上 !default 即可。

```
$baseLineHeight:1.5 !default;
body{
    line-height: $baseLineHeight; 
}
编译后的css代码：
body{
    line-height:1.5;
}
```
sass 的默认变量一般是用来设置默认值，然后根据需求来覆盖的，覆盖的方式也很简单，只需要在默认变量之前重新声明下变量即可。

```
$baseLineHeight: 2;
$baseLineHeight: 1.5 !default;
body{
    line-height: $baseLineHeight; 
}
编译后的css代码：
body{
    line-height:2;
}
```

可以看出现在编译后的 line-height 为 2，而不是我们默认的 1.5。默认变量的价值在进行组件化开发的时候会非常有用。


!default应该是一个默认值，就相当于在一个变量里，先设置一个数值，如果有其他的值则优先替换为实际的，没有其他的则显示这个默认的
###### 优先级
!default < 新属性值 < !important(按css的书写)

**scss中覆盖默认变量的方式：在默认变量之前重新声明**
#### 变量的调用
在 Sass 中声明了变量之后，就可以在需要的地方调用变量。调用变量的方法也非常的简单。
比如在定义了变量

```
$brand-primary : darken(#428bca, 6.5%) !default; // #337ab7
$btn-primary-color: #fff !default;
$btn-primary-bg : $brand-primary !default;
$btn-primary-border : darken($btn-primary-bg, 5%) !default;
```

在按钮 button 中调用，可以按下面的方式调用

```
.btn-primary {
   background-color: $btn-primary-bg;
   color: $btn-primary-color;
   border: 1px solid $btn-primary-border;
}
```

编译出来的CSS:

```
.btn-primary {
  background-color: #337ab7;
  color: #fff;
  border: 1px solid #2e6da4;
}
```
### 全局变量与局部变量
Sass 中变量的作用域在过去几年已经发生了一些改变。直到最近，规则集和其他范围内声明变量的作用域才默认为本地。如果已经存在同名的全局变量，从 3.4 版本开始，Sass 已经可以正确处理作用域的概念，并通过创建一个新的局部变量来代替。

先来看一下代码例子：

```
//SCSS
$color: orange !default;//定义全局变量(在选择器、函数、混合宏...的外面定义的变量为全局变量)
.block {
  color: $color;//调用全局变量
}
em {
  $color: red;//定义局部变量
  a {
    color: $color;//调用局部变量
  }
}
span {
  color: $color;//调用全局变量
}
```

css 的结果：

```
//CSS
.block {
  color: orange;
}
em a {
  color: red;
}
span {
  color: orange;
}
```

上面的示例演示可以得知，在元素内部定义的变量不会影响其他元素。如此可以简单的理解成，全局变量就是定义在元素外面的变量，如下代码：

```
$color:orange !default;
```

$color 就是一个全局变量，而定义在元素内部的变量，比如 $color:red; 是一个局部变量。
除此之外，Sass 现在还提供一个 !global 参数。!global 和 !default 对于定义变量都是很有帮助的。我们之后将会详细介绍这两个参数的使用以及其功能。

#### 全局变量的影子
当在局部范围（选择器内、函数内、混合宏内...）声明一个已经存在于全局范围内的变量时，局部变量就成为了全局变量的影子。基本上，局部变量只会在局部范围内覆盖全局变量。
上面例子中的 em 选择器内的变量 $color 就是一个全局变量的影子。

```
//SCSS
$color: orange !default;//定义全局变量
.block {
  color: $color;//调用全局变量
}
em {
  $color: red;//定义局部变量（全局变量 $color 的影子）
  a {
    color: $color;//调用局部变量
  }
}
```

#### 什么时候声明变量？
我的建议，创建变量只适用于感觉确有必要的情况下。不要为了某些骇客行为而声明新变量，这丝毫没有作用。只有满足所有下述标准时方可创建新变量：
1. 该值至少重复出现了两次；
1. 该值至少可能会被更新一次；
1. 该值所有的表现都与变量有关（非巧合）。

基本上，没有理由声明一个永远不需要更新或者只在单一地方使用变量。

### 嵌套-选择器嵌套
Sass 中还提供了选择器嵌套功能，但这也并不意味着你在 Sass 中的嵌套是无节制的，因为你嵌套的层级越深，编译出来的 CSS 代码的选择器层级将越深，这往往是大家不愿意看到的一点。这个特性现在正被众多开发者滥用。
选择器嵌套为样式表的作者提供了一个通过局部选择器相互嵌套实现全局选择的方法，Sass 的嵌套分为三种：

1. 选择器嵌套
1. 属性嵌套
1. 伪类嵌套

#### 1、选择器嵌套
假设我们有一段这样的结构：

```
<header>
<nav>
    <a href=“##”>Home</a>
    <a href=“##”>About</a>
    <a href=“##”>Blog</a>
</nav>
<header>
```

想选中 header 中的 a 标签，在写 CSS 会这样写：

```
nav a {
  color:red;
}

header nav a {
  color:green;
}
```

那么在 Sass 中，就可以使用选择器的嵌套来实现：

```
nav {
  a {
    color: red;

    header & {
      color:green;
    }
  }  
}
```
> &代表&所在的嵌套结构。
&理解为父选择器，虽然header是父级，但它写在最里面，&引用父级，即为nav a

### 嵌套-属性嵌套
Sass 中还提供属性嵌套，CSS 有一些属性前缀相同，只是后缀不一样，比如：border-top/border-right，与这个类似的还有 margin、padding、font 等属性。假设你的样式中用到了：

```
.box {
    border-top: 1px solid red;
    border-bottom: 1px solid green;
}
```

在 Sass 中我们可以这样写：

```
.box {
  border: {
   top: 1px solid red;
   bottom: 1px solid green;
  }
}
```

### 嵌套-伪类嵌套
其实伪类嵌套和属性嵌套非常类似，只不过他需要借助`&`符号一起配合使用。我们就拿经典的“clearfix”为例吧：

```
.clearfix{
&:before,
&:after {
    content:"";
    display: table;
  }
&:after {
    clear:both;
    overflow: hidden;
  }
}
```

编译出来的 CSS：

```
clearfix:before, .clearfix:after {
  content: "";
  display: table;
}
.clearfix:after {
  clear: both;
  overflow: hidden;
}
```

#### 避免选择器嵌套：
1. 选择器嵌套最大的问题是将使最终的代码难以阅读。开发者需要花费巨大精力计算不同缩进级别下的选择器具体的表现效果。<br>
1. 选择器越具体则声明语句越冗长，而且对最近选择器的引用(&)也越频繁。在某些时候，出现混淆选择器路径和探索下一级选择器的错误率很高，这非常不值得。<br>

为了防止此类情况，我们应该尽可能避免选择器嵌套。然而，显然只有少数情况适应这一措施。
### 混合宏-声明混合宏
如果你的整个网站中有几处小样式类似，比如颜色，字体等，在 Sass 可以使用变量来统一处理，那么这种选择还是不错的。但当你的样式变得越来越复杂，需要重复使用大段的样式时，使用变量就无法达到我们目了。这个时候 Sass 中的混合宏就会变得非常有意义。在这一节中，主要向大家介绍 Sass 的混合宏。
#### 1、声明混合宏
不带参数混合宏：
在 Sass 中，使用“@mixin”来声明一个混合宏。如：

```
@mixin border-radius{
    -webkit-border-radius: 5px;
    border-radius: 5px;
}
```

其中 @mixin 是用来声明混合宏的关键词，有点类似 CSS 中的 @media、@font-face 一样。border-radius 是混合宏的名称。大括号里面是复用的样式代码。
带参数混合宏：
除了声明一个不带参数的混合宏之外，还可以在定义混合宏时带有参数，如：

```
@mixin border-radius($radius:5px){
    -webkit-border-radius: $radius;
    border-radius: $radius;
}
```

#### 复杂的混合宏：
上面是一个简单的定义混合宏的方法，当然， Sass 中的混合宏还提供更为复杂的，你可以在大括号里面写上带有逻辑关系，帮助更好的做你想做的事情,如：

```
@mixin box-shadow($shadow...) {
  @if length($shadow) >= 1 {
    @include prefixer(box-shadow, $shadow);
  } @else{
    $shadow:0 0 4px rgba(0,0,0,.3);
    @include prefixer(box-shadow, $shadow);
  }
}
```

这个 box-shadow 的混合宏，带有多个参数，这个时候可以使用“ … ”来替代。简单的解释一下，当 $shadow 的参数数量值大于或等于“ 1 ”时，表示有多个阴影值，反之调用默认的参数值“ 0 0 4px rgba(0,0,0,.3) ”。
注：复杂的混合宏中的逻辑关系（@if...@else）后面小节会有讲解。

#### 混合宏-调用混合宏
在 Sass 中通过 @mixin 关键词声明了一个混合宏，那么在实际调用中，其匹配了一个关键词“@include”来调用声明好的混合宏。例如在你的样式中定义了一个圆角的混合宏“border-radius”:

```
@mixin border-radius{
    -webkit-border-radius: 3px;
    border-radius: 3px;
}
```

在一个按钮中要调用定义好的混合宏“border-radius”，可以这样使用：

```
button {
    @include border-radius;
}
```

这个时候编译出来的 CSS:

```
button {
  -webkit-border-radius: 3px;
  border-radius: 3px;
}
```
#### 混合宏的参数--传一个不带值的参数
Sass 的混合宏有一个强大的功能，可以传参，那么在 Sass 中传参主要有以下几种情形：
##### A) 传一个不带值的参数
在混合宏中，可以传一个不带任何值的参数，比如：

```
@mixin border-radius($radius){
  -webkit-border-radius: $radius;
  border-radius: $radius;
}
```

在混合宏“border-radius”中定义了一个不带任何值的参数“$radius”。
在调用的时候可以给这个混合宏传一个参数值：

```
.box {
  @include border-radius(3px);
}
```

这里表示给混合宏传递了一个“border-radius”的值为“3px”。
编译出来的 CSS:

```
.box {
  -webkit-border-radius: 3px;
  border-radius: 3px;
}
```

#### 混合宏的参数--传一个带值的参数
在 Sass 的混合宏中，还可以给混合宏的参数传一个默认值，例如：

```
@mixin border-radius($radius:3px){
  -webkit-border-radius: $radius;
  border-radius: $radius;
}
```

在混合宏“border-radius”传了一个参数“$radius”，而且给这个参数赋予了一个默认值“3px”。
在调用类似这样的混合宏时，会多有一个机会，假设你的页面中的圆角很多地方都是“3px”的圆角，那么这个时候只需要调用默认的混合宏“border-radius”:

```
.btn {
  @include border-radius;
}
```

编译出来的 CSS:

```
.btn {
  -webkit-border-radius: 3px;
  border-radius: 3px;
}
```

但有的时候，页面中有些元素的圆角值不一样，那么可以随机给混合宏传值，如：

```
.box {
  @include border-radius(50%);
}
```

编译出来的 CSS:

```
.box {
  -webkit-border-radius: 50%;
  border-radius: 50%;
}
```
#### 混合宏的参数--传多个参数
Sass 混合宏除了能传一个参数之外，还可以传多个参数，如：

```
@mixin center($width,$height){
  width: $width;
  height: $height;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -($height) / 2;
  margin-left: -($width) / 2;
}
```

在混合宏“center”就传了多个参数。在实际调用和其调用其他混合宏是一样的：

```
.box-center {
  @include center(500px,300px);
}
```

编译出来 CSS:

```
.box-center {
  width: 500px;
  height: 300px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -150px;
  margin-left: -250px;
}
```

  有一个特别的参数“…”。当混合宏传的参数过多之时，可以使用参数来替代，如：

```
@mixin box-shadow($shadows...){
  @if length($shadows) >= 1 {
    -webkit-box-shadow: $shadows;
    box-shadow: $shadows;
  } @else {
    $shadows: 0 0 2px rgba(#000,.25);
    -webkit-box-shadow: $shadow;
    box-shadow: $shadow;
  }
}
```

在实际调用中：

```
.box {
  @include box-shadow(0 0 1px rgba(#000,.5),0 0 2px rgba(#000,.2));
}
```

编译出来的CSS:

```
.box {
  -webkit-box-shadow: 0 0 1px rgba(0, 0, 0, 0.5), 0 0 2px rgba(0, 0, 0, 0.2);
  box-shadow: 0 0 1px rgba(0, 0, 0, 0.5), 0 0 2px rgba(0, 0, 0, 0.2);
}
```
#### 混合宏的参数--混合宏的不足
混合宏在实际编码中给我们带来很多方便之处，特别是对于复用重复代码块。但其最大的不足之处是会生成冗余的代码块。比如在不同的地方调用一个相同的混合宏时。如：

```
@mixin border-radius{
  -webkit-border-radius: 3px;
  border-radius: 3px;
}

.box {
  @include border-radius;
  margin-bottom: 5px;
}

.btn {
  @include border-radius;
}
```

示例在“.box”和“.btn”中都调用了定义好的“border-radius”混合宏。先来看编译出来的 CSS：

```
.box {
  -webkit-border-radius: 3px;
  border-radius: 3px;
  margin-bottom: 5px;
}

.btn {
  -webkit-border-radius: 3px;
  border-radius: 3px;
}
```

上例明显可以看出，Sass 在调用相同的混合宏时，并不能智能的将相同的样式代码块合并在一起。这也是 Sass 的混合宏最不足之处。
 
###  扩展/继承
继承对于了解 CSS 的同学来说一点都不陌生，先来看一张图：

图中代码显示“.col-sub .block li,.col-extra .block li” 继承了 “.item-list ul li”选择器的 “padding : 0;” 和 “ul li” 选择器中的 “list-style : none outside none;”以及 * 选择器中的 “box-sizing:inherit;”。
在 Sass 中也具有继承一说，也是继承类中的样式代码块。在 Sass 中是通过关键词 “@extend”来继承已存在的类样式块，从而实现代码的继承。如下所示：

```
//SCSS
.btn {
  border: 1px solid #ccc;
  padding: 6px 10px;
  font-size: 14px;
}

.btn-primary {
  background-color: #f36;
  color: #fff;
  @extend .btn;
}

.btn-second {
  background-color: orange;
  color: #fff;
  @extend .btn;
}
```

编译出来之后：

```
//CSS
.btn, .btn-primary, .btn-second {
  border: 1px solid #ccc;
  padding: 6px 10px;
  font-size: 14px;
}

.btn-primary {
  background-color: #f36;
  color: #fff;
}

.btn-second {
  background-clor: orange;
  color: #fff;
}
```

从示例代码可以看出，在 Sass 中的继承，可以继承类样式块中所有样式代码，而且编译出来的 CSS 会将选择器合并在一起，形成组合选择器：

```
.btn, .btn-primary, .btn-second {
  border: 1px solid #ccc;
  padding: 6px 10px;
  font-size: 14px;
}
```
### 占位符 %placeholder
Sass 中的占位符 %placeholder 功能是一个很强大，很实用的一个功能，这也是我非常喜欢的功能。他可以取代以前 CSS 中的基类造成的代码冗余的情形。因为 %placeholder 声明的代码，如果不被 @extend 调用的话，不会产生任何代码。来看一个演示：

```
%mt5 {
  margin-top: 5px;
}
%pt5{
  padding-top: 5px;
}
```

这段代码没有被 @extend 调用，他并没有产生任何代码块，只是静静的躺在你的某个 SCSS 文件中。只有通过 @extend 调用才会产生代码：

```
//SCSS
%mt5 {
  margin-top: 5px;
}
%pt5{
  padding-top: 5px;
}

.btn {
  @extend %mt5;
  @extend %pt5;
}

.block {
  @extend %mt5;

  span {
    @extend %pt5;
  }
}
```

编译出来的CSS

```
//CSS
.btn, .block {
  margin-top: 5px;
}

.btn, .block span {
  padding-top: 5px;
}
```

从编译出来的 CSS 代码可以看出，通过 @extend 调用的占位符，编译出来的代码会将相同的代码合并在一起。这也是我们希望看到的效果，也让你的代码变得更为干净。

### 混合宏 VS 继承 VS 占位符
初学者都常常纠结于这个问题“什么时候用混合宏，什么时候用继承，什么时候使用占位符？”其实他们各有各的优点与缺点，先来看看他们使用效果：
#### a) Sass 中的混合宏使用
举例代码见右侧 2-24 行
编译出来的 CSS 见右侧结果窗口。
总结：编译出来的 CSS 清晰告诉了大家，他不会自动合并相同的样式代码，如果在样式文件中调用同一个混合宏，会产生多个对应的样式代码，造成代码的冗余，这也是 CSSer 无法忍受的一件事情。不过他并不是一无事处，他可以传参数。

个人建议：如果你的代码块中涉及到变量，建议使用混合宏来创建相同的代码块。
#### b) Sass 中继承
同样的，将上面代码中的混合宏，使用类名来表示，然后通过继承来调用：
代码见右侧 26-48 行
总结：使用继承后，编译出来的 CSS 会将使用继承的代码块合并到一起，通过组合选择器的方式向大家展现，比如 .mt, .block, .block span, .header, .header span。这样编译出来的代码相对于混合宏来说要干净的多，也是 CSSer 期望看到。但是他不能传变量参数。

个人建议：如果你的代码块不需要专任何变量参数，而且有一个基类已在文件中存在，那么建议使用 Sass 的继承。
#### c) 占位符
最后来看占位符，将上面代码中的基类 .mt 换成 Sass 的占位符格式：
代码见右侧 50-72 行

**总结：**
编译出来的 CSS 代码和使用继承基本上是相同，只是不会在代码中生成占位符 mt 的选择器。那么占位符和继承的主要区别的，“占位符是独立定义，不调用的时候是不会在 CSS 中产生任何代码；继承是首先有一个基类存在，不管调用与不调用，基类的样式都将会出现在编译出来的 CSS 代码中。”
来看一个表格：
![image](http://img.mukewang.com/55263aa30001913307940364.jpg)
### 插值#{}
使用 CSS 预处理器语言的一个主要原因是想使用 Sass 获得一个更好的结构体系。比如说你想写更干净的、高效的和面向对象的 CSS。Sass 中的插值(Interpolation)就是重要的一部分。让我们看一下下面的例子：

```
$properties: (margin, padding);
@mixin set-value($side, $value) {
    @each $prop in $properties {
        #{$prop}-#{$side}: $value;
    }
}
.login-box {
    @include set-value(top, 14px);
}
```

@each...in...语句会在《Sass进级篇》中 1-6 @each循环 中讲解。
它可以让变量和属性工作的很完美，上面的代码编译成 CSS：

```
.login-box {
    margin-top: 14px;
    padding-top: 14px;
}
```

这是 Sass 插值中一个简单的实例。当你想设置属性值的时候你可以使用字符串插入进来。另一个有用的用法是构建一个选择器。可以这样使用：

```
@mixin generate-sizes($class, $small, $medium, $big) {
    .#{$class}-small { font-size: $small; }
    .#{$class}-medium { font-size: $medium; }
    .#{$class}-big { font-size: $big; }
}
@include generate-sizes("header-text", 12px, 20px, 40px);
```

编译出来的 CSS:
.
```
header-text-small { font-size: 12px; }
.header-text-medium { font-size: 20px; }
.header-text-big { font-size: 40px; }
```

一旦你发现这一点，你就会想到超级酷的 mixins，用来生成代码或者生成另一个 mixins。然而，这并不完全是可能的。第一个限制，这可能会很删除用于 Sass 变量的插值。

```
$margin-big: 40px;
$margin-medium: 20px;
$margin-small: 12px;
@mixin set-value($size) {
    margin-top: $margin-#{$size};
}
.login-box {
    @include set-value(big);
}
```

上面的 Sass 代码编译出来，你会得到下面的信息：

```
error style.scss (Line 5: Undefined variable: “$margin-".)
```

所以，#{}语法并不是随处可用，你也不能在 mixin 中调用：

```
@mixin updated-status {
    margin-top: 20px;
    background: #F00;
}
$flag: "status";
.navigation {
    @include updated-#{$flag};
}
```

上面的代码在编译成 CSS 时同样会报错：

```
error style.scss (Line 7: Invalid CSS after "...nclude updated-": expected "}", was "#{$flag};")
```

幸运的是，可以使用 @extend 中使用插值。例如：

```
%updated-status {
    margin-top: 20px;
    background: #F00;
}
.selected-status {
    font-weight: bold;
}
$flag: "status";
.navigation {
    @extend %updated-#{$flag};
    @extend .selected-#{$flag};
}
```


上面的 Sass 代码是可以运行的，因为他给了我们力量，可以动态的插入 .class 和 %placeholder。当然他们不能接受像 mixin 这样的参数，上面的代码编译出来的 CSS:

```
.navigation {
    margin-top: 20px;
    background: #F00;
}
.selected-status, .navigation {
    font-weight: bold;
}
```
### 注释
注释对于一名程序员来说，是极其重要，良好的注释能帮助自己或者别人阅读源码。在 Sass 中注释有两种方式，我暂且将其命名为：
1. 类似 CSS 的注释方式，使用 ”/* ”开头，结属使用 ”*/ ”
1. 类似 JavaScript 的注释方式，使用“//”
两者区别，前者会在编译出来的 CSS 显示，后者在编译出来的 CSS 中不会显示，来看一个示例：

```
//定义一个占位符

%mt5 {
  margin-top: 5px;
}

/*调用一个占位符*/

.box {
  @extend %mt5;
}
```
编译出来的CSS
```
.box {
  margin-top: 5px;
}

/*调用一个占位符*/
```
### 数据类型
 Sass 和 JavaScript 语言类似，也具有自己的数据类型，在 Sass 中包含以下几种数据类型：
1.  数字: 如，1、 2、 13、 10px；
1.  字符串：有引号字符串或无引号字符串，如，"foo"、 'bar'、 baz；
1.  颜色：如，blue、 #04a3f9、 rgba(255,0,0,0.5)；
1.  布尔型：如，true、 false；
1.  空值：如，null；
1.  值列表：用空格或者逗号分开，如，1.5em 1em 0 2em 、 Helvetica, Arial, sans-serif。

SassScript 也支持其他 CSS 属性值（property value），比如 Unicode 范围，或 !important 声明。然而，Sass 不会特殊对待这些属性值，一律视为无引号字符串 (unquoted strings)。
#### 字符串
SassScript 支持 CSS 的两种字符串类型：
1. 有引号字符串 (quoted strings)，如 "Lucida Grande" 、'http://sass-lang.com'；
1. 无引号字符串 (unquoted strings)，如 sans-serifbold。
在编译 CSS 文件时不会改变其类型。只有一种情况例外，使用 #{ }插值语句 (interpolation) 时，有引号字符串将被编译为无引号字符串，这样方便了在混合指令 (mixin) 中引用选择器名。

```
@mixin firefox-message($selector) {
  body.firefox #{$selector}:before {
    content: "Hi, Firefox users!";
  }
}
@include firefox-message(".header");
```

编译为：

```
body.firefox .header:before {
  content: "Hi, Firefox users!"; }
```

需要注意的是：当 deprecated = property syntax 时 （暂时不理解是怎样的情况），所有的字符串都将被编译为无引号字符串，不论是否使用了引号。
#### 值列表
所谓值列表 (lists) 是指 Sass 如何处理 CSS 中： 
margin: 10px 15px 0 0
```

```

或者： 

```
font-face: Helvetica, Arial, sans-serif
```

像上面这样通过空格或者逗号分隔的一系列的值。
事实上，独立的值也被视为值列表——只包含一个值的值列表。

Sass列表函数（Sass list functions）赋予了值列表更多功能（Sass进级会有讲解）：
1. nth函数（nth function） 可以直接访问值列表中的某一项；
1. join函数（join function） 可以将多个值列表连结在一起；
1. append函数（append function） 可以在值列表中添加值； 
1. @each规则（@each rule） 则能够给值列表中的每个项目添加样式。

值列表中可以再包含值列表，比如 1px 2px, 5px 6px 是包含 1px 2px 与 5px 6px 两个值列表的值列表。如果内外两层值列表使用相同的分隔方式，要用圆括号包裹内层，所以也可以写成 (1px 2px) (5px 6px)。当值列表被编译为 CSS 时，Sass 不会添加任何圆括号，因为 CSS 不允许这样做。(1px 2px) (5px 6px)与 1px 2px 5px 6px 在编译后的 CSS 文件中是一样的，但是它们在 Sass 文件中却有不同的意义，前者是包含两个值列表的值列表，而后者是包含四个值的值列表。

可以用 () 表示空的列表，这样不可以直接编译成 CSS，比如编译 font-family: ()时，Sass 将会报错。如果值列表中包含空的值列表或空值，编译时将清除空值，比如 1px 2px () 3px 或 1px 2px null 3px。


### [Sass运算]加法
程序中的运算是常见的一件事情，但在 CSS 中能做运算的，到目前为止仅有 calc() 函数可行。但在 Sass 中，运算只是其基本特性之一。在 Sass 中可以做各种数学计算，在接下来的章节中，主要和大家一起探讨有关于 Sass 中的数学运算。
#### （一）、加法
加法运算是 Sass 中运算中的一种，在变量或属性中都可以做加法运算。如：

```
.box {
  width: 20px + 8in;
}
```

编译出来的 CSS:

```
.box {
  width: 788px;
}
```

但对于携带不同类型的单位时，在 Sass 中计算会报错，如下例所示：

```
.box {
  width: 20px + 1em;
}
```

编译的时候，编译器会报错：“Incompatible units: 'em' and ‘px'.”
in mm cm  pt pc px等绝对单位都能运算<br>
ex em rem等相对当前字体的都不能运算
### [Sass运算]减法
Sass 的减法运算和加法运算类似，我们通过一个简单的示例来做阐述：

```
$full-width: 960px;
$sidebar-width: 200px;

.content {
  width: $full-width -  $sidebar-width;
}
```

编译出来的 CSS 如下：

```
.content {
  width: 760px;
}
```

同样的，运算时碰到不同类型的单位时，编译也会报错，如：

```
$full-width: 960px;

.content {
  width: $full-width -  1em;
}
```

编译的时候，编译器报“Incompatible units: 'em' and ‘px’.”错误。

### [Sass运算]乘法
Sass 中的乘法运算和前面介绍的加法与减法运算还略有不同。虽然他也能够支持多种单位（比如 em ,px , %），但当一个单位同时声明两个值时会有问题。比如下面的示例：

```
.box {
  width:10px * 2px;  
}
```

编译的时候报“20px*px isn't a valid CSS value.”错误信息。
如果进行乘法运算时，两个值单位相同时，只需要为一个数值提供单位即可。上面的示例可以修改成：

```
.box {
  width: 10px * 2;
}
```

编译出来的 CSS:

```
.box {
  width: 20px;
}
```

Sass 的乘法运算和加法、减法运算一样，在运算中有不同类型的单位时，也将会报错。如下面的示例：

```
.box {
  width: 20px * 2em;
}
```

编译时报“40em*px isn't a valid CSS value.”错误信息。

### [Sass运算]除法
Sass 的乘法运算规则也适用于除法运算。不过除法运算还有一个特殊之处。众所周知“/”符号在 CSS 中已做为一种符号使用。因此在 Sass 中做除法运算时，直接使用“/”符号做为除号时，将不会生效，编译时既得不到我们需要的效果，也不会报错。一起先来看一个简单的示例：

```
.box {
  width: 100px / 2;  
}
```

编译出来的 CSS 如下：

```
.box {
  width: 100px / 2;
}
```

这样的结果对于大家来说没有任何意义。要修正这个问题，只需要给运算的外面添加一个小括号( )即可：

```
.box {
  width: (100px / 2);  
}
```

编译出来的 CSS 如下：

```
.box {
  width: 50px;
}
```

除了上面情况带有小括号，“/”符号会当作除法运算符之外，如果“/”符号在已有的数学表达式中时，也会被认作除法符号。如下面示例：

```
.box {
  width: 100px / 2 + 2in;  
}
```

编译出来的CSS：

```
.box {
  width: 242px;
}
```

另外，在 Sass 除法运算中，当用变量进行除法运算时，“/”符号也会自动被识别成除法，如下例所示：

```
$width: 1000px;
$nums: 10;

.item {
  width: $width / 10;  
}

.list {
  width: $width / $nums;
}
```

编译出来的CSS:

```
.item {
  width: 100px;
}

.list {
  width: 100px;
}
```

综合上述，”/  ”符号被当作除法运算符时有以下几种情况：
1. •    如果数值或它的任意部分是存储在一个变量中或是函数的返回值。
1. •    如果数值被圆括号包围。
1. •    如果数值是另一个数学表达式的一部分。
如下所示：

```
//SCSS
p {
  font: 10px/8px;             // 纯 CSS，不是除法运算
  $width: 1000px;
  width: $width/2;            // 使用了变量，是除法运算
  width: round(1.5)/2;        // 使用了函数，是除法运算
  height: (500px/2);          // 使用了圆括号，是除法运算
  margin-left: 5px + 8px/2px; // 使用了加（+）号，是除法运算
}
```

编译出来的CSS

```
p {
  font: 10px/8px;
  width: 500px;
  height: 250px;
  margin-left: 9px;
 }
```


Sass 的除法运算还有一个情况。我们先回忆一下，在乘法运算时，如果两个值带有相同单位时，做乘法运算时，出来的结果并不是我们需要的结果。但在除法运算时，如果两个值带有相同的单位值时，除法运算之后会得到一个不带单位的数值。如下所示：

```
.box {
  width: (1000px / 100px);
}
```

编译出来的CSS如下：

```
.box {
  width: 10;
}
```
### [Sass运算]变量计算
在 Sass 中除了可以使用数值进行运算之外，还可以使用变量进行计算，其实在前面章节的示例中也或多或少的向大家展示了。在 Sass 中使用变量进行计算，这使得 Sass 的数学运算功能变得更加实用。一起来看一个简单的示例：

```
$content-width: 720px;
$sidebar-width: 220px;
$gutter: 20px;

.container {
  width: $content-width + $sidebar-width + $gutter;
  margin: 0 auto;
}
```

编译出来的CSS

```
.container {
  width: 960px;
  margin: 0 auto;
}
```
### [Sass运算]数字运算
在 Sass 运算中数字运算是较为常见的，数字运算包括前面介绍的：加法、减法、乘法和除法等运算。而且还可以通过括号来修改他们的运算先后顺序。和我们数学运算是一样的，一起来看个示例。

```
.box {
  width: ((220px + 720px) - 11 * 20 ) / 12 ;  
}
```

编译出来的 CSS:

```
.box {
  width: 60px;
}
```

上面这个简单示例是一个典型的计算 Grid 单列列宽的运算。
### [Sass运算]颜色运算
所有算数运算都支持颜色值，并且是分段运算的。也就是说，红、绿和蓝各颜色分段单独进行运算。如：

```
p {
  color: #010203 + #040506;
}
```

计算公式为 01 + 04 = 05、02 + 05 = 07 和 03 + 06 = 09， 并且被合成为：
如此编译出来的 CSS 为：

```
p {
  color: #050709;
}
```

算数运算也能将数字和颜色值 一起运算，同样也是分段运算的。如：

```
p {
  color: #010203 * 2;
}
```

计算公式为 01 * 2 = 02、02 * 2 = 04 和 03 * 2 = 06， 并且被合成为：

```
p {
  color: #020406;
}
```
### [Sass运算]字符运算
在 Sass 中可以通过加法符号“+”来对字符串进行连接。例如：

```
$content: "Hello" + "" + "Sass!";
.box:before {
  content: " #{$content} ";
}
```

编译出来的CSS：
```
.box:before {
  content: " Hello Sass! ";
}
```
除了在变量中做字符连接运算之外，还可以直接通过 +，把字符连接在一起：
```
div {
  cursor: e + -resize;
}
编译出来的CSS:
div {
  cursor: e-resize;
}
```
注意，如果有引号的字符串被添加了一个没有引号的字符串 （也就是，带引号的字符串在 + 符号左侧）， 结果会是一个有引号的字符串。 同样的，如果一个没有引号的字符串被添加了一个有引号的字符串 （没有引号的字符串在 + 符号左侧）， 结果将是一个没有引号的字符串。 例如：
```
p:before {
  content: "Foo " + Bar;
  font-family: sans- + "serif";
}
```
编译出来的 CSS：
```
p:before {
  content: "Foo Bar";
  font-family: sans-serif; }
  ```
##   SASS指令
### @if
@if 指令是一个 SassScript，它可以根据条件来处理样式块，如果条件为 true 返回一个样式块，反之 false 返回另一个样式块。在 Sass 中除了 @if 之，还可以配合 @else if 和 @else 一起使用。
假设要控制一个元素隐藏或显示，我们就可以定义一个混合宏，通过 @if...@else... 来判断传进参数的值来控制 display 的值。如下所示：

```
//SCSS
@mixin blockOrHidden($boolean:true) {
  @if $boolean {
      @debug "$boolean is #{$boolean}";
      display: block;
    }
  @else {
      @debug "$boolean is #{$boolean}";
      display: none;
    }
}

.block {
  @include blockOrHidden;
}

.hidden{
  @include blockOrHidden(false);
}
```

编译出来的CSS:

```
.block {
  display: block;
}

.hidden {
  display: none;
}
```
#### @for循环（上）
在制作网格系统的时候，大家应该对 .col1~.col12 这样的印象较深。在 CSS 中你需要一个一个去书写，但在 Sass 中，可以使用 @for 循环来完成。在 Sass 的 @for 循环中有两种方式：

```
@for $i from <start> through <end>
@for $i from <start> to <end>
```

- $i 表示变量
- start 表示起始值
- end 表示结束值
这两个的区别是关键字 through 表示包括 end 这个数，而 to 则不包括 end 这个数。
如下代码，先来个使用 through 关键字的例子：

```
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}
```

编译出来的 CSS:

```
.item-1 {
  width: 2em;
}

.item-2 {
  width: 4em;
}

.item-3 {
  width: 6em;
}
```

再来个 to 关键字的例子：
@for $i from 1 to 3 {
  .item-#{$i} { width: 2em * $i; }
}
编译出来的 CSS:

```
.item-1 {
  width: 2em;
}

.item-2 {
  width: 4em;
}
```

#### @for循环 （下）
上一小节的那个实例几乎用不着，哈哈，所以其实是没什么营养的东西，只是帮助理解了原来 @for 是这么回事。怎么的也不能就这么忽悠大家啊，大家好不容易抽空看下文章，就这么点扯淡的东西怎么对得住呢。下面再来个营养级别的，@for应用在网格系统生成各个格子 class 的代码：

```
//SCSS 
$grid-prefix: span !default;
$grid-width: 60px !default;
$grid-gutter: 20px !default;

%grid {
  float: left;
  margin-left: $grid-gutter / 2;
  margin-right: $grid-gutter / 2;
}
@for $i from 1 through 12 {
  .#{$grid-prefix}#{$i}{
    width: $grid-width * $i + $grid-gutter * ($i - 1);
    @extend %grid;
  }  
}
```

编译出来的 CSS:

```
.span1, .span2, .span3, .span4, .span5, .span6, .span7, .span8, .span9, .span10, .span11, .span12 {
  float: left;
  margin-left: 10px;
  margin-right: 10px;
}

.span1 {
  width: 60px;
}

.span2 {
  width: 140px;
}

.span3 {
  width: 220px;
}

.span4 {
  width: 300px;
}

.span5 {
  width: 380px;
}

.span6 {
  width: 460px;
}

.span7 {
  width: 540px;
}

.span8 {
  width: 620px;
}

.span9 {
  width: 700px;
}

.span10 {
  width: 780px;
}

.span11 {
  width: 860px;
}

.span12 {
  width: 940px;
}
```

将上面的示例稍做修改，将 @for through 方式换成 @for to:：

```
//SCSS
@for $i from 1 to 13 {
  .#{$grid-prefix}#{$i}{
    width: $grid-width * $i + $grid-gutter * ($i - 1);
    @extend %grid;
  }  
}
```

其最终编译出来的 CSS 代码和上例所编译出来的一模一样。
这两段 Sass 代码并无太多差别，只是 @for中的 <end> 取值不同。配合 through 的 <end> 值是 12，其遍历出来的终点值也是 12，和 <end> 值一样。配合 to 的 <end> 值是 13，其遍历出来的终点值是 12，就是 <end> 对就的值减去 1 。

#### @while循环
@while 指令也需要 SassScript 表达式（像其他指令一样），并且会生成不同的样式块，直到表达式值为 false 时停止循环。这个和 @for 指令很相似，只要 @while 后面的条件为 true 就会执行。
这里有一个 @while 指令的简单用例：

```
//SCSS
$types: 4;
$type-width: 20px;

@while $types > 0 {
    .while-#{$types} {
        width: $type-width + $types;
    }
    $types: $types - 1;
}
```
编译出来的 CSS
```
.while-4 {
  width: 24px;
}

.while-3 {
  width: 23px;
}

.while-2 {
  width: 22px;
}

.while-1 {
  width: 21px;
}
```

#### @each循环
@each 循环就是去遍历一个列表，然后从列表中取出对应的值。
@each 循环指令的形式：

```
@each $var in <list>
```

如果你没有接触过列表，也不要紧，他也非常简单。
在下面的例子中你可以看到，$var 就是一个变量名，<list> 是一个 SassScript 表达式，他将返回一个列表值。变量 $var 会在列表中做遍历，并且遍历出与 $var 对应的样式块。
这有一个 @each 指令的简单示例：

```
$list: adam john wynn mason kuroir;//$list
```
 就是一个列表


```
@mixin author-images {
    @each $author in $list {
        .photo-#{$author} {
            background: url("/images/avatars/#{$author}.png") no-repeat;
        }
    }
}

.author-bio {
    @include author-images;
}
```

编译出 CSS:
.
```
author-bio .photo-adam {
  background: url("/images/avatars/adam.png") no-repeat; }
.author-bio .photo-john {
  background: url("/images/avatars/john.png") no-repeat; }
.author-bio .photo-wynn {
  background: url("/images/avatars/wynn.png") no-repeat; }
.author-bio .photo-mason {
  background: url("/images/avatars/mason.png") no-repeat; }
.author-bio .photo-kuroir {
  background: url("/images/avatars/kuroir.png") no-repeat; }
```
## SASS函数
### Sass的函数简介
在 Sass 中除了可以定义变量，具有 @extend、%placeholder 和 mixins 等特性之外，还自备了一系列的函数功能。其主要包括：

- 字符串函数
- 数字函数
- 列表函数
- 颜色函数
- Introspection 函数
- 三元函数等
- 
当然除了自备的函数功能之外，我们还可以根据自己的需求定义函数功能，常常称之为自定义函数。
#### 字符串函数-unquote()函数
字符串函数顾名思意是用来处理字符串的函数。Sass 的字符串函数主要包括两个函数：

      
```
unquote($string)：删除字符串中的引号；
      quote($string)：给字符串添加引号。
```

1、unquote()函数

unquote() 函数主要是用来删除一个字符串中的引号，如果这个字符串没有带有引号，将返回原始的字符串。简单的使用终端来测试这个函数的运行结果：

```
//SCSS
.test1 {
    content:  unquote('Hello Sass!') ;
}
.test2 {
    content: unquote("'Hello Sass!");
}
.test3 {
    content: unquote("I'm Web Designer");
}
.test4 {
    content: unquote("'Hello Sass!'");
}
.test5 {
    content: unquote('"Hello Sass!"');
}
.test6 {
    content: unquote(Hello Sass);
}
```

编译后的 css 代码：

```
//CSS
.test1 {
  content: Hello Sass!; }

.test2 {
  content: 'Hello Sass!; }

.test3 {
  content: I'm Web Designer; }

.test4 {
  content: 'Hello Sass!'; }

.test5 {
  content: "Hello Sass!"; }

.test6 {
  content: Hello Sass; }
```

注意：从测试的效果中可以看出，unquote( ) 函数只能删除字符串最前和最后的引号（双引号或单引号），而无法删除字符串中间的引号。如果字符没有带引号，返回的将是字符串本身。

#### 字符串函数-quote()函数
quote() 函数刚好与 unquote() 函数功能相反，主要用来给字符串添加引号。如果字符串，自身带有引号会统一换成双引号 ""。如：


```
//SCSS
.test1 {
    content:  quote('Hello Sass!');
}
.test2 {
    content: quote("Hello Sass!");
}
.test3 {
    content: quote(ImWebDesigner);
}
.test4 {
    content: quote(' ');
}
```

编译出来的 css 代码：


```
//CSS
.test1 {
  content: "Hello Sass!";
}
.test2 {
  content: "Hello Sass!";
}
.test3 {
  content: "ImWebDesigner";
}
.test4 {
  content: "";
}
```

使用 quote() 函数只能给字符串增加双引号，而且字符串中间有单引号或者空格时，需要用单引号或双引号括起，否则编译的时候将会报错。


```
.test1 {
    content:  quote(Hello Sass);
}
这样使用，编译器马上会报错：

error style.scss (Line 13: $string: ("Hello""Sass") is not a string for `quote')
```

解决方案就是去掉空格，或者加上引号：


```
.test1 {
    content:  quote(HelloSass);
}
.test1 {
    content:  quote("Hello Sass");
}
```

同时 quote() 碰到特殊符号，比如： !、?、> 等，除中折号 - 和 下划线_ 都需要使用双引号括起，否则编译器在进行编译的时候同样会报错：


```
error style.scss (Line 13: Invalid CSS after "...quote(HelloSass": expected ")", was "!);")
error style.scss (Line 16: Invalid CSS after "...t:  quote(Hello": expected ")", was “?);")
```
#### 字符串函数-To-upper-case()、To-lower-case()
##### 1、To-upper-case()

To-upper-case() 函数将字符串小写字母转换成大写字母。如：


```
//SCSS
.test {
  text: to-upper-case(aaaaa);
  text: to-upper-case(aA-aAAA-aaa);
}
```

编译出来的 css 代码：


```
//CSS
.test {
  text: AAAAA;
  text: AA-AAAA-AAA;
}
```

##### 2、To-lower-case()

To-lower-case() 函数 与 To-upper-case() 刚好相反，将字符串转换成小写字母：


```
//SCSS
.test {
  text: to-lower-case(AAAAA);
  text: to-lower-case(aA-aAAA-aaa);
}
```

编译出来的 css 代码：


```
//CSS
.test {
  text: aaaaa;
  text: aa-aaaa-aaa;
}
```
### 数字函数简介
Sass 中的数字函数提要针对数字方面提供一系列的函数功能：

-       percentage($value)：将一个不带单位的数转换成百分比值；
-       round($value)：将数值四舍五入，转换成一个最接近的整数；
-       ceil($value)：将大于自己的小数转换成下一位整数；
-       floor($value)：将一个数去除他的小数部分；
-       abs($value)：返回一个数的绝对值；
-       min($numbers…)：找出几个数值之间的最小值；
-       max($numbers…)：找出几个数值之间的最大值；
-       random(): 获取随机数
看到上面函数的简介，对于熟悉Javascript 同学而言并不会感觉陌生。因为他们有很多功能都非常类似，接下来对每个函数进行一些简单的测试 。

#### 数字函数-percentage()
1、percentage()

percentage()函数主要是将一个不带单位的数字转换成百分比形式：


```
>> percentage(.2)
20%
>> percentage(2px / 10px)
20%
>> percentage(2em / 10em)
20%
>>
 

.footer{
    width : percentage(.2)
}
```

编译后的 css 代码：

```
.footer{
    width : 20%
}
```

如果您转换的值是一个带有单位的值，那么在编译的时候会报错误信息：


```
>> percentage(2px / 10em)
SyntaxError: $value: 0.2px/em is not a unitless number for `percentage'
```
#### 数字函数-round()函数
round() 函数可以将一个数四舍五入为一个最接近的整数：


```
>> round(12.3)
12
>> round(12.5)
13
>> round(1.49999)
1
>> round(2.0)
2
>> round(20%)
20%
>> round(2.2%)
2%
>> round(3.9em)
4em
>> round(2.3px)
2px
>> round(2px / 3px)
1
>> round(1px / 3px)
0
>> round(3px / 2em)
2px/em
 

.footer {
   width:round(12.3px)
}
```


```
编译后的 css 代码：

.footer {
  width: 12px;
}
```


在round() 函数中可以携带单位的任何数值。
#### 数字函数-ceil()函数
ceil() 函数将一个数转换成最接近于自己的整数，会将一个大于自身的任何小数转换成大于本身 1 的整数。也就是只做入，不做舍的计算：

```
>> ceil(2.0)
2
>> ceil(2.1)
3
>> ceil(2.6)
3
>> ceil(2.3%)
3%
>> ceil(2.3px)
3px
>> ceil(2.5px)
3px
>> ceil(2px / 3px)
1
>> ceil(2% / 3px)
1%/px
>> ceil(1em / 5px)
1em/px
 

.footer {
   width:ceil(12.3px);
}
```

编译后的 css 代码：

```
.footer {
  width: 13px;
}
```
#### 数字函数-floor()函数
floor() 函数刚好与 ceil() 函数功能相反，其主要将一个数去除其小数部分，并且不做任何的进位。也就是只做舍，不做入的计算：


```
>> floor(2.1)
2
>> floor(2.5)
2
>> floor(3.5%)
3%
>> floor(10.2px)
10px
>> floor(10.8em)
10em
>> floor(2px / 10px)
0
>> floor(3px / 1em)
3px/em
 

.footer {
   width:floor(12.3px);
}
```

编译后的 css 代码：


```
.footer {
  width: 12px;
}
```
#### 数字函数-abs()函数
abs( ) 函数会返回一个数的绝对值。


```
>> abs(10)
10
>> abs(-10)
10
>> abs(-10px)
10px
>> abs(-2em)
2em
>> abs(-.5%)
0.5%
>> abs(-1px / 2px)
0.5
 

.footer {
   width:abs(-12.3px);
}
```

编译后的 css 代码：


```
.footer {
  width: 12.3px;
}
```
#### 数字函数-min()函数、max()函数
##### min()函数

min() 函数功能主要是在多个数之中找到最小的一个，这个函数可以设置任意多个参数：


```
>> min(1,2,1%,3,300%)
1%
>> min(1px,2,3px)
1px
>> min(1em,2em,6em)
1em
```

不过在 min() 函数中同时出现两种不同类型的单位，将会报错误信息：


```
>> min(1px,1em)
SyntaxError: Incompatible units: 'em' and 'px'.
```

#### max()函数

max() 函数和 min() 函数一样，不同的是，max() 函数用来获取一系列数中的最大那个值：


```
>> max(1,5)
5
>> max(1px,5px)
5px
```

同样的，如果在 max() 函数中有不同单位，将会报错：

```
>> max(1,3px,5%,6)
SyntaxError: Incompatible units: '%' and ‘px'.
```
#### 数字函数-random()函数
random() 函数是用来获取一个随机数：


```
>> random()
0.03886
>> random()
0.66527
>> random()
0.8125
>> random()
0.26839
>> random()
0.85063
```

### 列表函数简介
列表函数主要包括一些对列表参数的函数使用，主要包括以下几种：

-       length($list)：返回一个列表的长度值；
-       nth($list, $n)：返回一个列表中指定的某个标签值
-       join($list1, $list2, [$separator])：将两个列给连接在一起，变成一个列表；
-       append($list1, $val, [$separator])：将某个值放在列表的最后；
-       zip($lists…)：将几个列表结合成一个多维的列表；
-       index($list, $value)：返回一个值在列表中的位置值。

列表函数中的每个函数都有其独特的作用与功能，接下来我们通过命令终端向大家展示每个列表函数的功能与使用。
#### length()函数
length() 函数主要用来返回一个列表中有几个值，简单点说就是返回列表清单中有多少个值：

```
>> length(10px)
1
>> length(10px 20px (border 1px solid) 2em)
4
>> length(border 1px solid)
3
```
length() 函数中的列表参数之间使用空格隔开，不能使用逗号，否则函数将会出错：

```
>> length(10px,20px,(border 1px solid),2em)
SyntaxError: wrong number of arguments (4 for 1) for `length'
>> length(1,2px)
SyntaxError: wrong number of arguments (2 for 1) for `length'
```
#### nth()函数
语法:

```
nth($list,$n)
```

nth() 函数用来指定列表中某个位置的值。不过在 Sass 中，nth() 函数和其他语言不同，1 是指列表中的第一个标签值，2 是指列给中的第二个标签值，依此类推。如：

```
>> nth(10px 20px 30px,1)
10px
>> nth((Helvetica,Arial,sans-serif),2)
"Arial"
>> nth((1px solid red) border-top green,1)
(1px "solid" #ff0000)
```

注：在 nth($list,$n) 函数中的 $n 必须是大于 0 的整数：

```
>> nth((1px solid red) border-top green 1 ,0)
SyntaxError: List index 0 must be a non-zero integer for `nth'
```
#### join()函数
join() 函数是将两个列表连接合并成一个列表。

```
>> join(10px 20px, 30px 40px)
(10px 20px 30px 40px)
>> join((blue,red),(#abc,#def))
(#0000ff, #ff0000, #aabbcc, #ddeeff)
>> join((blue,red),(#abc #def))
(#0000ff, #ff0000, #aabbcc, #ddeeff)
```

不过 join() 只能将两个列表连接成一个列表，如果直接连接两个以上的列表将会报错：

```
>> join((blue red),(#abc, #def),(#dee #eff))
SyntaxError: $separator: (#ddeeee #eeffff) is not a string for `join'
```

但很多时候不只碰到两个列表连接成一个列表，这个时候就需要将多个 join() 函数合并在一起使用：

```
>> join((blue red), join((#abc #def),(#dee #eff)))
(#0000ff #ff0000 #aabbcc #ddeeff #ddeeee #eeffff)
```

在 join() 函数中还有一个很特别的参数 $separator，这个参数主要是用来给列表函数连接列表值是，使用的分隔符号，默认值为 auto。

join() 函数中 $separator 除了默认值 auto 之外，还有 comma 和 space 两个值，其中 comma 值指定列表中的列表项值之间使用逗号（,）分隔，space 值指定列表中的列表项值之间使用空格（ ）分隔。

在 join() 函数中除非明确指定了 $separator值，否则将会有多种情形发生：

如果列表中的第一个列表中每个值之间使用的是逗号（,），那么 join() 函数合并的列表中每个列表项之间使用逗号,分隔：

```
>> join((blue, red, #eff),(green orange))
(#0000ff, #ff0000, #eeffff, #008000, #ffa500)
```
但当第一个列表中只有一个列表项，那么 join() 函数合并的列表项目中每个列表项目这间使用的分隔符号会根据第二个列表项中使用的，如果第二列表项中使用是,分隔，则使用逗号分隔；如果第二列项之间使用的空格符，则使用空格分隔：


```
>> join(blue,(green, orange))
(#0000ff, #008000, #ffa500)
>> join(blue,(green orange))
(#0000ff #008000 #ffa500)
```

如果列表中的第一个列表中每个值之间使用的是空格，那么 join() 函数合并的列表中每个列表项之间使用空格分隔：


```
>> join((blue green),(red,orange))
(#0000ff #008000 #ff0000 #ffa500)
>> join((blue green),(red orange))
(#0000ff #008000 #ff0000 #ffa500)
```

如果当两个列表中的列表项小于1时，将会以空格分隔：


```
>> join(blue,red)
(#0000ff #ff0000)
```

如此一来，会有多种情形发生，造成使用混乱的情形，如果你无法记得，什么时候会是用逗号分隔合并的列表项，什么时候是使用空格分隔合并 的列表项，在些建议大家使用 join() 函数合并列表项的时候就明确指定 $separator 参数，用来指定合并的列表中使用什么方式来分隔列表项：


```
>> join(blue,red,comma)
(#0000ff, #ff0000)
>> join(blue,red,space)
(#0000ff #ff0000)
>> join((blue green),(red,orange),comma)
(#0000ff, #008000, #ff0000, #ffa500)
>> join((blue green),(red,orange),space)
(#0000ff #008000 #ff0000 #ffa500)
>> join((blue, green),(red,orange),comma)
(#0000ff, #008000, #ff0000, #ffa500)
>> join((blue, green),(red,orange),space)
(#0000ff #008000 #ff0000 #ffa500)
>> join(blue,(red,orange),comma)
(#0000ff, #ff0000, #ffa500)
>> join(blue,(red,orange),space)
(#0000ff #ff0000 #ffa500)
>> join(blue,(red orange),comma)
(#0000ff, #ff0000, #ffa500)
>> join(blue,(red orange),space)
(#0000ff #ff0000 #ffa500)
```
#### append()函数
append() 函数是用来将某个值插入到列表中，并且处于最末位。


```
>> append(10px 20px ,30px)
(10px 20px 30px)
>> append((10px,20px),30px)
(10px, 20px, 30px)
>> append(green,red)
(#008000 #ff0000)
>> append(red,(green,blue))
(#ff0000 (#008000, #0000ff))
```

如果没有明确的指定 $separator 参数值，其默认值是 auto。

如果列表只有一个列表项时，那么插入进来的值将和原来的值会以空格的方式分隔。
如果列表中列表项是以空格分隔列表项，那么插入进来的列表项也将以空格分隔；
如果列表中列表项是以逗号分隔列表项，那么插入进来的列表项也将以逗号分隔。
当然，在 append() 函数中，可以显示的设置 $separator 参数，

如果取值为 comma 将会以逗号分隔列表项
如果取值为 space 将会以空格分隔列表项

```
>> append((blue green),red,comma)
(#0000ff, #008000, #ff0000)
>> append((blue green),red,space)
(#0000ff #008000 #ff0000)
>> append((blue, green),red,comma)
(#0000ff, #008000, #ff0000)
>> append((blue, green),red,space)
(#0000ff #008000 #ff0000)
>> append(blue,red,comma)
(#0000ff, #ff0000)
>> append(blue,red,space)
(#0000ff #ff0000)
```

 
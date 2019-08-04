---
title: chokidar API
tags: docs, npm
---
github地址：https://github.com/paulmillr/chokidar

# chokidar API

## chokidar.watch(paths, [options])** 

返回一个chokidar构造监听实例

### 参数：
#### paths
一个字符串或者是一个数组，描述监听的文件或者文件夹的路径
#### 配置对象数据类型
常用配置项：
- **persistent:bollean**,与原生fs.watch一样,表示是否保护进程不退出持久监听，默认值为true
- **ignored:string**,所要忽略监听的文件或者文件夹
- **ignoreInitial:bollean**,表示是否**忽略**对增加文件或者增加文件夹的时候进行发送事件，默认值为false表示add/addDir会触发事件
- **cwd:string**类型，没有默认值，类似于appBasepath，监听的paths所相对的路径。
- **usePolling:bollean**，表示是否使用前面提到的fs.watchFile()进行轮询操作，由于轮询会导致cpu飙升，所以此选项通常在需要通过网络监视文件的时候才设置为true即使用fs.watchFile()，默认值为false
- **depth:number**类型,没有默认值，如果设定则表示限定了会递归监听多少个子目录。

### 返回监听实例 FSWatcher API
#### on(eventName,(path, event) => {})

#### .add(path / paths):

添加文件，目录或glob模式以进行跟踪。
支持字符串数组或单独字符串路径

#### .on(event, callback): 
监听支持的事件

**支持的事件名eventName**
- add	新增文件时触发
- addDir	新增文件夹的时候触发
- unlink	对应的文件的删除
- unlinkDir	对应的文件夹的删除
- change	文件内容改变时触发
- all 指代以上所有事件（除了ready, raw, and error之外所有的事件类型）
- ready
- raw
- error 捕获error

**callback (path, event) => {}**
path 指代监听到的文件/文件夹路径

#### .unwatch(path / paths): 

停止监听传入文件/文件夹

#### .close():

从监视文件中移除/关闭所有侦听器

#### .getWatched(): 

返回此FSWatcher实例正在监视的文件系统上所有路径的对象，
对象的键是所有目录（使用绝对路径，除非使用了cwd选项），并且值是每个目录中包含的项的名称的数组。



## 代码示例


```
const chokidar = require('chokidar')

chokidar.watch('testFolder', {
  persistent: true,
  ignored: /(^|[\/\\])\../, // 忽略点文件
  cwd: '.', // 表示当前目录
  depth:0 // 只监听当前目录不包括子目录
}).on('all', (event, path) => {//监听除了ready, raw, and error之外所有的事件类型
  console.log(event, path);
});

```

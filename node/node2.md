# node中获取正在运行的全部进程数据
问题分析：
本质上，这并不是一个关于 node api 的使用。这个问题解决的关键在于，你需要知道使用你当前系统下的命令行工具，需要运行什么命令可以查询系统的全部进程数据，node 只是提供了一个可以运行这样命令的接口罢了。了解了这一点后，问题就很好解决了。

所以这个问题的第一步是需要知道当前系统该如何查看进程信息，这边系统是 windows ，windows 在命令行中执行 tasklist 可以查看进程信息。

在知道如何查看后，需要结合 node ，我们需要用 node 中的子进程来执行命令，这边使用 exce
详细代码如下：

```js
const ecxe = require('child_process');
exec('tasklist', function(error, stdout, stderr){
    if(error) {
        console.error('error: ' + error);
        return;
    }
    console.log('stdout: ' + stdout);
    console.log('stderr: ' + typeof stderr);
});
```
至于其他系统方法类似，只是命令不同罢了。更详细的进程数据分析需要另外再做处理。
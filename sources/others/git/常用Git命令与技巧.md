
仓库在收到别人的 pr 后可以拉取 pr 上的对应代码来测试审核，其中拉取的命令为：
```
git fetch origin pull/xxx/head:pr
//（xxx == pr 序号，pr == 名字）
```
设置换行符，在遇到总有文件显示修改变化时,,,,
```
git config --global core.autocrlf false
```
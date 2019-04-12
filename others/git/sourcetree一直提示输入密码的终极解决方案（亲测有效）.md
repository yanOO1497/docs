# sourcetree一直提示输入密码的终极解决方案（亲测有效）
如题，最开始使用 sourcetree 的时候，每次拉代码或者是提交代码都会弹出 gihub 的登录窗口，不胜其扰。
网上查询过的方法都不能解决我的问题，后面翻了 sourcetree 的各个菜单项，解决这个问题。其实很简单，步骤如下：

打开工具 —— 选项 —— 验证 —— 添加账户，选择 github 后，点击刷新令牌，在弹出的浏览器页面中填好登录信息，账户添加玩笔后，就不会再每次弹出让你登录的页面了。

![步骤图](https://note.youdao.com/yws/public/resource/957e568d7283ee91059392153cb96480/xmlnote/WEBRESOURCE4d7375fcf8fc60adbbc869f9432cd917/20001)

当然，如果这是你的账户设为默认会更方便。

![](https://note.youdao.com/yws/public/resource/957e568d7283ee91059392153cb96480/xmlnote/WEBRESOURCEd4afc6c4ce6065bcb5fe944607061ea6/20004)

如果以上不能解决你的问题，可以尝试以下方案结合使用：

1. 在选项中设置 git 为系统 git

![](https://note.youdao.com/yws/public/resource/957e568d7283ee91059392153cb96480/xmlnote/WEBRESOURCE16725cc802300b1314f71c791df8eb3e/20006)

2. 
设置你的 ssh key 位置，确保下图圈起来的部分都是填好的。ssh key 生成完记得添加到 git 上。不了解的再自行查询步骤了。
![](https://note.youdao.com/yws/public/resource/957e568d7283ee91059392153cb96480/xmlnote/WEBRESOURCE82265e5e620a746fea246646d4704f97/20008)
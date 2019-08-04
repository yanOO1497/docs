---
title: 你可能不知道的 vscode 使用技巧
tags: tools
---
# 你可能不知道的 vscode 使用技巧

## 关于快捷键部分
1. Ctrl + G（跳转对应行）：打开后再输入数字可以快速跳转到当前打开文件的对应行号（该快捷键等于 Ctrl + P 后输入 : 的效果。）
2. Ctrl + O（跳转符号）： 打开后输入函数名等可以快速定位到对应函数位置（该快捷键等于 Ctrl + P 后输入 @ 的效果。）
3. 按下 “Cmd + Option + 左 / 右方向键”（Windows 上是 Ctrl + Pagedown/Pageup）在编辑器 Tab 之间进行跳转。
4. Ctrl + J:可以快速的显示隐藏底部的工具栏
5. Ctrl + \: 创建出不同的编辑器窗口（并排显示）
6. “Ctrl + -” （Windows 上是 Alt + Left）跳转回上一次光标所在的位置
7. “Ctrl + Shift + -” （Windows 上是 Alt + Right）则可以跳到下一次光标所在的位置
![](https://static001.geekbang.org/resource/image/11/8c/1111c17d45a16da352a5b71f05c6d18c.png)
## 配合鼠标操作的部分
1. 在光标位置，按下 Ctrl 使用鼠标中键来拖出一个框，在这个框中的代码都会背选中，并且每一行都有一个独立的光标；
2. 双击鼠标左键选中单词；三击鼠标左键选中当前行；四击选中整个文档（= Ctrl + A);

## 其他命令
通过运行 “切换禅模式”(Toggle Zen Mode)，就可以把侧边栏、面板等全部隐藏。进入禅模式后，只需按下 Escape 键，即可退出禅模式。

可以通过 debug.toolBarLocation 设置，调整工具栏的位置，比如说 debug.toolBarLocation: docked 就可以将工具栏固定到调试窗口中了。
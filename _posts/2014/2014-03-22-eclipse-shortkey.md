---
layout: post
title: Eclipse快捷键
categories: java
tags: 
- java
- Eclipse
---

>当Eclipse快捷键功能，或者使用菜单时都无效。例如：搜索引用（快捷键Ctrl+Shift+G）无效；
解决方案：转换WorkSpac‍e，或者删除WorkSpace目录下的‍.metadata文件夹，重启Eclipse，重新设置。
Eclipse的编辑功能非常强大，掌握了Eclipse快捷键功能，能够大大提高开发效率。

## 编辑相关的快捷键。

1. 【ALT+/】

此快捷键为用户编辑的好帮手，能为用户提供内容的辅助，不要为记不全方法和属性名称犯愁，当记不全类、方法和属性的名字时，多体验一下【ALT+/】快捷键带来的好处吧

1. 【Ctrl+/】、【Ctrl+Shift+/】

快速添加注释，能为光标所在行或所选定行快速添加注释或取消注释，在调试的时候可能总会需要注释一些东西或取消注释，现在好了，不需要每行进行重复的注释。

1. 【Ctrl+O】

显示类中方法和属性的大纲，能快速定位类的方法和属性，在查找Bug时非常有用。

1. 【Ctrl+D】

删除当前行，这也是笔者的最爱之一，不用为删除一行而按那么多次的删除键。

    >【Ctrl+Alt+Up】：向上复制当前行（可以选择多行则一次复制多行）
    >【Ctrl+Alt+Down】：向下复制当前行（可以选择多行则一次复制多行）

1. 【Ctrl+M】

窗口最大化和还原，用户在窗口中进行操作时，总会觉得当前窗口小（尤其在编写代码时），现在好了，试试【Ctrl+M】快捷键。

## 查看和定位快捷键

在程序中，迅速定位代码的位置，快速找到Bug的所在，是非常不容易的事，Eclipse提供了强大的查找功能，可以利用如下的快捷键帮助完成查找定位的工作。

1. 【Ctrl+Shift+T】

查找工作空间（Workspace）构建路径中的可找到Java类文件，不要为找不到类而痛苦，而且可以使用“*”、“？”等通配符。

1. 【Ctrl+Shift+R】

和【Ctrl+Shift+T】对应，查找工作空间（Workspace）中的所有文件（包括Java文件），也可以使用通配符。

1. 【Ctrl+Shift+G】

查找类、方法和属性的引用。这是一个非常实用的快捷键，例如要修改引用某个方法的代码，可以通过【Ctrl+Shift+G】快捷键迅速定位所有引用此方法的位置。

1. 【Ctrl+Shift+O】

快速生成import，当从网上拷贝一段程序后，不知道如何import进所调用的类，试试【Ctrl+Shift+O】快捷键，一定会有惊喜。

1. 【Ctrl+Shift+F】

格式化代码，书写格式规范的代码是每一个程序员的必修之课，当看见某段代码极不顺眼时，选定后按【Ctrl+Shift+F】快捷键可以格式化这段代码，如果不选定代码则默认格式化当前文件（Java文件）。

1. 【Ctrl+K】、【Ctrl++Shift+K】

快速向下和向上查找选定的内容，从此不再需要用鼠标单击查找对话框了。

1. 【Ctrl+L】

定位到当前编辑器的某一行，对非Java文件也有效。

1. 【Alt+←】、【Alt+→】

后退历史记录和前进历史记录，在跟踪代码时非常有用，用户可能查找了几个有关联的地方，但可能记不清楚了，可以通过这两个快捷键定位查找的顺序。

1. 【F3】

快速定位光标位置的某个类、方法和属性。

1. 【F4】

显示类的继承关系，并打开类继承视图。

## 调试快捷键

Eclipse中有如下一些和运行调试相关的快捷键。

1. 【Ctrl+Shift+B】：在当前行设置断点或取消设置的断点。
1. 【F11】：调试最后一次执行的程序。
1. 【Ctrl+F11】：运行最后一次执行的程序。
1. 【F5】：跟踪到方法中，当程序执行到某方法时，可以按【F5】键跟踪到方法中。
1. 【F6】：单步执行程序。
1. 【F7】：执行完方法，返回到调用此方法的后一条语句。
1. 【F8】：继续执行，到下一个断点或程序结束。

## 其他快捷键

Eclipse中还有很多快捷键，无法一一列举，用户可以通过帮助文档找到它们的使用方式，另外还有几个常用的快捷键如下。

1. 【Ctrl+F6】：切换到下一个编辑器。
1. 【Ctrl+Shift+F6】：切换到上一个编辑器。
1. 【Ctrl+F7】：切换到下一个视图。
1. 【Ctrl+Shift+F7】：切换到上一个视图。
1. 【Ctrl+F8】：切换到下一个透视图。
1. 【Ctrl+Shift+F8】：切换到上一个透视图。

## 补充

1. 【Ctrl+F11】：运行当前项目 = 【Alt+Shift+X,J】
1. 【Ctrl+MouseLeft】： = 【F3】
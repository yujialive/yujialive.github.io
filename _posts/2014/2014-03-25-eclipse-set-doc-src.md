---
layout: post
title: Eclipse中如何关联Javadoc
categories: java
tags: 
- java
- Eclipse
---

Eclipse有直接查看java文档和类库源码的功能，不过得手工添加才行，下面对如何在Eclipse中添加java文档和类库源码进行总结

1. Window->Preferences打开参数选择对话框，展开Java节点，单击“InstalledJREs"，此时右边窗口会显示已经加载的jre。

2. 选中要设置的jre版本，单击"Edit"，弹出JRE编辑窗口

3. 添加javadoc：将JREsystem libraries下的所有包选中，单击右边的“JavadocLocation”按钮，弹出javadoc设置窗口。选择“JavadocURL”单选框，单击“Browse”按钮，选中docs/api目录，然后点击“OK”

4. 添加source：将JREsystem libraries下的所有包选中，单击右边的“SourceAttachment”按钮，弹出sourceattachment configuration窗口。单击“ExternalFile”按钮，选中java安装目录中的src.zip文件，然后点击“OK”

5. 后面就一路OK、确定就行了。

6. 在添加好了javadoc与source后，

在eclipse中，使用快捷键`Shift+F2`，可快速调出选中类的api文档；
使用快捷建`F3`（或在类上点击右键，现在查看声明），可打开类的源文件。

    Shift+F2 -> Go to JavaDoc
    F3 -> Goto Source


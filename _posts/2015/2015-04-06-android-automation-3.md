---
layout: post
title: Android自动化3_架构实现
categories: android
tags: 
- automation
---


前两节讲了用Android SDK自带的tool-hierarchyviewer来捕获Activity上Element，并分析了其中的原理。对于要实现GUI自动化，还有哪些工作没有完成呢？

1. Invoke界面上的Element，如点击按钮，在文本框中输入内容等
2. Press手机自身所有的按键，如HOME键，Menu键，左右上下方向键，通话键，挂机键等
3. 判断测试结果

前面说过，直接从Emulator内部获取当前Activity上的Element这条路已经断了，同理，探索像UI Automation上一样Invoke Element的操作估计是行不通了，因为你拿不到Element的对象实例，所以实例所支持的方法当然也没有办法拿到。

怎么办？实在不行，基于坐标来对Element进行触发总可以吧。在Windows中发送基于坐标发送键盘和鼠标事件一般是在无法识别Element的情况下，想的最后一招，这使我想起起了Android中的monkey测试，对着屏幕就是一通乱点，压根就不管点的是什么。所幸的是，当前Android系统中我们得到了Element的属性信息，其中就包括坐标信息，而且这种信息是具有弹性的，也就是说即使Element的坐标随着开发的改变而有所变化，也不用担心，因为当前的坐标是实时获得的。

那么怎样才能给Element发送模拟按键等操作呢？总不能用Windows当前的键盘和鼠标事件吧，那样一旦模拟器的位置改变或失去焦点，啥都白搭，风险太大了。看来给Emulator内部发送模拟按键等操作比较靠谱。查了一下SDK，其中确实有这样的方法存在，但是我们当前的测试基础架构程序位于Emulator外部，怎么办？突然想起了hierarchyviewer的实现机制，通过Socket来发送信息。Hierarchyviewer有系统自带的进程给予答复响应（具体是哪个进程进行的响应不清楚，没有研究过）。那么我们也来模拟做一个Listener总可以吧。

其实对于模拟按键发送，网上的帖子很多，但大部分是基于一种方式实现的，IWindowManager接口。不巧的是，SDK并没有将该接口提供为public，所以需要用android源码替代android.jar包进行编译的方式进行绕行，感觉方法有点复杂。在后面另一篇系列文章中我会列出我在网上看到的另一种基于Instrumentation和MessageQueue的机制实现方法。

最后就剩下判断测试结果了。判断测试结果一般分为如下两种：外部条件是否满足，如文件是否产生，数据是否生成等；内部条件是否满足，如对应的Element是否出现或消失，Element上内容如字符串是否有变化。对于前一种本文不予讨论，后一种情况下，Element出现或消失可以通过hierarchyviewer来获取。仔细研究过hierarchyviewer会发现，它并没有提供Element界面上内容（Text）的属性。这可有点晕了，好像又要回到实现捕获Activity实例的老路上来了。考虑图像识别？这好像不靠谱。突然想到，4939端口上发送DUMP命令后的返回结果中会不会有此类hierarchyviewer没有显示出来的信息呢，万幸，还真有。在我上一篇博文（Hierarchyviewer 捕获Element的实现原理）中查询mText字段，会发现mText=1,5这样的信息，其实就是代表了计算器Button5上显示的内容5，逗号前的1表示后跟一位信息。

至此，问题似乎都解决掉了。画个基础架构图做个总结：

<img src="/media/img/android_automation.png" />
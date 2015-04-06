---
layout: post
title: Android自动化5_再述模拟键盘鼠标事件adb_shell_实现
categories: android
tags: 
- automation
---


上一篇博文中讲述了通过Socket编程从外部向Emulator发送键盘鼠标模拟事件，貌似实现细节有点复杂。其实Android还有一种更简单的模拟键盘鼠标事件的方法，那就是通过使用adb shell 命令。

1. 发送键盘事件：
命令格式1：adb shell input keyevent “value”
其中value以及对应的key code如下表所列：

在SDK2.1的模拟器中命令失效，sendevent命令可行
 
命令格式2：adb shell sendevent [device] [type] [code] [value]
如： 

    adb shell sendevent /dev/input/event0 1 229 1 代表按下按下menu键
    adb shell sendevent /dev/input/event0 1 229 0 代表按下松开menu键

说明：上述的命令需组合使用
另外所知道的命令如下：

    Key Name                       CODE
    MENU                           229
    HOME                           102
    BACK (back button)             158
    CALL (call button)             231
    END (end call button)          107
 
2. 发送鼠标事件(Touch)：
命令格式：adb shell sendevent [device] [type] [code] [value]
 
情况1：在某坐标点上touch
如在屏幕的x坐标为40，y坐标为210的点上touch一下，命令如下

    adb shell sendevent /dev/input/event0 3 0 40
    adb shell sendevent /dev/input/event0 3 1 210
     
    adb shell sendevent /dev/input/event0 1 330 1 //touch
    adb shell sendevent /dev/input/event0 0 0 0       //it must have
     
    adb shell sendevent /dev/input/event0 1 330 0 //untouch
    adb shell sendevent /dev/input/event0 0 0 0 //it must have
 
注：以上六组命令必须配合使用，缺一不可
 
情况2: 模拟滑动轨迹（可下载并采用aPaint软件进行试验）
如下例是在aPaint软件上画出一条开始于（100,200），止于（108,200）的水平直线

    adb shell sendevent /dev/input/event0 3 0 100 //start from point (100,200)
    adb shell sendevent /dev/input/event0 3 1 200
     
    adb shell sendevent /dev/input/event0 1 330 1 //touch
    adb shell sendevent /dev/input/event0 0 0 0
     
    adb shell sendevent /dev/input/event0 3 0 101 //step to point (101,200)
    adb shell sendevent /dev/input/event0 0 0 0     //must list each step, here just skip
    adb shell sendevent /dev/input/event0 3 0 108 //end point(108,200)
    adb shell sendevent /dev/input/event0 0 0 0
     
    adb shell sendevent /dev/input/event0 1 330 0 //untouch
    adb shell sendevent /dev/input/event0 0 0 0
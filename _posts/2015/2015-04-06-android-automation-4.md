---
layout: post
title: [Android自动化4]模拟键盘鼠标事件(Socket+Instrumentation实现)
categories: android
tags: 
- automation
---

通过Socket + Instrumentation实现模拟键盘鼠标事件主要通过以下三个部分组成：
## Socket编程：
实现PC和Emulator通讯，并进行循环监听

## Service服务：
将Socket的监听程序放在Service中，从而达到后台运行的目的。这里要说明的是启动服务有两种方式，bindService和startService，两者的区别是，前者会使启动的Service随着启动Service的Activity的消亡而消亡，而startService则不会这样，除非显式调用stopService，否则一直会在后台运行因为Service需要通过一个Activity来进行启动，所以采用startService更适合当前的情形

## Instrumentation发送键盘鼠标事件：
Instrumentation提供了丰富的以send开头的函数接口来实现模拟键盘鼠标，

如下所述：

    sendCharacterSync(int keyCode)            //用于发送指定KeyCode的按键
    sendKeyDownUpSync(int key)                //用于发送指定KeyCode的按键
    sendPointerSync(MotionEvent event)     //用于模拟Touch
    sendStringSync(String text)                   //用于发送字符串

注意：以上函数必须通过Message的形式抛到Message队列中。如果直接进行调用加会导致程序崩溃。


对于Socket编程和Service网上有很多成功的范例，此文不再累述，下面着重介绍一下发送键盘鼠标模拟事件的代码：
1. 发送键盘KeyCode

步骤1. 声明类handler变量

    private static Handler handler;
 
步骤2. 循环处理Message

    //在Activity的onCreate方法中对下列函数进行调用
    private void createMessageHandleThread(){
        //need start a thread to raise looper, otherwise it will be blocked
            Thread t = new Thread() {
                public void run() {
                    Log.i( TAG,"Creating handler ..." );
                    Looper.prepare();
                    handler = new Handler(){
                        public void handleMessage(Message msg) {
                               //process incoming messages here
                        }
                    };
                    Looper.loop();
                    Log.i( TAG, "Looper thread ends" );
                }
            };
            t.start();
    }
 
步骤3. 在接收到Socket中的传递信息后抛出Message

    handler.post( new Runnable() {
                public void run() {
    Instrumentation inst=new Instrumentation();
    inst.sendKeyDownUpSync(keyCode);
    }
    } );
 
2. Touch指定坐标，如下例子即touch point（240,400）

CODE

    Instrumentation inst=new Instrumentation();
    inst.sendPointerSync(MotionEvent.obtain(SystemClock.uptimeMillis(),SystemClock.uptimeMillis(), MotionEvent.ACTION_DOWN, 240, 400, 0));
    inst.sendPointerSync(MotionEvent.obtain(SystemClock.uptimeMillis(),SystemClock.uptimeMillis(), MotionEvent.ACTION_UP, 240, 400, 0));
          
3. 模拟滑动轨迹

将上述方法中间添加 MotionEvent.ACTION_MOVE
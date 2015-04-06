---
layout: post
title: Android自动化2_Hierarchyviewer捕获Element的实现原理
categories: android
tags: 
- automation
---

# [Android自动化2]Hierarchyviewer捕获Element的实现原理

Android SDK tools下的工具hierarchyviewer可以展现Device上的Element的层次分布和自身属性，其核心函数之一就是LoadScene，研究后发现其实现方法是向Device的4939端口通过socket的方式发送了一个DUMP的命令，Device会自动处理该命令并将所有Screen上的Element层次结构和属性一并发回，实现代码如下：

{% highlight java %}
public static void listElement(IDevice device) {
    Socket socket;
    BufferedReader in;
    BufferedWriter out;
    socket = null;
    in = null;
    out = null;
   
    do {
        DeviceBridge.setupDeviceForward(device);
    } while(4939!=DeviceBridge.getDeviceLocalPort(device));
   
    socket = new Socket();
    try {

        socket.connect(new InetSocketAddress("127.0.0.1", DeviceBridge.getDeviceLocalPort(device)));
        out = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
         
        in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
                   
        System.out.println("==> DUMP");
        out.write((new StringBuilder()).append("DUMP -1").toString());
                   
        out.newLine();
        out.flush();
        do {
            String line;
            if ((line = in.readLine()) == null || "DONE.".equalsIgnoreCase(line))
                break;
            line = line.trim();
            System.out.println(line);
        } while (true);

    } catch (IOException e) {
        e.printStackTrace();
    }
}

{% endhighlight %}

运行后的结果摘录其中一部分（button5），列举如下。注：当前device中运行的是2.1SDK中自带的Calculator程序：

    com.android.calculator2.ColorButton@43b8bee8 mText=1,5 getEllipsize()=4,null mMinWidth=1,0 mMinHeight=1,0 mMeasuredWidth=2,79 mPaddingBottom=1,0 mPaddingLeft=1,0 mPaddingRight=1,0 mPaddingTop=1,0 mMeasuredHeight=2,78 mLeft=2,81 mPrivateFlags_DRAWING_CACHE_INVALID=3,0x0 mPrivateFlags_DRAWN=4,0x20 mPrivateFlags=8,16779312 mID=9,id/digit5 mRight=3,160 mScrollX=1,0 mScrollY=1,0 mTop=1,0 mBottom=2,78 mUserPaddingBottom=1,0 mUserPaddingRight=1,0 mViewFlags=9,402669569 getBaseline()=2,54 getHeight()=2,78 layout_gravity=4,NONE layout_weight=3,1.0 layout_bottomMargin=1,0 layout_leftMargin=1,1 layout_rightMargin=1,0 layout_topMargin=1,0 layout_height=11,FILL_PARENT layout_width=11,FILL_PARENT getTag()=4,null getVisibility()=7,VISIBLE getWidth()=2,79 hasFocus()=5,false isClickable()=4,true isDrawingCacheEnabled()=5,false isEnabled()=4,true isFocusable()=4,true isFocusableInTouchMode()=5,false isFocused()=5,false isHapticFeedbackEnabled()=4,true isInTouchMode()=4,true isOpaque()=5,false isSelected()=5,false isSoundEffectsEnabled()=4,true willNotCacheDrawing()=5,false willNotDraw()=5,false

另外还支持如下命令：

    - LIST will show the list of windows:
    LIST
    43514758 com.android.launcher/com.android.launcher.Launcher
    4359e4d0 TrackingView
    435b00a0 StatusBarExpanded
    43463710 StatusBar
    43484c58 Keyguard
    DONE.

END
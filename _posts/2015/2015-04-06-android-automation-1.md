---
layout: post
title: Android自动化测试初探1: 捕获Activity上的Element
categories: android
tags: 
- automation
---

## 第一部分：前言

 SDK中android.test等命名空间下的内容进行，但是Android系统下应用程序的测试现在应该还算是个新的领域，网上关于这方面的资料很多都是基于白盒测试的，一般都是基于JUnit框架和Android有一个前提，那就是必须要有应用程序的源代码以提供测试接入点，但是这在很多软件公司中是不现实的。很多测试工程师做的工作是完全黑盒，基本接触不到源代码，白盒测试大部分也是由开发自己完成。

回顾一下Windows下的黑盒测试自动化，先前使用的是微软提供的基于.net framework的UI Automation自动化测试框架（要求版本在.net framework 3.0以上，即VS.NET 2008 开发环境），对与擅长C#语言的人来说，使用起来确认比较好用。本人也写了基于UI Automation的轻量级的自动化框架，将在以后的博文中引出。

那在Android操作系统中能不能做类似于UI Automation的事情呢？不幸的是，Android的权限控制分的非常清楚，不同程序之间的数据访问只能通过Intent，content provider类似的功能实现。也就是说你开发的运行在Android中的自动化程序想要捕获当前运行的AUT (Application under Test) 界面上的控件等Element（该术语引自UI Automation，觉得翻译成元素有点生硬，故不作翻译）基本不可能，你也拿不到当前active activity的引用（截止本文发帖为止，个人暂时没有找到办法获得此引用）。

无路可走了？模拟器里面不能走，外面能不能走？或许可以。

## 第二部分：捕获Activity上的Element

在Android的SDK中自带了一个对自动化测试比较有用的工具：hierarchyviewer（位于SDK的tools目录下）。在模拟器运行的情况下，使用该工具可以将当前的Activity上的Element以对象树的形式展现出来，每个Element所含的属性也能一一尽显。这有点像Windows上运行的UI SPY，唯一遗憾的是不支持事件的触发。不过没有关系，可以想办法绕，当务之急是能在自行编写的自动化测试代码里找到Activity上的Element。

第一个想到的办法就是看hierarchyviewer源码，不巧，网上搜了一下，没有资源。或许Google的官网上有，但是上不去。看来只能反编译了，找来XJad，暴力之。虽然反编译出来的代码很多地方提示缺少import，但代码基本上是正确的。看了一下，确实也知道了许多。后来在编写代码的过程中，确实也证明了如果想引用hierarchyviewer.jar这个包并调试，还是需要知道里面的一些设置的。

创建基于hierarchyviewer.jar这个包的调用，需要将它和另外两个包，ddmlib.jar（在hierarchyviewer.jar同级目录中有）和org-netbeans-api-visual.jar（需要下载并安装netbeans，在其安装目录中有）一并导入到工程项目中，因为hierarchyviewer的实现依附于这两个包。

想在代码中获取Activity上的Element需要进行如下几个步骤（如果使用过hierarchyviewer这个工具后会发现，自动化代码所要写的就是该工具上的使用步骤）：

1. Ensure adb running
2. Set adb location（因为hierarchyviewer和模拟器的沟通完全是依靠adb做的，所以设定正确的adb程序的位置至关重要，本人就曾在这个问题上栽了半天多）
3. Get Active Device (这个等同动作发生在启动hierarchyviewer工具时)
4. Start View Server  (等同于工具上Start Server 菜单触发事件)
5. Load Scene (等同于工具上Load View Hierarchy菜单触发事件)
6. Get Root View Node (获得对象树的根节点，这个动作在工具上点击Load View Hierarchy菜单后会自动加载)
7. Get Sub View Node (获得想要查找的View Node，这个动作在工具上点击Load View Hierarchy菜单后会自动加载)

说明：上述步骤中一些名称实际上就是hierarchyviewer中所提供的可访问方法名称，如startViewServer、loadScene、rootNode等。另外View Node实际上hierarchyviewer中的一个类，表示的对象树上的一个Element。

现将部分核心代码粘贴如下：

1. Set adb location

CODE 

    System.setProperty("hierarchyviewer.adb","E:/Android/android-sdk-windows/tools");
    其中"hierarchyviewer.adb" 这个key是hierarchyviewer.jar中指定的，后面的value是存放Android SDK的路径。这个目录必须是当前运行的模拟器所对应的adb的目录，不能自行使用其他目录下adb，否则会发生adb进程异常退出的错误。
     
2. Get Active Device

CODE 

{% highlight java %}

IDevice[] devices = null;
DeviceBridge.terminate();
while(null==devices || 0==devices.length){
    DeviceBridge.initDebugBridge();
    //it must wait for some time, otherwise will throw exception
    try {
        Thread.sleep(1000);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    devices = DeviceBridge.getDevices();
}
return devices;

{% endhighlight %}

以上方法返回的是所有当前运行的Device列表
 
3. Start View Server

CODE 

    DeviceBridge.startViewServer(device);
 
4. Load Scene

CODE

    ViewHierarchyLoader.loadScene(device, Window.FOCUSED_WINDOW) ;
 
5. Get Root View Node

CODE

    vhs.getRoot();
    其中vhs是ViewHierarchyScene的实例对象
 
6. Get Sub View Node

CODE

{% highlight java %}

public ViewNode findFirstChildrenElement(IDevice device, 
            ViewNode entryViewNode, String elementID) {
    ViewNode node=null;
    if(0!=entryViewNode.children.size()) {
          for(int i=0;i<entryViewNode.children.size();i++) {
                node=entryViewNode.children.get(i);
                if(node.id==elementID)
                    return node;
                else
                    continue;
          }
    }
    return node;
}

{% endhighlight %}

虽然上述步骤所涉及的代码量不多，但是花了一天多的时间才终究研究出来，写下此文希望对正在研究Android自动化测试的同学们有些帮助。
到目前为止，Element已经得到了，接下去就是实现怎么去触发这些Element,如click button，enter text等等，尚需再慢慢研究，等有结果再贴出来分享！
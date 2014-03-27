---
layout: post
title: cygwin和emacs搭建
categories: emacs
tags: 
- cygwin
- emacs
---
## Java GregorianCalendar class

{% highlight java %}
GregorianCalendar a = new GregorianCalendar(1999, Calendar.DECEMBER, 31);
GregorianCalendar now = new GregorianCalendar();
int month = now.get(Calendar.MONTH);
int weekday = now.get(Calendar.DAY_OF_WEEK);

GregorianCalendar now = new GregorianCalendar();
int month = now.get(Calendar.MONTH);
int weekday = now.get(Calendar.DAY_OF_WEEK);

deadline.set(Calendar.YEAR, 2001);
deadline.set(Calendar.MONTH, Calendar.APRIL);
deadline.set(Calendar.DAY_OF_MONTH, 15);

Date time = calendar.getTime();
calendar.setTime(time);

{% endhighlight %}

## CMD

    set | find /i /n "home"
    doskey findstr=findstr /a:a /sinc:$
    doskey findfile=for /r %%i in (*$*) do @echo %%i

## cygwin

## emacs

### links

- [一年成为Emacs高手(像神一样使用编辑器)](http://blog.csdn.net/redguardtoo/article/details/7222501)
- [http://blog.binchen.org/](http://blog.binchen.org/)

## Git shortcut: git_bash

{% highlight vb %}
Set fso = CreateObject("Scripting.FileSystemObject")
Set shell = CreateObject("WScript.Shell")

Const TemporaryFolder = 2
linkfile = fso.BuildPath(fso.GetSpecialFolder(TemporaryFolder), "Git Bash.lnk")
gitdir = fso.GetParentFolderName(WScript.ScriptFullName)

' Dynamically create a shortcut with the current directory as the working directory.
Set link = shell.CreateShortcut(linkfile)
link.TargetPath = fso.BuildPath(gitdir, "bin\sh.exe")
link.Arguments = "--login -i"
link.IconLocation = fso.BuildPath(gitdir, "etc\git.ico")
If WScript.Arguments.Length > 0 Then link.WorkingDirectory = WScript.Arguments(0)
link.Save

Set app = CreateObject("Shell.Application")
app.ShellExecute linkfile
{% endhighlight %}
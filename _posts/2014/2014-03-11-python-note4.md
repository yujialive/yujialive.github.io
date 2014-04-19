---
layout: post
title: Python学习4
categories: study
tags: 
- python
---

> Here’s a tip on how to memorize something without going insane: Do a tiny bit at a time throughout
the day and mark down what you need to work on most. Do not try to sit down for two hours
straight and memorize these tables. This won’t work. Your brain will really only retain whatever
you studied in the first 15 or 30 minutes anyway.


## Tuple
Tuple 是不可变的 list。一旦创建了一个 tuple，就不能以任何方式改变它。

What does result = sentence[:] do?
That’s a Python way of copying a list.
a = b  # 只是copy引用
a = b[:]    # clone 复制新对象


    class Employee(Person):
    def __init__(self, name, salary):
    ## hmm what is this strange magic?
    super(Employee, self).__init__(name)
    ## 
    self.salary = salary

## Python 关键字大小写注意
* object
* None

### os.environ

    import os
    path = os.environ["PATH"]
    user = os.environ["USER"]
    editor = os.environ["EDITOR"]
    ... etc ...

Modifications to os.environ affect both the running program and subprocesses created
by Python.

### sys.path
import sys
sys.path.append("mymodules.zip")
import foo, bar
---
layout: post
title: python + xml + excel
categories: python
tags: 
- lxml
- xlrd
- xlwt
- xlutils
---
## python excel
- http://www.gocalf.com/blog/python-read-write-excel.html
- http://www.python-excel.org/
- http://www.cnblogs.com/lhj588/archive/2012/01/06/2314181.html

- pip install xlrd
- pip install xlwt
- pip install xlutils

code

    import win32com.client
    excel = win32com.client.DispatchEx('Excel.Application')
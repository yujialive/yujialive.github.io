---
layout: post
title: Python学习1
categories: study
tags: 
- python
- python3
- crawler
---

## 札记
> 初学编程，最应该记住的是在学习区刻意大量练习，千万少看书，要多练习。当年我从管理咨询行业继承的陋习，先看大量资料，才进入某个领域，并不适合学习编程。
什么是执行意图？就是使用if...then...的思考范式。比如， 不要再说，我要学Ruby。 而是说，如果我要学习Ruby，那么，今天晚上就装上环境。

## 用什么做爬虫
- Python + requests + lxml + celery
> 我是把爬虫的各个功能部分分成小任务, 然后按需放入任务队列中. 这样既能有效的降低爬虫的复杂度, 同时用队列也能提高爬虫的稳健度, 比如失败重做.
还有, 使用celery后你的爬虫就变成分布式的了, 可以简单的布置在多台机器上跑
- Node 	+ jquery
> 前几天 用nodejs写个玩，但不知道怎么部署在只有web服务的 PaaS上－，－
cheerio很好用阿，完全是jQuery的语法。
require('http');require('cheerio');require('iconv').Iconv;require('mongodb');
- Python + requests + pyquery 
- Python + Scrapy (http://scrapy.org/)
- Python + pyquery
- Python + Beautiful Soup + lxml + Scrapy
- Java + jsoup (http://try.jsoup.org/)
- Ruby + norogiri (http://nokogiri.org/)
- PHP + curl\_multi\_*
- PHP + snoopy
- Phantomjs + Casperjs
- Node + cheerio


## 阿里云OS
阿里云OS的本质是移动互联网大数据收集器

平台、金融和数据是阿里集团的三个发展阶段：平台是阿里过去打造的业务也是主要的利润来源；金融是阿里集团正在努力发展的，由彭蕾负责；而数据则代表阿里集团的未来。

## Python
如果我要学习Python，那么，今天晚上就装上环境

### 3 Skills
1. reading and writing
2. attention to detail
3. spotting differences

	[Environment]::SetEnvironmentVariable("Path", "$env:Path;C:\Python27", "User")

### Numbers and Match
	+ 	plus
	- 	minus
	/ 	slash
	* 	asterisk
	% 	percent / modulus
	< 	less-than
	> 	greater-than
	<= 	less-than-equal
	>= 	greater-than-equal

### pygments: true
{% highlight python %}
my_name = 'Zed A. Shaw'
my_age = 35 # not a lie
my_height = 74 # inches
my_weight = 180 # lbs
my_eyes = 'Blue'
my_teeth = 'White'
my_hair = 'Brown'

print "Let's talk about %s." % my_name
print "He's %d inches tall." % my_height
print "He's %d pounds heavy." % my_weight
print "Actually that's not too heavy."
print "He's got %s eyes and %s hair." % (my_eyes, my_hair)
print "His teeth are usually %s depending on the coffee." % my_teeth

# this line is tricky, try to get it exactly right
print "If I add %d, %d, and %d I get %d." % (
	my_age, my_height, my_weight, my_age + my_height + my_weight)
{% endhighlight %}

### Python3格式化字符串
Python3中如何`print()`方法 `format string`
具体请参看官方文档[python docs](http://docs.python.org/2/library/string.html)
使用"str".format()方法
{% highlight python %}
# Sample 1
my_name = "Panda Yu"
my_age = 32 # not a lie
out_string = "let's talk about {0}, my age is {1}".format(my_name, my_age)
print(out_string)

# Sample 2
int_count = 30
float_num = 2323.443
out_string = "|{0:20d}|{0:>20d}|{1:.3f}|{1:20f}|".format(int_count, float_num)
print(out_string)

out_string = "|{0:20d}|{0:<20d}|{1:.3f}|{1:20f}|".format(int_count, float_num)
print(out_string)

# Sample 3
print('This {food} is {adjective}.'.format(food='spam', adjective='absolutely horrible'))
print("abc {:s}".format("gagaag"))

# Sample 4
x = "There are %d types of people." % 10
y = "Hello world"
print("I said: %r." % x)
print("I also said: '%s'." % y)
print("%d %s %f" %(10, "hello", 34))
# What is the difference between %r and %s?
# We use %r for debugging, since it displays the “raw” data of the variable, but we use %s and
# others for displaying to users.

# Sample 5
hilarious = False
joke_evaluation = "Isn't that joke so funny?! %r"
print(joke_evaluation % hilarious)
print('.' * 10)

# Sample 6
formatter = "%r %r %r %r"

print(formatter % (1, 2, 3, 4))
print(formatter % ("one", "two", "three", "four"))
print(formatter % (True, False, False, True))
print(formatter % (formatter, formatter, formatter, formatter))
print(formatter % (
	"I had this thing.",
	"That you could type up right.",
	"But it didn't sing.",
	"So I said goodnight."
	))
{% endhighlight %}
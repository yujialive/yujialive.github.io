---
layout: post
title: Python学习1
categories: study
tags: 
- python
- python3
---

## 札记
> 初学编程，最应该记住的是在学习区刻意大量练习，千万少看书，要多练习。当年我从管理咨询行业继承的陋习，先看大量资料，才进入某个领域，并不适合学习编程。
什么是执行意图？就是使用if...then...的思考范式。比如， 不要再说，我要学Ruby。 而是说，如果我要学习Ruby，那么，今天晚上就装上环境。

> 如果我要学习Python，那么，今天晚上就装上环境
	1. reading and writing
	2. attention to detail
	3. spotting differences

	[Environment]::SetEnvironmentVariable("Path", "$env:Path;C:\Python27", "User")

## Numbers and Match
	+ 	plus
	- 	minus
	/ 	slash
	* 	asterisk
	% 	percent / modulus
	< 	less-than
	> 	greater-than
	<= 	less-than-equal
	>= 	greater-than-equal

## pygments: true
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

## Python3格式化字符串
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

## Printing
{% highlight python %}
days = "Mon Tue Wed Thu Fri Sat Sun"
months = "Jan\nFeb\nMar\nApr\nMay\nJun\nJul\nAug"

print("Here are the days: ", days)
print("Here are the months: ", months)

print("""
There's something going on here.
With the three double- quotes.
We'll be able to type as much as we like.
Even 4 lines if we want, or 5, or 6.
""")

# Output
# Here are the days:  Mon Tue Wed Thu Fri Sat Sun
# Here are the months:  Jan
# Feb
# Mar
# Apr
# May
# Jun
# Jul
# Aug

# There's something going on here.
# With the three double- quotes.
# We'll be able to type as much as we like.
# Even 4 lines if we want, or 5, or 6

{% endhighlight %}

## Escape Sequences

	\\ 			Backslash (\)
	\' 			Single-quote (')
	\" 			Double-quote (")
	\a 			ASCII bell (BEL)
	\b 			ASCII backspace (BS)
	\f 			ASCII formfeed (FF)
	\n 			ASCII linefeed (LF)
	\N{name} 	Character named name in the Unicode database (Unicode only)
	\r 			ASCII carriage return (CR)
	\t 			ASCII horizontal tab (TAB)
	\uxxxx 		Character with 16-bit hex value xxxx (Unicode only)
	\Uxxxxxxxx 	Character with 32-bit hex value xxxxxxxx (Unicode only)
	\v 			ASCII vertical tab (VT)
	\ooo 		Character with octal value oo
	\xhh 		Character with hex value hh

## pygments 备忘
> {% raw %}{% endhighlight %}{% endraw %}之前行不要有'.'或者最好加个空行
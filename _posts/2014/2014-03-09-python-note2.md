---
layout: post
title: Python学习2
categories: study
tags: python, python3
---

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
> {% endhighlight %}之前行不要有.或者最好加个空行
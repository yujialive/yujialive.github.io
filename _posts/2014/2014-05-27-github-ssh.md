---
layout: post
title: Github SSH 设置
categories: github
tags: 
- ssh
---

link: <http://beiyuu.com/github-pages/>
link: <https://help.github.com/articles/changing-a-remote-s-url>

## open git bash to gen key

{% highlight bash %}

	ssh-keygen -T rsa -C "yujialive@gmail.com"
	passphrase # 可以为空格

	<homedir>/.ssh/id_rsa
	<homedir>/.ssh/id_rsa.pub

{% endhighlight %}

## copy pub key to github site

{% highlight bash %}

	id_rsa.pub to github.com -- user settings -- ssh keys

{% endhighlight %}

## test ssh and gen hosts

{% highlight bash %}

	ssh -T git@github.com

{% endhighlight %}

## config repo

{% highlight bash %}

	# change to ssh link for old repo
	git remote -v
	git remote set-url origin git@github.com:yujialive/yujialive.github.io.git

	# new git repo
	git remote add origin git@github.com:yujialive/yujialive.github.io.git

	git config --global user.name "yujialive"
	git config --global user.email "yujialive@gmail.com"

	# or
	git config --local user.name "yujialive"
	git config --local user.email "yujialive@gmail.com"

{% endhighlight %}
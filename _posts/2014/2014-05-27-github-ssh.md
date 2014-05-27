---
layout: post
title: Github SSH 设置
categories: github
tags: 
- ssh
---

reference: <http://beiyuu.com/github-pages/>

## Open git bash
	ssh-keygen -T rsa -C "yujialive@gmail.com"
	passphrase

	<userhome>/.ssh/id_rsa
	<userhome>/.ssh/id_rsa.pub

## Copy pub key
	id_rsa.pub to github.com -- user settings -- ssh keys

## Test SSH
	ssh -T git@github.com
---
layout: post
title: 日记
categories: live
tags: android
---

## 2014-3-2
===========

* Android 开发

[Android Dev](http://developer.android.com)

Activity
Intent

	Intent intent = new Intent(this, DisplayMessageActivity.class);
	EditText editText = (EditText) findViewById(R.id.edit_message);
	String message = editText.getText().toString();
	intent.putExtra(EXTRA_MESSAGE, message);

* Github

git clone https://github.com/yujialive/yujialive.github.io yujialive.github.io
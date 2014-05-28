---
layout: post
title: Django框架
categories: python
tags: django
---
Django


	#in some dir
	python django-admin.py startproject <projname>

	python manage.py startapp <appname>
	
		polls/
		    __init__.py
		    admin.py
		    models.py
		    tests.py
		    views.py

	python manage.py runserver
	python manage.py runserver 8080

	python manage.py syncdb

## Projects vs. apps

What’s the difference between a project and an app? An app is a Web application that does something – e.g., a Weblog system, a database of public records or a simple poll app. A project is a collection of configuration and apps for a particular Web site. `A project can contain multiple apps. An app can be in multiple projects.`

`Your apps can live anywhere on your Python path`. In this tutorial, we’ll create our poll app right next to your manage.py
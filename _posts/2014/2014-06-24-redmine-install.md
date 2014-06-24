---
layout: post
title: Redmine 安装相关
categories: ruby
tags: redmine
---


## 安装系统相关类库组件

	$ sudo apt-get install wget vim build-essential 
	  openssl libreadline6 libreadline6-dev curl git-core 
	  zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev 
	  libxslt-dev autoconf automake libtool imagemagick libpcre3-dev 

## install ruby on rails

如何快速正确的安装 Ruby, Rails 运行环境
link: <https://ruby-china.org/wiki/install_ruby_guide>

以下代码区域，带有 $ 打头的表示需要在控制台（终端）下面执行（不包括 $ 符号）

{% highlight bash %}

$ sudo apt-get install curl

# 安装 RVM
$ curl -L https://get.rvm.io | bash -s stable

# 然后，载入 RVM 环境（新开 Termal 就不用这么做了，会自动重新载入的）
$ source ~/.rvm/scripts/rvm

$ rvm -v
$ rvm install 2.0.0
# 同样继续等待漫长的下载，编译过程，完成以后，Ruby, Ruby Gems 就安装好了。

# RVM 装好以后，需要执行下面的命令将指定版本的 Ruby 设置为系统默认版本
$ rvm 2.0.0 --default

$ ruby -v
$ gem -v

# update source
$ gem source -r https://rubygems.org/
$ gem source -a https://ruby.taobao.org

# 上面 3 个步骤过后，Ruby 环境就安装好了，接下来安装 Rails
$ gem install rails -v '3.2.17'

# 然后测试安装是否正确
$ rails -v

{% endhighlight %}

## install mysql

link: <https://help.ubuntu.com/10.04/serverguide/mysql.html>

{% highlight bash %}

# Installation
$ sudo apt-get install mysql-server

# -u root -p root
$ mysql -u root -p
> show databases;

$ sudo netstat -tap | grep mysql

# When you run this command, you should see the following line or something similar:
$ tcp        0      0 localhost:mysql         *:*                     LISTEN      2556/mysqld

# If the server is not running correctly, you can type the following command to start it:
$ sudo /etc/init.d/mysql restart

** Configuration

# You can edit the /etc/mysql/my.cnf file to configure the basic settings 
# -- log file, port number, etc. For example, to configure MySQL to listen for
# connections from network hosts, change the bind-address directive to the server's IP address:

bind-address = 192.168.0.5

# After making a change to /etc/mysql/my.cnf the mysql daemon will need to be restarted:

$ sudo /etc/init.d/mysql restart


$ sudo apt-get install libmysqlclient-dev
$ sudo dpkg -L libmysqlclient-dev|grep config

> grant all on redmine.* to 'redmine'@'localhost';
> flush privileges;
* install redmine

{% endhighlight %}

## Download redmine
link: http://www.redmine.org/projects/redmine/wiki/RedmineInstall

$ tar -xvf redmine-2.5.1.tar.gz 
basedir: ~/redmine/redmine-2.5.1

## Copy config/database.yml.example to config/database.yml

	# edit 
	production:
	  adapter: mysql2
	  database: redmine
	  host: localhost
	  port: 3307
	  username: redmine
	  password: 'my_password'


## Dependencies installation

{% highlight bash %}

# You need to install Bundler first
$ gem install bundler

# cd to redmine dir
$ cd ~/redmine/redmine-2.5.1

# Then you can install all the gems required by Redmine using the following command
$ bundle install --without development test

# If ImageMagick is not installed on your system, you should skip the installation of the rmagick gem using:
$ bundle install --without development test rmagick

# troubleshooting for install mysql2 failed
link: http://rubydoc.info/gems/mysql2/frames

$ gem install mysql2 -- --with-mysql-dir=/usr/share/mysql

# Session store secret generation
$ rake generate_secret_token

$ RAILS_ENV=production rake db:migrate

$ RAILS_ENV=production rake redmine:load_default_data

{% endhighlight %}

<http://www.2cto.com/os/201207/144189.html>

---
layout: post
title:  "Try Jekyll"
date:   2015-02-22
categories: jekyll update
---

## 使用Jekyll
1. 下载安装Jekyll
	
	因为需要使用gem安装Jekyll，但是出现一些不安全提示：
	/System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/lib/ruby/2.0.0/universal-darwin14/rbconfig.rb:213: warning: Insecure world writable dir /usr in PATH, mode 040777
	之后通过硬盘修复得到了解决：
	![image](http://i.stack.imgur.com/OhmNJ.png)

2. 使用Jekyll
	
	基础操作是：添加post到_post文件夹中，我使用的文件格式是Markdown，所以命名格式是：
	
	`YEAR-MOUTH-DAY-DOCNAME.markdown`
	
3. Post规范

	1) 用---前后包住配置文件，之间写一些配置选项
		layout: 文件形式，一般是post
		title: 显示的title
		data: 显示的时间
		categories: 文件路径 `这里我还没有搞懂这个路径和url是怎么对应的`



## 配置Jekyll
1. 修改了config文件，但是却没有反应

	重新开了一个jekyll blog，修改配置文件，文件便可以使用。并且持续修改配置文件，显示有效。
	`不知道为什么之前的不可以`
	（之后我由于添加了post，又出现了无法正常反映改变的情况，即使重新build。当我手动修了index之后，重新build，便可以显示了。同时`根目录中的index.html是一个template，可以通过修改，影响index，同时它可以是markdown，textile格式，之后再进行学习`）
	
2. 搭建到github pages

	http://theloverz.me/tutorials/2013/08/24/use-github-and-jekyll-to-establish-blog/




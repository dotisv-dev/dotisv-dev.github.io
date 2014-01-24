---
layout: post
title: "laravel前置知识点-Composer"
description: ""
category: 
tags: []
---
{% include JB/setup %}

## 使用前提

1. 在线安装Laravel时，需要通过Composer来进行安装；
2. 即使是，下载Laravel的压缩包，也需要Composer来安装依赖的Libs

## Composer [官网](http://www.getcomposer.org/)

百度一下O(∩_∩)O哈哈~

1. 简介

	Composer[1]是PHP中用来管理依赖（dependency）关系的工具。
	你可以在自己的项目中声明所依赖的外部工具库（libraries），
	Composer会帮你安装这些依赖的库文件。

2. 安装

	+ Mac、linux等系统可以通过下载composer.phar文件
		
			命令：curl -sS https://getcomposer.org/installer | php
	+ windows系统可以执行进行安装，安装包：
		[下载地址](https://getcomposer.org/Composer-Setup.exe)

3. 使用
	
	+	定义依赖关系

		+ 创建composer.json，编写:

				{
					"require": {
						"monolog/monolog": "1.*"
					}
				}

	+	执行下载

			php composer.phar install

	很简单哦，这将monolog加载到你们的项目中了

	<img src="/images/composer-install-success.png" alt="composer-install-success" style="width:500px;align:center;">
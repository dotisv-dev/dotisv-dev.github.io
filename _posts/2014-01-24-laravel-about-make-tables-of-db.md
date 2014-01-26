---
layout: post
title: "Laravel之数据的那点事"
description: ""
category: 
tags: []
---
{% include JB/setup %}

# 数据层 

Web开发离不开MVC，M离不开持久层，从数据库结构定义开始分析吧

+ 表结构调整

	1. 创建表结构

			Schema::create('users', function($table)
			{
				$table->increments('id');
			});
	2. 重命名表结构

			Schema::rename($from, $to)
	3. 指定链接数据库
			
			Schema::connection('foo')->create('users', function($data)
			{
				$table->increments('id');
			});
	4. 删除一个表
		
			Schema::drop('users');
			Schema::dropIfExits('users');

+ 字段操作

	1. 添加字段

			Schema::table('users', function($table)
			{
				$table->string('email');
			});
			其他字段类型定义：
			bigIncrements('id'); // bigint 20 pk
			bigInteger('votes'); // bigint 20
			binary('data'); // blob 0
			boolean('confirmed'); // tinyint 1
			date('created_at'); // date 0
			dateTime('created_at'); // datetime 0
			decimal('amount', 5, 2); // decimal 5,2
			double('column', 15, 8); // double 15,8
			enum('choices', array('foo', 'bar')); // enum 0 value:'foo','bar'
			float('amount'); // float 8,2
			increments('id'); // int 10 pk
			integer('votes'); // int 11 pk
			longText('description'); // longtext 0
			mediumText('description'); // mediumtext 0
			morphs('tagglable'); // tagglable_id:int 10 另1个为:tagglable_type:varchar 255
			smallInteger('votes'); // smallint 6
			softDeletes(); // add columns named deleted_at timestamp 0
			string('email'); // varchar 255
			string('name', 100); // varchar 100 
			text('description'); // text 0 
			time('sunrise'); // time 0
			timestamp('added_on'); // add column named created_at timestamp 0, other column named updated_at timestamp 0
			timestamps();
			nullable(); // 允许为空
			default($value); // 设置默认值
			unsigned(); // 无符号数值指定

			注意：可以使用after来指定顺序，如：$table->string('name')->after('email');
	2. 改名

			Schema::table('users', function($table)
			{
				$table->renameColumn('from', 'to');
			});
	3. 删除 

			Schema::table('users', function($table)
			{
				// 单字段
				$table->dropColumn('votes');
				// 多字段
				$table->dropColumn('votes', 'avatar', 'location');
			});
	4. 检测存在

			if(Schema::hasTable('users'))
			{
				// 检测表
			}

			if(Schema::hasColumn('users', 'email'))
			{
				// 检测表中字段
			}
+ 索引-提高性能

	1. 创建索引

			$table->primary('id'); // 主键索引
			$table->primary(array('first', 'last')); // 组合索引
			$table->unique('email'); // 唯一索引，也可以直接添加到定义字段后
			$table->index('state'); // 基本索引
	2. 删除索引
	
			$table->dropPrimary('id');
			$table->dropUnique('email');
			$table->dropIndex('state');

+ 外键约束-常常不使用

	1. 添加外键

			$table->foreign('user_id')->references('id')->on('users');
	2. 声明约束

			$table->foreign('user_id')
				->references('id')->on('users')
				->onDelete('cascade');
	3. 删除外键

			$table->dropForeign('user_id');

+ 存储引擎选择

		Schema::table('users', function($data)
		{
			$table->engine = 'InnoDB';
			$table->string('email');
		});
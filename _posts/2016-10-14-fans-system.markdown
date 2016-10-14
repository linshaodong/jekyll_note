---
layout: post
title:  "粉丝系统的实现"
date:   2016-05-22 04:10:03 +0700
categories: [python, codefights]
---

实现一个效率高，易扩展的粉丝系统

**_1、表结构_**

维护俩张关系表：
关注表：user_attention_分表下标
粉丝表：user_fans_分表下标
注：分表下标 = 用户id % 64
```
CREATE TABLE `user_attention_7` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` bigint(20) NOT NULL COMMENT '我的userid',
  `master_user_id` bigint(20) NOT NULL COMMENT '我的关注的userId',
  `date` datetime NOT NULL COMMENT '关注日期',
  `type` tinyint(2) NOT NULL DEFAULT '0' COMMENT '关系类型：0：关注；2：互粉',
  PRIMARY KEY (`id`),
  KEY `userId_attetionId` (`user_id`,`master_user_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='用户关注表';

CREATE TABLE `user_fans_7` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` bigint(20) NOT NULL COMMENT '我的userid',
  `fans_user_id` bigint(20) NOT NULL COMMENT '粉丝的userId',
  `date` datetime NOT NULL COMMENT '关注日期',
  `type` tinyint(2) NOT NULL DEFAULT '1' COMMENT '关系类型：1：粉丝；2：互粉',
  `status` tinyint(2) NOT NULL DEFAULT '0' COMMENT '状态： 0：新增粉丝；1：已查看过',
  PRIMARY KEY (`id`),
  KEY `userId_fansId` (`user_id`,`fans_user_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='用户粉丝表';
```

**_2、数据交互_**

a) 关注：
- 往user_attention_7和user_fans_7各增加一条数据：
 - user_attention_7：我关注了指定用户
 - user_fans_7：我成为指定用户的粉丝
- 当指定用户也关注了我即互粉关系，新增的和上一步增加数据的type置为2：互粉：
	user_attention_7：指定用户关注了我
	user_fans_7：指定用户成为我的粉丝
	
b) 取消关注：
- 删除user_attention_7和user_fans_7指定的数据，并且如果指定的用户关注了我，则取消该用户的互粉状态：
	user_attention_7：我关注了指定用户
	user_fans_7：我成为指定用户的粉丝

c) 获取关注的相关信息：只需查询user_attention_7

d) 获取关注的相关信息：只需查询user_fans_7
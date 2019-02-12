---
layout: post
title: "LogStash配置-Pipeline"
author: "高灶顺"
header-style: text
tags:
  - ELK日志管理
---
# LogStash配置-Pipeline

# 1、配置语法
字符串类型String：path => "/etc/logstash"<br />布尔类型Boolean：isFailed => true<br />数值类型Number：port => 8888<br />数组Array/List：<br />user => [{id=>1,name=>"gzs"},{id=>2,name=>"gjw"}]<br />path=>["/var/log/msg","var/log/msg2"]<br />哈希类型Hash<br />match => {<br />"field1"=>"value1"<br />"field2"=>"value2"<br />}<br />注释 #<br />取logstash event中的字段值 用[],多层用[][]...<br />字符串中用到字段用%{}，多层嵌套的用%{[][]}<br />支持条件判断语法，格式如下：<br />if EXPRESSION {<br />...<br />} else if EXPRESSION {<br />...<br />} else {<br />...<br />}<br />表达式操作符：<br />-比较：== 、!=、<、>、<=、>=<br />-正则是否匹配：=~、!~<br />-包含(包含字符串和数组)：in、not in<br />-布尔操作符：and、or、nand、xor、!<br />-分组操作符: ()
# 2、input插件
codec
* plain 读取原始内容
* dots 将内容简化为点输出，如果不想输出内容可以使用。![image.png](https://cdn.nlark.com/yuque/0/2019/png/150236/1548406659099-ecfb4b2e-d01c-49dd-ac80-c2fa53388efc.png#align=left&display=inline&height=380&linkTarget=_blank&name=image.png&originHeight=380&originWidth=682&size=41050&width=682)
* rubydebug 将logstash event按照ruby格式输出，方便调试
* line 处理带换行符的内容![image.png](https://cdn.nlark.com/yuque/0/2019/png/150236/1548406114824-0afd0b18-b559-4a3f-85ee-b6a413824c84.png#align=left&display=inline&height=262&linkTarget=_blank&name=image.png&originHeight=262&originWidth=845&size=45705&width=845)
* json 处理json格式的内容![image.png](https://cdn.nlark.com/yuque/0/2019/png/150236/1548406878852-e4c225dd-0c82-4ed8-b976-afabaa1affe8.png#align=left&display=inline&height=447&linkTarget=_blank&name=image.png&originHeight=447&originWidth=755&size=80769&width=755)
* multiline 处理多行数据内容
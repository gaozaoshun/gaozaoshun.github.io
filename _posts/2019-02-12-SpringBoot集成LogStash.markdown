---
layout: post
title: "SpringBoot集成LogStash"
author: "高灶顺"
header-style: text
tags:
  - ELK日志管理
---
# SpringBoot集成LogStash

# 1、集成的好处？
应用日志数据收集、数据处理、集中管理。日志文件不落地到应用服务器，全部通过TCP输出到ES中，方便检索。
# 2、配置依赖
用处：将各种日志框架的日志输出到logstash的input上
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-logging</artifactId>
</dependency>
<dependency>
  <groupId>net.logstash.logback</groupId>
  <artifactId>logstash-logback-encoder</artifactId>
  <version>5.2</version>
</dependency>
```
# 3、配置logback-spring.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <include resource="org/springframework/boot/logging/logback/base.xml" />
    <appender name="LOGSTASH" class="net.logstash.logback.appender.LogstashTcpSocketAppender">
        <!--logstash ip和暴露的端口，我目前理解就是通过这个地址把日志发送过去-->
        <destination>192.168.184.129:9250</destination>
        <encoder charset="UTF-8" class="net.logstash.logback.encoder.LogstashEncoder" />
    </appender>
    <root level="INFO">
        <appender-ref ref="LOGSTASH" />
        <appender-ref ref="CONSOLE" />
    </root>
</configuration>
```
# 4、开放端口
```bash
firewall-cmd --zone=public --add-port=9250/tcp --permanent
firewall-cmd --reload
```
# 5、启动项目

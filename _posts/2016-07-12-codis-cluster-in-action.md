---
layout: post
title:  "Codis集群线上实战"
date:   2016-07-12 21:59:33 +0800
author: ranwuer
categories: work
tags:   redis, 集群, 豌豆荚codis
excerpt:    本文主要介绍了豌豆荚开发的Codis中间件在Redis集群中的应用，基于zookeeper+go+java，都是线上实战记录，干货满满！
---

## 安装Codis集群环境


### 1. 配置服务器A
1. 安装Java环境
2. 安装Go环境
3. 安装Zookeeper
4. 安装Codis
5. 配置Redis(master)
6. 配置Zookeeper
7. 配置Config.ini
8. 配置Redis服务组
9. 配置Redis服务组的Slot


### 2. 配置服务器B
1. 安装Java环境
2. 安装Go环境
2. 安装Zookeeper
3. 安装Codis
4. 配置Redis(slave)
5. 配置Zookeeper

### 3. 配置服务器C
1. 安装Java环境
2. 安装Zookeeper
3. 配置Zookeeper

## 启动各项服务
1. 启动Zookeeper
2. 启动Dashboard
3. 初始化Slot
4. 调整内存分配策略
5. 启动Codis
6. 启动Codis-Proxy

## 测试
1. 压力测试
2. 主从同步测试
3. 高可用测试



## 修改问答板块代码
 1. 修改网页端缓存
 2. 修改APP端缓存


## 常用功能
1. 在线增加分片
2. 数据迁移
3. 自动均衡
4. codis-server的HA

## 容灾机制
1. 服务器重启后的机制
2. 单个Redis挂掉后的机制



## Links
1. [Centos6下Codis集群的搭建与使用](http://www.hi-linux.com/2016/03/28/Centos6%E4%B8%8BCodis%E9%9B%86%E7%BE%A4%E7%9A%84%E6%90%AD%E5%BB%BA%E4%B8%8E%E4%BD%BF%E7%94%A8/)


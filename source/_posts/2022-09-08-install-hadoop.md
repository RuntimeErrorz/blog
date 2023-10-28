---
layout: post
title: 安装Hadoop
subtitle: MapReduce!
author: RuntimeEroor
categories: 软件配置
tags: Hadoop 大数据
date: 2022-09-08
---
# 1. 说在前面

   别在Windows下装这个，超级麻烦的。如果大佬装成功了可以出个教程。
# 2. 下载 Hadoop

   [下载（中科大镜像站）](https://mirrors.ustc.edu.cn/apache/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz)不知道为什么清华镜像站封了我的IP？
# 3. 安装配置SSH免密登录

   不太清楚Standalone模式是否还需要这个？
   ssh密钥应该在home目录下进行生成。
   ```bash
   sudo apt install ssh
   sudo apt install sshd
   ssh-keygen -t rsa
   cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
   chmod og-wx ~/.ssh/authorized_keys
   ssh localhost #如果不需要密码就成功了
   ```
# 4. 下载JDK

   ```bash
   sudo apt install openjdk-8-jdk
   ```
# 5. 配置JDK环境变量

   ```bash
   sudo nano hadoop/etc/hadoop/hadoop-env.sh
   #添加下列
   export JAVA_HOME=/usr/java/latest
   ```
# 6.  运行

   下面这段代码，找出了 `etc/hadoop/`中的 `xml`文件中符合 `dfs[a-z.]+`正则的例子以及出现次数
   ```bash
   mkdir input
   cp etc/hadoop/*.xml input
   bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.4.jar grep input output 'dfs[a-z.]+'
   cat output/*
   ```

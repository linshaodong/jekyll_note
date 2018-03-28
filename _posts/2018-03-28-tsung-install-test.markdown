---
layout: post
title:  "centosm6.5安装tsung和压力测试"
date:   2018-03-28 04:10:03 +0700
categories: [python, codefights]
---

centosm6.5安装tsung和压力测试

**_1、在安装之前确保安装了以下工具_**

```bash
yum install gcc -y
yum install perl -y
yum install unixODBC
yum install unixODBC-devel
yum install -y ncurses-devel
```

**_2、下载并安装erlang_**

```bash
# wget http://www.erlang.org/download/otp_src_R14B04.tar.gz
# tar -zxvf otp_src_R14B04.tar.gz
# cd otp_src_R14B04
# ./configure --prefix=/usr/local/erlang
# make
# make install
```

**_3、下载并安装Tsung_**

```bash
# wget http://tsung.erlang-projects.org/dist/tsung-1.4.2.tar.gz
# tar -zxvf tsung-1.4.2.tar.gz
# cd tsung-1.4.2
# ./configure --prefix=/usr/local/tsung --with-erlang=/usr/local/erlang
# make
# make install
```

**_4、下载并安装perl Template,用于生成报告模版_**

```bash
# wget http://cpan.org/modules/by-module/Template/Template-Toolkit-2.24.tar.gz
# tar -zxvf Template-Toolkit-2.24.tar.gz
# cd Template-Toolkit-2.24
# perl Makefile.PL
# make
# make test
# make install
```

**_5、下载并安装gnuplot,用于聊天生成_**

```bash
# yum install -y gnuplot gd libpng zlib
```

**_6、安装成后添加erlang、tsung环境变量_**

```bash
# vim /etc/profile
export PATH=$PATH:/usr/local/erlang/bin:/usr/local/tsung/bin
:x保存,退出
# source /etc/profile
不报错则成功
# tsung -v
# erl -v
```

**_7、测试基本http请求_**

```bash
复制基本的http压测配置到自定义的目录下
# cp /usr/local/tsung/share/tsung/example/http_example.xml /home/test/tsung.xml
创建日志生产目录
# mkdir /home/test/log
# tsung -f /home/test/tsung.xml -l /home/test/log/ start
生产html格式的报告
# /usr/local/tsung/lib/tsung/bin/tsung-stats.pl --stats /home/test/log/执行日期时间/tsung.log
```


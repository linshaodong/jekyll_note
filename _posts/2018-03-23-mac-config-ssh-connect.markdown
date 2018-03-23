---
layout: post
title:  "mac系统终端配置ssh连接远程服务器"
date:   2016-05-22 04:10:03 +0700
categories: [python, codefights]
---

mac系统终端配置ssh连接多台远程服务器

**_1、生成ssh-key_**

```bash
$ ssh-keygen -t rsa -C 'lianginet@gmail.com'
```

**_1、复制到服务器_**

```bash
$ scp ~/.ssh/id_rsa.pub user@hostname:~/.ssh/
```

**_1、登录到服务器_**

```bash
$ cd ~/.ssh
$ cat id_rsa.pub >> authorized_keys
```

**_1、本地配置**

```bash
$ vim ~/.ssh/config
# 输入以下内容
Host          alias     # 别名
HostName      hostname  # ip或者域名
Port          22        # 默认22，根据实际填写
User          root      # 登录用户名
IdentityFile  ~/.ssh/id_rsa # 公钥文件对应的私钥
# 若是有其他服务器，则空一行，添加新的服务器信息
```

**_1、登录**

```bash
$ ssh alias
```
---
layout: post
title:  "Elasticsearch + kibana + marvel安装"
date:   2016-05-22 04:10:03 +0700
categories: [python, codefights]
---

**下载解压指定$VERSION版本的zip包，解压即可。(<a href="www.elasticsearch.org/downloads">直接下载包地址</a>)**

```
curl -L -O http://download.elasticsearch.org/PATH/TO/VERSION.zip
unzip elasticsearch-$VERSION.zip
cd  elasticsearch-$VERSION

```

**Elasticsearch安装license和marvel-agent。**

```
./bin/plugin install license 
./bin/plugin install marvel-agent 

```

**下载解压指定系统的kibana包，解压即可。(<a href="https://www.elastic.co/downloads/kibana">直接下载包地址</a>)**
>注意：一定要先启动ES（启动方法为bin目录下的elasticsearch）,否则kibana启动不了（kibana启动方法：bin目录下的kibana）

进入kibana目录下执行以下代码

```
./bin/kibana plugin --install elasticsearch/marvel/latest

```

访问http://localhost:5601
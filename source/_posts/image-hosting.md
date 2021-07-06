---
title: 腾讯云 COS+CDN 作图床
date: 2021-06-30 09:35:20
tags:
comments: false
nowshow: true
---

{%note warning%}请勿滥用公共资源，请勿jsDelivr CDN 加速GitHub仓库作图床（[具体政策](https://www.jsdelivr.com/terms/acceptable-use-policy-jsdelivr-net)）{%endnote%}

# 主要思路
使用[PicGo](https://molunerfinn.com/PicGo/)，将图片上传至腾讯云COS，再利用CDN访问COS，提高速度（降低COS费用）。使用效果：
[测试图片](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706133820.jpg)

<!-- more -->

# 腾讯云配置
## COS配置
[创建](https://console.cloud.tencent.com/cos5/bucket)一个用于存放静态文件的COS储存桶，名称符合规定，选择`私有读写`，降低恶意访问的流量消耗
![创建存储桶](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706143149.png)
## CDN配置
选择刚刚创建的桶，点击左侧`域名管理与传输管理-默认CDN加速域名`,编辑即可，务必开启**回源鉴权**
![默认 CDN 加速域名](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706144646.png)

# PicGo配置
在[这里](https://github.com/Molunerfinn/PicGo/releases)选择对应操作系统`release`下载发行版
安装并打开PicGo，在`图床设置`处配置腾讯云COS图床，详细参考[官方配置手册](https://picgo.github.io/PicGo-Doc/zh/guide/config.html#%E8%85%BE%E8%AE%AF%E4%BA%91cos)，在自定义域名处填写CDN地址即可实现通过CDN访问COS
![腾讯云COS图床](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706145432.png)


# 结语
创建 腾讯云COS，并开启CDN，填入 PicGo 配置即可完成。
* COS，CDN的钱该花得花
* 使用 PicGo 能够将上传图片到 腾讯云COS，并直接获取 CDN 的加速后的图片地址，直接可以得到markdown格式，方便快捷。


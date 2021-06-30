---
title: jsDelivr CDN加速GitHub图床
date: 2021-06-30 09:35:20
tags:

---

{%note info%}“jsDelivr 是中国大陆唯一一家拥有合法ICP备案的公共CDN服务提供商”（[官方介绍](https://www.jsdelivr.com/network)）{%endnote%}

# 主要思路
使用[PicGo](https://molunerfinn.com/PicGo/)，将图片上传至GitHub，再利用jsDelivr CDN加速图片访问速度。使用效果：[测试图片](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210630104209.jpg)

<!-- more -->

# GitHub配置
[创建](https://github.com/new)一个用于存放静态文件的仓库，在[这里](https://github.com/settings/tokens)创建一个用于管理图片的`token`
![创建token](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210630105509.png)

勾选 `repo`，生成并复制`token`，后续填入[PicGo配置](#PicGo配置)
![勾选权限](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210630105548.png)

# PicGo配置
在[这里](https://github.com/Molunerfinn/PicGo/releases)选择对应操作系统`release`下载发行版
安装并打开PicGo，在`图床设置`处配置GitHub图床
![GitHub 图床设置](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210630105658.png)

## 设定仓库名
填入你上面创建的仓库名，格式为：用户名/仓库名；
## 设定分支名
GitHub 默认分支为`main`；
## 设定 Token
将 [Github 配置](#GitHub配置)中得到的 `token` 粘贴进去；
## 指定存储路径
你想要把图片放在仓库的哪个位置
## 设置自定义域名
`https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main`，其中：
* gh 表示来自 GitHub 的仓库
* Lusk-Liu/GitHub-hosting 表示仓库的具体位置
* main 表示 仓库的分支
上传成功后，图片链接形式如下：
`https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210630104209.jpg`

# 结语
创建 GitHub 仓库，并获取 token，填入 PicGo 配置即可完成。
* 使用 jsDelivr 加速静态文件访问，优化体验。
* 在 GitHub 存储图片，free（1024MB）。
* 使用 PicGo 能够将上传图片到 Github，并直接获取 jsDelivr 的加速后的图片地址，直接可以得到markdown格式，方便快捷。


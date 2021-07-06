---
title: Blog自定义域名
date: 2021-06-30 16:52:42
tags:
comments: false
---

# 前期准备
* 自有域名

# 主要思路
通过GitHub pages `custom domain`设置自定义域名
<!--more-->

# 域名解析设置
在域名注册商管理处添加两条`CNAME`解析记录，名称（主机记录）分别是`www`和`@`，内容（记录值）填写GitHub pages地址
![域名解析设置](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706141317.png)

# GitHub配置
在blog对应仓库`setting`页面`Pages`选项卡中，填入自有域名（国内域名商注册域名需备案），域名前不加`www`
![自定义域名设置](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706141326.png)

勾选`Enforce HTTPS` 将强制开启HTTPS访问，若开启需注意hexo主题中静态文件引用是否通过HTTPS

点击`save`后GitHub将自动生成一个`CNAME`文件，文件内容为自有域名

# hexo设置
使用自有域名后，blog根目录将变为`custom-domain.xxx/`，需将`_config.yml`-`root`修改为`/`
![根目录修改](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706141346.png)

由于blog使用自动化部署方案，GitHub custom domain生成的CNAME文件会被覆盖，需在`_config.yml`-`skip_render`中添加`CNAME`忽略对`CNAME`文件的渲染
![忽略渲染](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706141358.png)

# 小结
通过自有域名将GitHub pages访问方式个性化、便捷化，域名解析生效后（1-24小时）以后即可通过自有域名访问博客


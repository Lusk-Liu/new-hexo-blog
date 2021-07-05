---
title: Hexo更换NexT主题并启用CDN加速
date: 2021-07-05 13:22:24
tags:
comments: false
---

# 前期准备
* [Google Chrome](https://www.google.com/chrome/), [Microsoft Edge based on Chromium](https://support.microsoft.com/en-us/microsoft-edge/download-the-new-microsoft-edge-based-on-chromium-0f4a3dd7-55df-60f5-739f-00010dba52cf)等chromium浏览器
* [Lighthouse插件](https://chrome.google.com/webstore/detail/lighthouse/blipmdconlkpinefehnmjammfjpmpbjk)

# 主要思路
* 使用[jsDelivr](https://www.jsdelivr.com/)加速GitHub Pages仓库中的使用到的静态资源
* 开启`minify`,`preconnect`等特性加快页面加载
<!--more-->

# 安装NexT主题
```bash
cd hexo-blog # 跳转至hexo-blog目录
npm install hexo-theme-next # npm直接安装
```
# 自定义NexT主题配置
{%note info%}NexT[推荐](https://theme-next.js.org/docs/getting-started/configuration.html)使用`Hexo`中的`主题配置代理文件`[特性](https://hexo.io/docs/configuration.html#Using-an-Alternate-Config){%endnote%}
## 使用主题配置代理文件
```bash 
cd hexo-blog # 跳转至hexo-blog目录
cp node_modules/hexo-theme-next/_config.yml _config.next.yml # 将主题复制到 hexo-blog目录下并重命名
```
## 修改NexT主题配置
为加速blog访问，修改或启用如下配置：
### 启用minify
启用minify用于压缩合并JavaScript和CSS文件
![minify](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210705144725.png)

### 修改favicon路径
原路径为GitHub Pages地址，可使用jsDelivr加速
![favicon](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210705144847.png)

### 启用preconnect
启用preconnect以在一个 HTTP 请求正式发给服务器前预先执行一些操作，包括 DNS 解析，TLS 协商，TCP 握手
![preconnect](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210705145033.png)

### 启用lazyload
启用lazyload增加图片懒加载特性以降低[FCP](https://developer.mozilla.org/en-US/docs/Glossary/First_contentful_paint)
![lazyload](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210705145333.png)

### vendors设置
{%note warning%}当你使用最新版NexT时请勿修改`internal`配置{%endnote%}
可在此统一修改第三方插件CDN，默认为jsDelivr
![vendors](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210705150613.png)

### 修改assets路径
将NexT使用的JavaScript、CSS、Images通过jsDelivr加速
![assets](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210705152154.png)

# 效果对比
使用[Lighthouse](https://developers.google.com/web/tools/lighthouse)对前端页面进行审查
## NexT默认配置
NexT默认配置前端页面加载情况如下：
![默认配置-DevTools](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210705152606.png)
![默认配置-Lighthouse](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210705152651.png)

自定义NexT配置后前端页面加载情况如下：
![自定义配置-DevTools](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210705153130.png)
![自定义配置-Lighthouse](https://cdn.jsdelivr.net/gh/Lusk-Liu/GitHub-hosting@main/blog/img20210705153147.png)

# 结语
* 使用NexT主题并自定义NexT配置，优化访问体验。


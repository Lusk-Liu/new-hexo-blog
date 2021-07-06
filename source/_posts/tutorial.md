---
title: Blog自动化部署
date: 2021-06-29 13:25:20
tags:
comments: false

---

# 前期准备

* 本地安装 [node.js](https://nodejs.org/zh-cn/)
* 本地安装[git](https://git-scm.com/)
* [GitHub账号](https://github.com/signup?user_email=&source=form-home-signup)
* [GitHub仓库](https://github.com/new)
* [Travis CI账号](https://travis-ci.com/)

<!-- more -->

## 本地安装node.js
npm设置阿里源，加快国内访问速度
```bash
npm config set registry https://registry.npm.taobao.org/
```
检查是否设置成功
```bash
npm config get registry
```

## 本地安装git
检查Git是否安装成功
```bash
git --version
```
设置Git用户名和邮箱
```bash
git config --global user.name "用户名" 
git config --global user.email "邮箱"
```
## GitHub账号
本地生成`RSA`密钥
```bash
ssh-keygen -t rsa -b 4096 -C "邮箱"
```
**回车三次**

查看rsa公钥信息
```bash
cat ~./.ssh/id_rsa.pub
```
将公钥信息添加到[GitHub SSH Keys](https://github.com/settings/ssh/new)

##  GitHub仓库
{%note warning%} 新建一个**仓库名称！==用户名**的**Public**仓库{%endnote%}

##  Travis CI
{%note warning%} 2021-06-15后 应使用 [travis-ci.com](https://www.travis-ci.com/) {%endnote%}
1. 使用GitHub账号[登录](https://travis-ci.com/signin)
2. 在[这里](https://travis-ci.com/account/repositories)同步账户
![Travis 同步账户](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706141011.png)

# hexo
## 安装hexo
使用`terminal/cmd`安装
```bash 
npm install -g hexo-cli
```
验证hexo安装
```bash
hexo -v
```
## 使用hexo搭建博客
在**当前目录**下生成一个名为`new-hexo-blog`的新目录
```bash
hexo init new-hexo-blog
cd new-hexo-blog
npm install
```
`new-hexo-blog`目录如下
```bash
. 
├── _config.yml 
├── package.json 
├── node_modules 
├── scaffolds 
├── source 
|	├── _drafts 
|	└── _posts 
└── themes

```

`_config.yml`：`站点配置文件`
`scaffolds`：存放新建文章的模板文件
`source `：资源文件夹

在`new-hexo-blog`目录下运行命令
```bash
hexo server #默认使用4000端口
#hexo server -p 8000 #使用-p 参数更换其他接口
```
打开`http://localhost:4000`即可访问

# 部署到GitHub Pages
{%note info%}本次使用Travis CI自动部署方案，需要将源文件和生成的网页静态文件放在**同一仓库**的**不同分支**，源文件放在`main`分支，静态文件放在`gh-pages`分支{%endnote%}

## GitHub配置
将本地文件推送至GitHub
```bash
cd new-hexo-blog
git init
git add .
git commit -am "init blog"
git remote add origin blog仓库地址
git push -u origin main # GitHub默认分支
#git push -f -u origin main # -f 强制推送，会删除原有数据，慎用
```
创建新本地分支`gh-pages`并关联远程分支
```bash
git checkout -b gh-pages # hexo内置分支名为gh-pages，不要修改
git push -u origin gh-pages
```
在项目`Settings`页面`Pages`tab中选择`gh-pages分支`

## hexo配置

修改`new-hexo-blog`目录下的`hexo`的配置文件(`_config.yml`)
```yml
url: https://lusk-liu.github.io/new-hexo-blog/ # Pages页面提供的地址
root: /new-hexo-blog/ 
deploy: 
  type: 'git' 
  repo: git@github.com:Lusk-Liu/new-hexo-blog.git # 设置为仓库地址
  branch: gh-pages
```
安装`hexo-deployer-git`
```bash
cd new-hexo-blog
npm install hexo-deployer-git --save
```
生成网页静态文件并部署
```bash
hexo clean && hexo generate
hexo deploy
# hexo clean && hexo g -d # 等效前两行
```
将文件推送至`main`分支保存，以备份和多设备编辑
```bash
git checkout main
git add .
git commit -am "commit message"
git push
```
# 使用Travis CI进行自动化部署
注释`new-hexo-blog`目录下的`hexo`的配置文件(`_config.yml`)中`repo`信息
```yml
deploy: 
  type: 'git' 
  # repo: git@github.com:Lusk-Liu/new-hexo-blog.git # 设置为仓库地址
  branch: gh-pages
```
在`new-hexo-blog`目录下创建`.travis.yml`文件，与`_config.yml`文件同级
```yml
sudo: false 
language: node_js 
node_js: 
  - 14 # node.js版本，最好与本地版本保持一致
cache: npm 
branches: 
  only: 
  - main # 只build main分支 
script: 
  - hexo generate 
deploy: 
  provider: pages 
  skip-cleanup: true 
  github-token: $GH_TOKEN # Travis环境变量
  keep-history: true 
  on: 
    branch: main 
  local-dir: public
```

`Travis`正确关联`GitHub`账号后，[这里](https://travis-ci.com/dashboard)会出现仓库信息
![Travis Dashboard](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706141038.png)

在[这里](https://github.com/settings/tokens)生成一个新的`token`以供`Travis`使用
![生成token](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706140532.png)

在`travis`中对应blog仓库的`settings - Environment Variables `中填入`token`
![对应blog仓库](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706141059.png)

![环境变量配置](https://blog-res-1254383992.file.myqcloud.com/blog/img/20210706141111.png)
新建一篇blog，然后推送到GitHub
```bash
cd hexo-new-blog
git checkout main 
hexo new "my first blog" 
git add . 
git commit -am"add a new blog" 
git push
```
`Travis CI`将自动build，等待一会即可完成部署。
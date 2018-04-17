---
title: '使用hexo，next主题重建博客'
date: 2017-02-23 16:43:25
tags:
---

### 第一步：在github中建立新项目

**这里只需要注意一点，项目名格式必须是github昵称.github.io**

### 第二步：clone项目到本地

### 第三步：安装hexo，务必参考[官方教程](https://hexo.io/zh-cn/docs/)，非常详细，少走弯路

### 第四步：安装next主题，务必参考[官方教程](http://theme-next.iissnan.com/)，非常详细，少走弯路

记住hexo常用命令，用于调试

1. `hexo new [layout] <title>`
2. `hexo generate`，也可以用 `hexo g`，生成静态文件
3. `hexo server`，也可以用 `hexo s`，启动服务器，用于本地测试
4. `hexo deploy`，发布，需要在config文件中配置github地址，其实就是把生成的静态文件推送到github
5. `hexo clean`，清除缓存文件
6. `hexo list post`，列出post下的所有文件详细信息

**推荐一个mac上的markdown工具Typora，谁用谁知道**

网上有很多教程介绍如何搭建博客，多多少少都会有瑕疵，最后还是强烈建议阅读官方文档。
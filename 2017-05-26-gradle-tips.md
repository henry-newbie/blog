---
title: gradle配置小技巧
date: 2017-05-26 15:52:16
tags:
---

1. #### gradle extra

   描述问题：每次发布app新版本都会更改gradle配置文件中的versionCode和versionName，改完as就会提示我们gradle配置更改了需要sync。

   解决问题：新建config.gradle文件，
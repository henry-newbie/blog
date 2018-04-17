---
layout: post
title: 2月份和三月份碰到的问题总结
date: 2016-03-01
categories: blog
tags: [技术]
description: 问题总结
header-img: "img/green.jpg"
---

## 吐槽自己

一个月没写东西，吐槽下自己太懒了，不过也存在其他原因啦，好家长3.2版本需求太多，一直忙的没停下来（不要为自己的懒找借口了），坚持坚持，一定要坚持。

## 问题总结

- mob的分享问题

新浪微博的分享：由于分享到新浪微博的时候分享的内容都是在content里面，所有如果要分享url也需要放在content里面，但是同样的内容分享到其他平台的时候有不能放到content里面，所以要对新浪微博单独处理，在PlatformListFakeActivity里面的onShareButtonClick方法进行处理，判断如果是新浪微博，就把分享的文字内容和url都放到content里面。

- 如何监听webview中url的变化

WebViewClient类的shouldOverrideUrlLoading和onPageStarted方法，在shouldOverrideUrlLoading中进行重定向的处理。

- android webview js交互， 响应webview中的图片点击事件

思路：1：点击图片的时候h5中的js回调java方法，并传回图片的url

2：添加一个显示图片的遮罩层来显示图片

[具体实现](http://blog.csdn.net/zzf112/article/details/19618101)

- fresco加载gif动画

首先gif文件和png一样要放大drawable文件夹下，但是gif动画是连续播放的（虽然在制作的时候可以设置只播放一次），我们需要gif动画只播放一遍，fresco没有给出方法来控制，所以我们自定义了一个定时器，播放固定的时间。

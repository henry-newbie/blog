---
title: 优化应用启动时间
date: 2017-03-17 16:29:26
tags:
---

- #### 优化应用启动时间

启动方式分两种：冷启动（重新创建进程，启动时间较长），热启动（后台已保留有进程，不走application的生命周期）。

冷启动流程：Aplication构造方法—》attachBaseContent—》onCreate—》activity构造方法—》onCreate—》渲染主题背景等属性—》onStart—》onResume—》measure—》layout—》draw

##### 测试启动时间

adb shell am start -W [packageN

```
adb shell am start -W [packageName]/[packageName.MainActivity]
```

##### 减少应用启动耗时

Application的onCreate方法中不要进行耗时操作，MainActivity中sp初始化数据太多不要放在主线程操作。

##### 优化应用启动时的体验

欢迎界面的activity主题背景设置颜色或图片，这个背景会在显示第一帧前提前显示出来

```
<style name="AppTheme.Launcher">
    <item name="android:windowBackground">@drawable/bule</item>
</style>
```


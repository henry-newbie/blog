---
title: 权限
date: 2017-09-27 17:19:37
tags: 
---

#### targetSdkVersion

CompileSdkVersion和minSdkVersion都容易理解，但targetSdkVersion的作用是什么呢？官方解释：

> targetSdkVersion is the main way Android provides forward compatibility

其实就是为了解决系统为了向前兼容的问题；

举个例子：android N（6.0）增加了运行时权限的功能，为了解决6.0系统之前的兼容问题，会判断targetSdkVersion是否小于23，是的话就会默认给应用需要的全部权限，否的话就会执行新的运行时权限规则；

#### 运行时权限

android6.0（api23）才增加的新功能；

权限分为正常权限和危险权限；

###### 检查权限：

api23之后：

```Java
// Assume thisActivity is the current activity
int permissionCheck = ContextCompat.checkSelfPermission(thisActivity,
        Manifest.permission.WRITE_CALENDAR);
```

api23之前：

```java
int permissionCheck = PermissionChecker.checkSelfPermission(this, PERMISSION);
```

经试验，在anroid6.0以下系统中使用ContextCompat.checkSelfPermission方法无论有没有权限都是返回true，所以应使用v4包中的PermissionChecker.checkSelfPermission方法；

###### 请求权限：

activity：

```Java
ActivityCompat.requestPermissions(this, new String[]{PERMISSION}, REQUEST_CODE);
```

fragment:

```Java
fragment.requestPermissions(this, new String[]{PERMISSION}, REQUEST_CODE);
```

子fragment：

```java
getParentFragment.requestPermissions(this, new String[]{PERMISSION}, REQUEST_CODE);
```

在子fragment中使用requestPermissions，onRequestPermissionsResult不会接收回调，所以使用父fragment的requestPermissions方法，然后在父fragment中透传给子fragment。

```java
@Override
  public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
      super.onRequestPermissionsResult(requestCode, permissions, grantResults);
      List<Fragment> fragments = getChildFragmentManager().getFragments();
      if (fragments != null) {
          for (Fragment fragment : fragments) {
              if (fragment != null) {
                  fragment.onRequestPermissionsResult(requestCode,permissions,grantResults);
              }
          }
      }
  }
```

#### 注意事项

app的targetSdkVersion小于23，在android6.0及以上系统上运行时，如果在设置中改变应用权限状态，app的每个界面都会重新创建；在android6.0以下运行时，由于系统中没有权限选项，不存在该问题。

app的targetSdkVersion大于等于23，在6.0及以上运行时，会按照运行时权限规则执行；在6.0以下运行时，会默认获得app需求的全部权限。

设置系统亮度和音量不需要权限；

华为和小米的系统在api23（6.0）一下时也会询问权限，但经过测试，小米上的权限管理貌似不起作用。
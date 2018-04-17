---
title: 使用TableLayout遇到的坑
date: 2017-03-17 11:12:13
tags:
---

- #### 前请概要：

项目中用到用TableLayout画表格，遇到不少坑，总结一下。

- #### 行和列match_parent无效果

为row何column设置match_parent没有效果，和wrap_content一样，但可以设置固定尺寸，如果要想match_parent有两种办法，1：设置weight	2：设置stretchColumns；需要注意设置stretchColumns之后，divider效果就会出问题（end不显示），尽量不要使用stretchColumns。

- #### layout_span的问题

wrap_content和layout_span配合起来没问题，但match_parent配合layout_span就达不到理想效果，推荐用weight来实现match_parent的效果

- #### divider的问题

因为TableLayout是继承LinearLayout，所以也是支持showDividers属性的，正常使用没什么问题，但是和stretchColumns属性配合使用会导致end不显示分割线。
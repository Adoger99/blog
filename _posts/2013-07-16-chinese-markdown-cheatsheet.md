---
layout: post
title: Markdown语法简介
date: 2013-07-16
Author: 邶城花海 
tags: [效率]
comments: true
toc: true
---

[Markdown语法](http://daringfireball.net/projects/markdown/syntax)。下面整理的这些为了方便写博客时参考。

## 标题

```
#       一级标题
##      二级标题
###     三级标题
####    四级标题
#####   五级标题
######  六级标题
```
#       一级标题
##      二级标题
###     三级标题
####    四级标题
#####   五级标题
######  六级标题

## 引用
```
> 引用一段文字 
```
> 笛卡儿曾经提到过，读一切好书，就是和许多高尚的人谈话。带着这句话，我们还要更加慎重的审视这个问题： 现在，解决标记语言的问题，是非常非常重要的。 
## 列表

```
*   无序列表
+   无序列表
-   无序列表
```
*   无序列表
*   无序列表
*   无序列表

```
1.  有序列表
2.  有序列表
3.  有序列表
```
1.  有序列表
3.  有序列表
2.  有序列表
## 代码块

```java
import java.utils
```

## 横线
```
* * *
```
* * * * *
## 链接
```
[链接文字](链接地址 "链接描述") 
例如 [Google](http://google.com/ "Google")，[Yahoo](http://search.yahoo.com/ "Yahoo Search")，[MSN](http://search.msn.com/ "MSN Search").
```
[链接文字](链接地址 "链接描述") 
例如 [Google](http://google.com/ "Google")，[Yahoo](http://search.yahoo.com/ "Yahoo Search")，[MSN](http://search.msn.com/ "MSN Search").
## 强调
```
*斜体* _斜体_
**粗体** **粗体**
***又粗又斜***
```
*斜体* _斜体_

**粗体** **粗体**

***又粗又斜*** ___又粗又斜___

## 图片
```
![替代文字](图片url "图片说明")
```
![img](/images/designpatterns0.png "设计模式")
## 转义字符

如果需要使用以上标记字符而不被Markdown理解为格式标记，需要用`\`转义：例如`\\`，效果为\\。

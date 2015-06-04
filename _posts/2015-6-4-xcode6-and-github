---
layout: post
title: xcode6使用Github进行版本控制
---

学习编程第一步首先要养成好习惯，而对源代码进行版本控制就是一个良好的编程习惯
xcode自从5.x开始已经集成git控制。可以使用图形化方式对项目进行管理。

### 使用Github

本文参考《Xcode版本控制Git及在GitHub/Oschina提交项目》[传送门](http://m.blog.csdn.net/blog/g1jun/25422953)一文。
原文已经介绍得十分详细了。这里我就不重复。你可以参考上述链接尝试。

### 一些问题

这里笔者遇到一个问题，就是当使用界面提交时会一直“Perpare to push”。 通过查看stackoverflow相关问题[传送门](http://stackoverflow.com/questions/11968353/cannot-push-to-remote-git-repository)
找到解决方案。 这里列出我解决的方法，通过命令行完成：

```
cd 【GIT仓库】
git config http.postBuffer 524288000
git config --global push.default simple
git push
【输入用户名】
【输入密码】
```
刷新Github对应仓库页面[传送门](https://github.com/summit4you/BID)，就可以发现刚提交的代码。
上述链接是我阅读《Beging Iphone Development Exploring the ios SDK》一书完成的源代码，持续更新。


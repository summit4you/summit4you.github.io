---
layout: post
title: 使用Jekyll构建个人博客!
---

今天，参考一篇外文在Github.io上面创建个人博客。[原文传送门](http://www.smashingmagazine.com/2014/08/01/build-blog-jekyll-github-pages/)。这外文是采用fork直接在Github上面部署，比在本地更新，然后提交方便多了。

步骤如下：

- 首先，fork [Jekyll now](https://github.com/barryclark/jekyll-now)
- 然后，修改位于根目录下的_config.yml文件
![_config.yml]({{ site.baseurl }}/images/config.png)
- 进入/_post/目录，修改并更新Hello World的markdown文件

笔者在构建时，总出现404错误。后来才发现，原来构建时需要已验证邮箱。


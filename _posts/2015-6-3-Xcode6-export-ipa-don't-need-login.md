---
layout: post
title:  Xcode6导出ipa时绕过登入开发帐号简易方法
---

xcode6新版本在Archive中导出ipa时会要求登入并选择相关的Apple开发账号

![导出需要登入开发者帐号](http://blog.k-res.net/wp-content/uploads/2014/10/111-300x181.png)

本文介绍了一种绕过必须登陆开发者帐号的简易方法

# 使用命令行 #

文章[《Xcode 6导出ipa时必须登入开发账号的绕过方法》](http://blog.k-res.net/archives/1761.html) 使用命令行方式
绕过。但是当工程比较大时，项目依赖多，使用命令行编译就显得复杂和麻烦

# 折衷方案 #

本文提出一种图形化操作和命令行结合的方法：

- 使用xcode6图形化操作生成Archive
- 通过finder找到生成的Archive文件
- 把Archive拷贝至工程文件下
- 执行以下命令行

{% highlight ruby linenos %}

`xcodebuild -exportArchive -archivePath $projectname.xcarchive -exportPath $projectname -exportFormat ipa -exportProvisioningProfile “Provisioning Profile Name”`

{% highlight ruby linenos %}

- 在工程文件下得到ipa文件

# 小结 #

本方法比单纯使用命令行便简单易行。如果你有更好的解决方法，请联系我。


---
layout: post
title: 通过Gmail使用Python发送邮件
---

很多时候用户运行程序，我们是无法得知出错信息。因此，健壮的应用应该提供bug上报机制。那么问题来了？怎么发送邮件呢？

### 选择Gmail

经过一天的使用心得，GMail是最理想的免费邮箱。因为，因内很多邮箱现在已经不直接支持SMTP。而sendCould对SMTP的支持也不太好。
当然使用GMail的一个最大问题就是要翻墙注册，而程序发送邮件是不受限的。

### smtplib

smtplib是python的一个smtp发送邮件库，使用十分简单。下面就给出相关的实例，不详细解释，有兴趣的可以查看相关的文档。

```
# -*- coding: utf-8 -*-
"""
Created on Tue Jul 07 10:10:57 2015

@author: Administrator
"""


import smtplib
from email.MIMEMultipart import MIMEMultipart
from email.MIMEText import MIMEText
from email.MIMEBase import MIMEBase
from email import encoders

try:
	fromaddr = 'summit.qiu@gmail.com'
	toaddrs  = '809104518@qq.com'
	msg = "\r\n".join([
	  "From: user_me@gmail.com",
	  "To: user_you@gmail.com",
	  "Subject: Just a message",
	  "",
	  "Why, oh why"
	  ])
	username = '邮箱名'
	password = '密码'
	#password = 'abc12345'
	server = smtplib.SMTP('smtp.gmail.com:587')
	server.ehlo()
	server.starttls()
	server.ehlo()
	server.login(username,password)
	server.sendmail(fromaddr, toaddrs, msg)
	server.close()
except Exception as e:
	print e
```

### 注意事项

单纯运行上面的代码会出现错误

```
SMTPAuthenticationError: (534, '5.7.9 Please log in with your web browser and then try again. Learn more at\n5.7.9 https://support.google.com/mail/bin/answer.py?answer=78754 qo11sm4014232igb.17 - gsmtp')
```

这是出于安全考虑，google禁用了明文的第三方应用登陆。解决方法如下：

- 在[登录 Google](https://myaccount.google.com/security?utm_source=OGB#signin)里找到[二步认证](https://accounts.google.com/b/0/SmsAuthConfig?hl=zh_CN?utm_source=OGB)
- 启用二步认证
- 为你的第三方应用，选择【其它类型】， 增加一个安全密码。
- 通过使用安全密码，替换原来代码中password的值

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/smtplib-res.png)

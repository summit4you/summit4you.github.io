---
layout: post
title: python(x,y)安装SimpleITK及入门
---

python(x,y)是基于Python编程语言免费的科学与工程开发软件。当前引入强大的Spyder集成开发环境。本文主要结合作者研究方向，说明python(x,y)的使用。python(x,y)包含丰富的科学可视化，但是并不包含像SimpleITK这类强大的图像开发包。下面通过SimpleITK说明如何在Python(x,y)安装
新的python库。

### SimpleITK的安装

打开，IPython，在提示符下使用pip安装SimpleITK，

![SimpleITK在Python(x,y)的安装](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SimpleITK.jpg)

更多有关SimpleITK的安装，请参见[传送门](http://www.itk.org/Wiki/SimpleITK/GettingStarted#Python_installation)

### 测试SimpleITK

打开Spyder，输入以下测试代码

```
	# -*- coding: utf-8 -*-
	"""
	Spyder Editor

	This is a temporary script file.
	"""

	import SimpleITK as sitk

	image = sitk.Image( 256, 256, 256, sitk.sitkInt16 );
	twoD = sitk.Image( 64, 64 , sitk.sitkFloat32 )
	print "hello world", twoD
```

- sitk是对应的模块
- Image是图像类的构造函数

点击运行, 得到如下输出结果：

```
hello world Image (0CF59640)
  RTTI typeinfo:   class itk::Image<float,2>
  Reference Count: 1
  Modified Time: 903
  Debug: Off
  Object Name: 
  Observers: 
    none
  Source: (none)
  Source output name: (none)
  Release Data: Off
  Data Released: False
  Global Release Data: Off
  PipelineMTime: 0
  UpdateMTime: 0
  RealTimeStamp: 0 seconds 
  LargestPossibleRegion: 
    Dimension: 2
    Index: [0, 0]
    Size: [64, 64]
  BufferedRegion: 
    Dimension: 2
    Index: [0, 0]
    Size: [64, 64]
  RequestedRegion: 
    Dimension: 2
    Index: [0, 0]
    Size: [64, 64]
  Spacing: [1, 1]
  Origin: [0, 0]
  Direction: 
1 0
0 1

  IndexToPointMatrix: 
1 0
0 1

  PointToIndexMatrix: 
1 0
0 1

  Inverse Direction: 
1 0
0 1

  PixelContainer: 
    ImportImageContainer (133E9D98)
      RTTI typeinfo:   class itk::ImportImageContainer<unsigned long,float>
      Reference Count: 1
      Modified Time: 904
      Debug: Off
      Object Name: 
      Observers: 
        none
      Pointer: 13580770
      Container manages memory: true
      Size: 4096
      Capacity: 4096
```
### 像素操作

```
# Addressing pixels
image . GetPixel ( 0 , 0 , 0 )
image . SetPixel ( 0 , 0 , 0 , 1 )
image . GetPixel ( 0 , 0 , 0 )

```

可以使用下标方式简写

```
image [ 0 , 0 , 0 ]
image [ 0 , 0 , 0 ] = 10

```

### 显示图像

```
sitk.Show( twoD )
```

注：此函数需要在系统已安装[ImageJ](http://rsb.info.nih.gov/ij/download.html)的环境下才能调用成功，否则会提示

> Error in administering child process

运行后显示如下图所示：

![SimpleITK-SHOW](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SimpleITK-SHOW.png)
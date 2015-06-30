---
layout: post
title: SimpleITK入门--Python语法下的图像
---

Image Basics Notebook看起来与ITK C++接口一致（除了没有烦人的模板）。

糖果是一种好东西，它给你能量使得事情能够完成得更快！SimpleITK拥有丰富有力的
语义“糖果”来帮助你快速开发。

```
import SimpleITK as sitk
```

让我们开始开发一个简便的方法用来显示我们的图像。

```
img = sitk.GaussianSource(size=[64]*2)
imshow(sitk.GetArrayFromImage(img))
```

```
<matplotlib.image.AxesImage at 0x11d376910>
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image.jpg)

```
img = sitk.GaussianSource(size=[64]*2)
imshow(sitk.GetArrayFromImage(img))
```
```
<matplotlib.image.AxesImage at 0x11d3ada90>
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image2.jpg)

```
def myshow(img):
    nda = sitk.GetArrayFromImage(img)
    imshow(nda)
myshow(img)
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image3.jpg)

### 多维切片索引

如果你熟悉numpy，那么切片索引也应该适用于Simple image。Python对于1维对象的标准切片接口：

<table><tbody>
<tr><td>操作</td>  <td>结果</td></tr>
<tr><td>d[i]</td>   <td>ith item of d, starting index 0</td></tr>
<tr><td>d[i:j]</td> <td>slice of d from i to j</td></tr>
<tr><td>d[i:j:k]</td>   <td>slice of d from i to j with step k</td></tr>
</tbody></table>

通过这种简写，许多数值运算任何可以很容易完成

```
img[24, 24]
```

> 0.048901304602622986

### 裁剪


```
myshow(img[16:48,:])
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image4.jpg)

```
myshow(img[:,16:-16])
```
![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image5.jpg)

```
myshow(img[:32, :32])
```
![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image6.jpg)

### 翻转

```
img_corner = img[:32, :32]
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image6.jpg)

```
myshow(img_corner[::-1, :]) #左右翻转
```
![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image7.jpg)

```
myshow(sitk.Tile(img_corner, # (0,0)
                 img_corner[::-1,::], # (0, 1)
                img_corner[::,::-1], # (1, 0)
                img_corner[::-1,::-1],  # (1, 1)
                [2,2]))
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image8.jpg)

### 析取切片

可以从三维体数据中析取二维图像

```
img = sitk.GaborSource(size=[64]*3, frequency=0.05)

# Why does this produce an error?
myshow(img)
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image9.jpg)

```
TypeError                                 Traceback (most recent call last)
<ipython-input-12-a990f90669fe> in <module>()
      2 
      3 # Why does this produce an error?
----> 4 myshow(img)

<ipython-input-4-8b0cddf8dfc0> in myshow(img)
      1 def myshow(img):
      2     nda = sitk.GetArrayFromImage(img)
----> 3     imshow(nda)
      4 myshow(img)

/Users/blowekamp/.virtualenvs/sitkpy/lib/python2.7/site-packages/matplotlib/pyplot.pyc in imshow(X, cmap, norm, aspect, interpolation, alpha, vmin, vmax, origin, extent, shape, filternorm, filterrad, imlim, resample, url, hold, **kwargs)
   2890                         vmax=vmax, origin=origin, extent=extent, shape=shape,
   2891                         filternorm=filternorm, filterrad=filterrad,
-> 2892                         imlim=imlim, resample=resample, url=url, **kwargs)
   2893         draw_if_interactive()
   2894     finally:

/Users/blowekamp/.virtualenvs/sitkpy/lib/python2.7/site-packages/matplotlib/axes.pyc in imshow(self, X, cmap, norm, aspect, interpolation, alpha, vmin, vmax, origin, extent, shape, filternorm, filterrad, imlim, resample, url, **kwargs)
   7298                        filterrad=filterrad, resample=resample, **kwargs)
   7299 
-> 7300         im.set_data(X)
   7301         im.set_alpha(alpha)
   7302         self._set_artist_props(im)

/Users/blowekamp/.virtualenvs/sitkpy/lib/python2.7/site-packages/matplotlib/image.pyc in set_data(self, A)
    427         if (self._A.ndim not in (2, 3) or
    428             (self._A.ndim == 3 and self._A.shape[-1] not in (3, 4))):
--> 429             raise TypeError("Invalid dimensions for image data")
    430 
    431         self._imcache = None

TypeError: Invalid dimensions for image data
```

```
myshow(img[:,:,32])
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image10.jpg)

```
myshow(img[16,:,:])
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image11.jpg)

### 超采样

```
myshow(img[:,::3,32])
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image12.jpg)

### 数学运算

许多python数学运算通过调用SimpleITK滤波器重载，使得对每个像素执行对应的操作。这些操作有对两
张图像的二元操作也有对一个图像或图像标量的一元操作。如果两张图进行数学运算，必须确保它们具有相同的像素类型，输出的图像类型通常是一样的。
因为这些操作是基于ITK滤波器的，所以底层是原始的C++操作，因此要小心溢出和除数为0的情况。

操作包含有

- +
- -
- *
- /
- //
- **

```
img = sitk.ReadImage("cthead1.png")
img = sitk.VectorIndexSelectionCast(img, i, sitk.sitkFloat32)
myshow(img)
img[150,150]
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image13.jpg)

```
timg = img**2
myshow(timg)
print timg[150, 150]
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image14.jpg)

### 除法操作

python内置的__floordiv__, __truediv__ 和 __div__均有实现。

truediv输出一个double像素类型的图像。

参见[PEP 238](http://www.python.org/peps/pep-0238)了解为啥Python3改变除法运算

### 位运算

支持操作：

- &
- |
- ^
- ~

### 比较运算

支持操作：

- >
- >=
- <
- <=
- ==

比较运算遵循与SimpleITK相同的约定。像素类型为sitkUInt8， 值域为0或1.

### 使用比较运算完成阈值分割

```
myshow(img>90)
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image15.jpg)

```
myshow(img>150)
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image16.jpg)

```
myshow((img>90)+(img>150))
```

![运行结果](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SITK_Pythonic_Image17.jpg)
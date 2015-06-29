---
layout: post
title: SimpleITK入门--图像基础
---

欢迎来到第一个SimpleITK Notebook示例：

### SimpleITK图像基础

本文档将简要介绍SimpleITK图像类。
首先，我们导入SimpleITK Python模块。为了让我们导入的模块显得更简短，我们给一个本地的别名“sitk”。

```python
import SimpleITK as sitk
```

### 创建图像

有许多方式创建一个图像，所有图像的像素初始值为0.

```python
image = sitk.Image(256, 128, 64, sitk.sitkInt16)
image_2D = sitk.Image(64, 64, sitk.sitkFloat32)
image_2D = sitk.Image([32,32], sitk.sitkUInt32)
image_RGB = sitk.Image([128,128], sitk.sitkVectorUInt8, 3)
```

### 像素类型

像素类型表示为枚举类型。下表给出了枚举值对应的意思。

类型名  | 说明
------------- | -------------
sitkUInt8  | Unsigned 8 bit integer
sitkInt8  | Signed 8 bit integer
sitkUInt16  | Unsigned 16 bit integer
sitkInt16  | Signed 16 bit integer
sitkUInt32  | Unsigned 32 bit integer
sitkInt32  | Signed 32 bit integer
sitkUInt64  | Unsigned 64 bit integer
sitkInt64  | Signed 64 bit integer
sitkFloat32  | 32 bit float
sitkFloat64  | 64 bit float
sitkComplexFloat32  | complex number of 32 bit float
sitkComplexFloat64  | complex number of 64 bit float
sitkVectorUInt8  | Multi-component of unsigned 8 bit integer
sitkVectorInt8  | Multi-component of signed 8 bit integer
sitkVectorUInt16  | Multi-component of unsigned 16 bit integer
sitkVectorInt16  | Multi-component of signed 16 bit integer
sitkVectorUInt32  | Multi-component of unsigned 32 bit integer
sitkVectorInt32  | Multi-component of signed 32 bit integer
sitkVectorUInt64  | Multi-component of unsigned 64 bit integer
sitkVectorInt64  | Multi-component of signed 64 bit integer
sitkVectorFloat32  | Multi-component of 32 bit float
sitkVectorFloat64  | Multi-component of 64 bit float
sitkLabelUInt8  | RLE label of unsigned 8 bit integers
sitkLabelUInt16  | RLE label of unsigned 16 bit integers
sitkLabelUInt32  | RLE label of unsigned 32 bit integers
sitkLabelUInt64  | RLE label of unsigned 64 bit integers

还有一个类型为sitkUnknown，用于未定义或错误的像素ID。它的值为-1。当前并不支持64位。当值没意义时为sitkUnknown。

### 更多信息可以从Image类的Docstring获取

SimpleITK classes and functions 包含从C++定义和Doxygen文件生成的Docstrings。

```python
help(image)
```
获取SimpleITK.SimpleITK对象的Image帮助信息：


class Image(__builtin__.object)
 |  The main Image class for SimpleITK.
 |  
 |  C++ includes: sitkImage.h
 |  
 |  Methods defined here:
 |  
 |  CopyInformation(self, *args, **kwargs)
 |      CopyInformation(Image self, Image srcImage)
 |      
 |      Copy common meta-data from an image to this one.
 |      
 |      
 |      Copies the Origin, Spacing, and Direction from the source image to
 |      this image.
 |      
 |      It is required for the source Image's dimension and size to match, this image's attributes, otherwise an
 |      exception will be generated.
 |  
 |  GetDepth(self)
 |      GetDepth(Image self) -> unsigned int
 |  
 |  GetDimension(self)
 |      GetDimension(Image self) -> unsigned int
 |  
 |  GetDirection(self)
 |      GetDirection(Image self) -> VectorDouble
 |  
 |  GetHeight(self)
 |      GetHeight(Image self) -> unsigned int
 |  
 |  GetITKBase(self, *args)
 |      GetITKBase(Image self) -> itk::DataObject
 |      GetITKBase(Image self) -> itk::DataObject const *
 |  
 |  GetMetaData(self, *args, **kwargs)
 |      GetMetaData(Image self, std::string const & key) -> std::string
 |      
 |      Get the value of a meta-data dictionary entry as a string.
 |      
 |      
 |      If the key is not in the dictionary then an exception is thrown.
 |      
 |      string types in the dictionary are returned as their native strings.
 |      Other types are printed to string before returning.
 |  
 |  GetMetaDataKeys(self)
 |      GetMetaDataKeys(Image self) -> VectorString
 |      
 |      get a vector of keys in from the meta-data dictionary
 |      
 |      
 |      Returns a vector of keys to the key/value entries in the image's meta-
 |      data dictionary. Iterate through with these keys to get the values.
 |  
 |  GetNumberOfComponentsPerPixel(self)
 |      GetNumberOfComponentsPerPixel(Image self) -> unsigned int
 |      
 |      Get the number of components for each pixel.
 |      
 |      
 |      For scalar images this methods returns 1. For vector images the number
 |      of components for each pixel is returned.
 |  
 |  GetOrigin(self)
 |      GetOrigin(Image self) -> VectorDouble
 |  
 |  GetPixel(self, *idx)
 |      Returns the value of a pixel.
 |      
 |      This method takes 2 parameters in 2D: the x and y index,
 |      and 3 parameters in 3D: the x, y and z index.
 |  
 |  GetPixelAsComplexFloat64(self, *args, **kwargs)
 |      GetPixelAsComplexFloat64(Image self, VectorUInt32 idx) -> std::complex< double >
 |  
 |  GetPixelID(self)
 |      GetPixelID(Image self) -> itk::simple::PixelIDValueEnum
 |  
 |  GetPixelIDTypeAsString(self)
 |      GetPixelIDTypeAsString(Image self) -> std::string
 |  
 |  GetPixelIDValue(self)
 |      GetPixelIDValue(Image self) -> itk::simple::PixelIDValueType
 |  
 |  GetSize(self)
 |      GetSize(Image self) -> VectorUInt32
 |  
 |  GetSpacing(self)
 |      GetSpacing(Image self) -> VectorDouble
 |  
 |  GetWidth(self)
 |      GetWidth(Image self) -> unsigned int
 |  
 |  HasMetaDataKey(self, *args, **kwargs)
 |      HasMetaDataKey(Image self, std::string const & key) -> bool
 |      
 |      Query the meta-data dictionary for the existence of a key.
 |  
 |  SetDirection(self, *args, **kwargs)
 |      SetDirection(Image self, VectorDouble direction)
 |  
 |  SetOrigin(self, *args, **kwargs)
 |      SetOrigin(Image self, VectorDouble origin)
 |  
 |  SetPixel(self, *args)
 |      Sets the value of a pixel.
 |      
 |      This method takes 3 parameters in 2D: the x and y index then the value,
 |      and 4 parameters in 3D: the x, y and z index then the value.
 |  
 |  SetPixelAsComplexFloat64(self, *args, **kwargs)
 |      SetPixelAsComplexFloat64(Image self, VectorUInt32 idx, std::complex< double > const v)
 |  
 |  SetSpacing(self, *args, **kwargs)
 |      SetSpacing(Image self, VectorDouble spacing)
 |  
 |  TransformContinuousIndexToPhysicalPoint(self, *args, **kwargs)
 |      TransformContinuousIndexToPhysicalPoint(Image self, VectorDouble index) -> VectorDouble
 |      
 |      Transform continuous index to physical point
 |  
 |  TransformIndexToPhysicalPoint(self, *args, **kwargs)
 |      TransformIndexToPhysicalPoint(Image self, VectorInt64 index) -> VectorDouble
 |      
 |      Transform index to physical point
 |  
 |  TransformPhysicalPointToContinuousIndex(self, *args, **kwargs)
 |      TransformPhysicalPointToContinuousIndex(Image self, VectorDouble point) -> VectorDouble
 |      
 |      Transform physical point to continuous index
 |  
 |  TransformPhysicalPointToIndex(self, *args, **kwargs)
 |      TransformPhysicalPointToIndex(Image self, VectorDouble point) -> VectorInt64
 |      
 |      Transform physical point to index
 |  
 |  __GetPixelAsComplexFloat32__(self, *args, **kwargs)
 |      __GetPixelAsComplexFloat32__(Image self, VectorUInt32 idx) -> std::complex< float >
 |  
 |  __GetPixelAsDouble__(self, *args, **kwargs)
 |      __GetPixelAsDouble__(Image self, VectorUInt32 idx) -> double
 |  
 |  __GetPixelAsFloat__(self, *args, **kwargs)
 |      __GetPixelAsFloat__(Image self, VectorUInt32 idx) -> float
 |  
 |  __GetPixelAsInt16__(self, *args, **kwargs)
 |      __GetPixelAsInt16__(Image self, VectorUInt32 idx) -> int16_t
 |  
 |  __GetPixelAsInt32__(self, *args, **kwargs)
 |      __GetPixelAsInt32__(Image self, VectorUInt32 idx) -> int32_t
 |  
 |  __GetPixelAsInt64__(self, *args, **kwargs)
 |      __GetPixelAsInt64__(Image self, VectorUInt32 idx) -> int64_t
 |  
 |  __GetPixelAsInt8__(self, *args, **kwargs)
 |      __GetPixelAsInt8__(Image self, VectorUInt32 idx) -> int8_t
 |  
 |  __GetPixelAsUInt16__(self, *args, **kwargs)
 |      __GetPixelAsUInt16__(Image self, VectorUInt32 idx) -> uint16_t
 |  
 |  __GetPixelAsUInt32__(self, *args, **kwargs)
 |      __GetPixelAsUInt32__(Image self, VectorUInt32 idx) -> uint32_t
 |  
 |  __GetPixelAsUInt64__(self, *args, **kwargs)
 |      __GetPixelAsUInt64__(Image self, VectorUInt32 idx) -> uint64_t
 |  
 |  __GetPixelAsUInt8__(self, *args, **kwargs)
 |      __GetPixelAsUInt8__(Image self, VectorUInt32 idx) -> uint8_t
 |  
 |  __GetPixelAsVectorFloat32__(self, *args, **kwargs)
 |      __GetPixelAsVectorFloat32__(Image self, VectorUInt32 idx) -> VectorFloat
 |  
 |  __GetPixelAsVectorFloat64__(self, *args, **kwargs)
 |      __GetPixelAsVectorFloat64__(Image self, VectorUInt32 idx) -> VectorDouble
 |  
 |  __GetPixelAsVectorInt16__(self, *args, **kwargs)
 |      __GetPixelAsVectorInt16__(Image self, VectorUInt32 idx) -> VectorInt16
 |  
 |  __GetPixelAsVectorInt32__(self, *args, **kwargs)
 |      __GetPixelAsVectorInt32__(Image self, VectorUInt32 idx) -> VectorInt32
 |  
 |  __GetPixelAsVectorInt64__(self, *args, **kwargs)
 |      __GetPixelAsVectorInt64__(Image self, VectorUInt32 idx) -> VectorInt64
 |  
 |  __GetPixelAsVectorInt8__(self, *args, **kwargs)
 |      __GetPixelAsVectorInt8__(Image self, VectorUInt32 idx) -> VectorInt8
 |  
 |  __GetPixelAsVectorUInt16__(self, *args, **kwargs)
 |      __GetPixelAsVectorUInt16__(Image self, VectorUInt32 idx) -> VectorUInt16
 |  
 |  __GetPixelAsVectorUInt32__(self, *args, **kwargs)
 |      __GetPixelAsVectorUInt32__(Image self, VectorUInt32 idx) -> VectorUInt32
 |  
 |  __GetPixelAsVectorUInt64__(self, *args, **kwargs)
 |      __GetPixelAsVectorUInt64__(Image self, VectorUInt32 idx) -> VectorUInt64
 |  
 |  __GetPixelAsVectorUInt8__(self, *args, **kwargs)
 |      __GetPixelAsVectorUInt8__(Image self, VectorUInt32 idx) -> VectorUInt8
 |  
 |  __SetPixelAsComplexFloat32__(self, *args, **kwargs)
 |      __SetPixelAsComplexFloat32__(Image self, VectorUInt32 idx, std::complex< float > const v)
 |  
 |  __SetPixelAsDouble__(self, *args, **kwargs)
 |      __SetPixelAsDouble__(Image self, VectorUInt32 idx, double v)
 |  
 |  __SetPixelAsFloat__(self, *args, **kwargs)
 |      __SetPixelAsFloat__(Image self, VectorUInt32 idx, float v)
 |  
 |  __SetPixelAsInt16__(self, *args, **kwargs)
 |      __SetPixelAsInt16__(Image self, VectorUInt32 idx, int16_t v)
 |  
 |  __SetPixelAsInt32__(self, *args, **kwargs)
 |      __SetPixelAsInt32__(Image self, VectorUInt32 idx, int32_t v)
 |  
 |  __SetPixelAsInt64__(self, *args, **kwargs)
 |      __SetPixelAsInt64__(Image self, VectorUInt32 idx, int64_t v)
 |  
 |  __SetPixelAsInt8__(self, *args, **kwargs)
 |      __SetPixelAsInt8__(Image self, VectorUInt32 idx, int8_t v)
 |  
 |  __SetPixelAsUInt16__(self, *args, **kwargs)
 |      __SetPixelAsUInt16__(Image self, VectorUInt32 idx, uint16_t v)
 |  
 |  __SetPixelAsUInt32__(self, *args, **kwargs)
 |      __SetPixelAsUInt32__(Image self, VectorUInt32 idx, uint32_t v)
 |  
 |  __SetPixelAsUInt64__(self, *args, **kwargs)
 |      __SetPixelAsUInt64__(Image self, VectorUInt32 idx, uint64_t v)
 |  
 |  __SetPixelAsUInt8__(self, *args, **kwargs)
 |      __SetPixelAsUInt8__(Image self, VectorUInt32 idx, uint8_t v)
 |  
 |  __SetPixelAsVectorFloat32__(self, *args, **kwargs)
 |      __SetPixelAsVectorFloat32__(Image self, VectorUInt32 idx, VectorFloat v)
 |  
 |  __SetPixelAsVectorFloat64__(self, *args, **kwargs)
 |      __SetPixelAsVectorFloat64__(Image self, VectorUInt32 idx, VectorDouble v)
 |  
 |  __SetPixelAsVectorInt16__(self, *args, **kwargs)
 |      __SetPixelAsVectorInt16__(Image self, VectorUInt32 idx, VectorInt16 v)
 |  
 |  __SetPixelAsVectorInt32__(self, *args, **kwargs)
 |      __SetPixelAsVectorInt32__(Image self, VectorUInt32 idx, VectorInt32 v)
 |  
 |  __SetPixelAsVectorInt64__(self, *args, **kwargs)
 |      __SetPixelAsVectorInt64__(Image self, VectorUInt32 idx, VectorInt64 v)
 |  
 |  __SetPixelAsVectorInt8__(self, *args, **kwargs)
 |      __SetPixelAsVectorInt8__(Image self, VectorUInt32 idx, VectorInt8 v)
 |  
 |  __SetPixelAsVectorUInt16__(self, *args, **kwargs)
 |      __SetPixelAsVectorUInt16__(Image self, VectorUInt32 idx, VectorUInt16 v)
 |  
 |  __SetPixelAsVectorUInt32__(self, *args, **kwargs)
 |      __SetPixelAsVectorUInt32__(Image self, VectorUInt32 idx, VectorUInt32 v)
 |  
 |  __SetPixelAsVectorUInt64__(self, *args, **kwargs)
 |      __SetPixelAsVectorUInt64__(Image self, VectorUInt32 idx, VectorUInt64 v)
 |  
 |  __SetPixelAsVectorUInt8__(self, *args, **kwargs)
 |      __SetPixelAsVectorUInt8__(Image self, VectorUInt32 idx, VectorUInt8 v)
 |  
 |  __abs__(self)
 |  
 |  __add__(self, other)
 |  
 |  __and__(self, other)
 |  
 |  __del__ lambda self
 |  
 |  __div__(self, other)
 |  
 |  __eq__(self, other)
 |  
 |  __floordiv__(self, other)
 |  
 |  __ge__(self, other)
 |  
 |  __getattr__ lambda self, name
 |  
 |  __getitem__(self, idx)
 |      Get an pixel value or a sliced image.
 |      
 |      This operator implements basic indexing where idx is
 |      arguments or a squence of integers the same dimension as
 |      the image. The result will be a pixel value from that
 |      index.
 |      
 |      Multi-dimension extended slice based indexing is also
 |      implemented. The return is a copy of a new image. The
 |      standard sliced based indices are supported including
 |      negative indices, to indicate location relative to the
 |      end, along with negative step sized to indicate reversing
 |      of direction.
 |      
 |      If the length of idx is less than the number of dimension
 |      of the image it will be padded with the defaults slice
 |      ":".
 |      
 |      A 2D image can be extracted from a 3D image by providing
 |      one argument being an integer instead of a slice.
 |  
 |  __gt__(self, other)
 |  
 |  __iadd__(self, other)
 |  
 |  __init__(self, *args)
 |      __init__(itk::simple::Image self) -> Image
 |      __init__(itk::simple::Image self, Image img) -> Image
 |      __init__(itk::simple::Image self, unsigned int width, unsigned int height, itk::simple::PixelIDValueEnum valueEnum) -> Image
 |      __init__(itk::simple::Image self, unsigned int width, unsigned int height, unsigned int depth, itk::simple::PixelIDValueEnum valueEnum) -> Image
 |      __init__(itk::simple::Image self, VectorUInt32 size, itk::simple::PixelIDValueEnum valueEnum, unsigned int numberOfComponents=0) -> Image
 |  
 |  __invert__(self)
 |  
 |  __iter__(self)
 |  
 |  __le__(self, other)
 |  
 |  __len__(self)
 |  
 |  __lt__(self, other)
 |  
 |  __mod__(self, other)
 |  
 |  __mul__(self, other)
 |  
 |  __ne__(self, other)
 |  
 |  __neg__(self)
 |  
 |  __or__(self, other)
 |  
 |  __pos__(self)
 |  
 |  __pow__(self, other)
 |  
 |  __radd__(self, other)
 |  
 |  __rand__(self, other)
 |  
 |  __rdiv__(self, other)
 |  
 |  __repr__ = _swig_repr(self)
 |  
 |  __rfloordiv__(self, other)
 |  
 |  __rmul__(self, other)
 |  
 |  __ror__(self, other)
 |  
 |  __rpow__(self, other)
 |  
 |  __rsub__(self, other)
 |  
 |  __rtruediv__(self, other)
 |  
 |  __rxor__(self, other)
 |  
 |  __setattr__ lambda self, name, value
 |  
 |  __setitem__(self, idx, value)
 |      Sets the pixel value at index idx to value.
 |      
 |      The dimension of idx should match that of the image.
 |  
 |  __str__(self)
 |      __str__(Image self) -> std::string
 |  
 |  __sub__(self, other)
 |  
 |  __truediv__(self, other)
 |  
 |  __xor__(self, other)
 |  
 |  ----------------------------------------------------------------------
 |  Data descriptors defined here:
 |  
 |  __dict__
 |      dictionary for instance variables (if defined)
 |  
 |  __weakref__
 |      list of weak references to the object (if defined)
 |  
 |  ----------------------------------------------------------------------
 |  Data and other attributes defined here:
 |  
 |  __swig_destroy__ = <built-in function delete_Image>
 |      delete_Image(Image self)
 |  
 |  __swig_getmethods__ = {}
 |  
 |  __swig_setmethods__ = {}


### 属性访问

如果你熟悉ITK，那么这些方法就是你了解的：

```python
print image.GetSize()
print image.GetOrigin()
print image.GetSpacing()
print image.GetDirection()
print image.GetNumberOfComponentsPerPixel()
```

> (256, 128, 64)
> (0.0, 0.0, 0.0)
> (1.0, 1.0, 1.0)
> (1.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0, 0.0, 1.0)
> 1

注意：SimpleITK图像的开始下标为0.如果ITK滤波器输出是一个非0开始下标，那么下标将被置为0，并对原点进行相应的映射。
图像的维度大小可以通过显示调用访问：

```python
print image.GetWidth()
print image.GetHeight()
print image.GetDepth()
```

> 256
> 128
> 64

SimpleITK图像的维数和像素类型是可以动态确定和访问的。

```python
print image.GetDimension()
print image.GetPixelIDValue()
print image.GetPixelIDTypeAsString()
```

> 3
> 2
> 16-bit signed integer

### 获取是二维图像的深度

```python
print image_2D.GetSize()
print image_2D.GetDepth()
```

> (32, 32)
> 0

### 向量图的大小和维度

```python
print image_RGB.GetDimension()
print image_RGB.GetSize()
```

> 2
> (128, 128)

```python
print image_RGB.GetNumberOfComponentsPerPixel()
```
> 3

对于指定文件类型，例如DICOM，有关附加信息可以从meta-data字典获得。

```python
for key in image.GetMetaDataKeys():
        print "\"{0}\":\"{1}\"".format(key, image.GetMetaData(key))
```

### 访问像素

SimpleITK提供类ITK接口的成员函数GetPixel和SetPixel用作像素访问。

```python
help(image.GetPixel)
```

获取模块SimpleITK.SimpleITK方法GetPixel的帮助信息：


GetPixel(self, *idx) method of SimpleITK.SimpleITK.Image instance
    Returns the value of a pixel.
    
    This method takes 2 parameters in 2D: the x and y index,
    and 3 parameters in 3D: the x, y and z index.


```python
print image.GetPixel(0, 0, 0)
image.SetPixel(0, 0, 0, 1)
print image.GetPixel(0, 0, 0)
```

> 0
> 1

```
print image[0,0,0]
image[0,0,0] = 10
print image[0,0,0]
```

>1
>10

### SimpleITK与numpy之间的转换

```python
nda = sitk.GetArrayFromImage(image)
print nda
```

> [[[10  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   ..., 
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]]
> 
>  [[ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   ..., 
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]]
> 
>  [[ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   ..., 
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]]
> 
>  ..., 
>  [[ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   ..., 
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]]
> 
>  [[ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   ..., 
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]]
> 
>  [[ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   ..., 
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]
>   [ 0  0  0 ...,  0  0  0]]]

```python
help(sitk.GetArrayFromImage)
```

SimpleITK.SimpleITK模块GetArrayFromImage函数的帮助信息


GetArrayFromImage(image)
    Get a numpy array from a SimpleITK Image.


```python
nda = sitk.GetArrayFromImage(image_RGB)
img = sitk.GetImageFromArray(nda)
img.GetSize()
```

> (3, 128, 128)

```python
help(sitk.GetImageFromArray)
```
SimpleITK.SimpleITK模块GetImageFromArray函数的帮助信息

GetImageFromArray(arr, isVector=False)
    Get a SimpleITK Image from a numpy array. If isVector is True, then a 3D array will be treaded as a 2D vector image, otherwise it will be treaded as a 3D image


```python
img = sitk.GetImageFromArray(nda, isVector=True)
print img
```

```python
VectorImage (0x7f8b68d90880)
  RTTI typeinfo:   itk::VectorImage<unsigned char, 2u>
  Reference Count: 1
  Modified Time: 497
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
    Size: [128, 128]
  BufferedRegion: 
    Dimension: 2
    Index: [0, 0]
    Size: [128, 128]
  RequestedRegion: 
    Dimension: 2
    Index: [0, 0]
    Size: [128, 128]
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

  VectorLength: 3
  PixelContainer: 
    ImportImageContainer (0x7f8b68d90a70)
      RTTI typeinfo:   itk::ImportImageContainer<unsigned long, unsigned char>
      Reference Count: 1
      Modified Time: 498
      Debug: Off
      Object Name: 
      Observers: 
        none
      Pointer: 0x7f8b69969c00
      Container manages memory: true
      Size: 49152
      Capacity: 49152
```

### 在转换的时候下标需要小心和维数的顺序

ITK图像类并不包含bracket操作，它包含一个GetPixel，传入一个ITK下标对象作为参数，顺序为(x, y, z)。对于SimpleITK也是按这顺序约定。
而在numpy中，一个数组的下标顺序恰好相反(z,y,x)。

```python
print img.GetSize()
print nda.shape
print nda.shape[::-1]
```

> (128, 128)
> (128, 128, 3)
> (3, 128, 128)

### 我们是在做图像处理吗？因为我们还没有看到一张图像...
Are we still dealing with Image, because I haven't seen one yet...

SimpleITK并不能完成可视化，但它包含一个内建的Show方法。此函数把图像写到磁盘，然后启动一个程序可视化，默认地它使用ImageJ，因为
它支持所有SimpleITK的图像类型并加载很快。然而，你可以很容易定制，通过修改环境变量可以设置选择的可视化程序。

```python
sitk.Show(image)
```

```python
sitk.Show?
```

通过转换成numpy数组，可以使用matplotlob进行可视化，它集成在python的科学可视化环境中

```python
import pylab
z = 0
slice = sitk.GetArrayFromImage(image)[z,:,:]
imshow(slice)
```

> <matplotlib.image.AxesImage at 0x110d3c290>

![SimpleITK使用matplotlob可视化](https://raw.githubusercontent.com/summit4you/summit4you.github.io/master/images/python/SimpleITK-Image-Basics.jpg)

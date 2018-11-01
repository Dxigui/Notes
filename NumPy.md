# NumPy

## 介绍

`NumPy` 提供了多维数组对象,多种派生对象(掩码数组、矩阵),以及快速操作数组的函数及 API,包括数学、逻辑、数组形状变换、排序、选择、I/O、离散傅里叶变换，基本线性代数、基本统计运算、随机模拟等.

`Numpy` 数组和标准的 `Python List` 之间的重要区别:

* `NumPy`数组在创建时具有固定的大小,与 `Python` 的原生数组(可动态增长)不同,更改 `NumPy` 数组大小时会删除原数组,创建新数组.
* `NumPy` 数组元素都需要具有相同的数据类型
* `NumPy` 数组有助于大量数据进行高级数学和其他类型操作

## 基础

`NumPy` 的主要对象是不同类型的多维数组.在 `NumPy` 中,维度(rank)为轴.例: `[1,2,3]` 是 `rank` 为 1 的数组,具有一个轴,该轴长度为 3.

### `ndarray` 属性

`NumPy` 中数组类为 `ndarray`,`ndarray` 属性:

* `ndarray.ndim`: 数组的轴(维度)的个数,在 `Python` 维度被称为 `rank`
* `ndarray.shape`: 数组的大小,
* `ndarray.size`: 数组中元素的总数,等于 `shape` 的元素乘积
* `ndarray.dtype`: 描述数组中元素的类型
* `ndarray.itemsize`: 数组中每个元素的字节大小.例:元素为 `float64` 类型的数组的 `itemsize` 为 8 (64/8),而 `complex32` 类型的数组的 `itemsize` 为 4 (32/8)
* `ndarray.data`: 该缓冲区包含数组的实际元素

An example:

```python
>>> import numpy as np
>>> a = np.arange(15).reshape(3, 5)
>>> a
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14]])
>>> a.shape
(3, 5)
>>> a.ndim
2
>>> a.dtype.name
'int64'
>>> a.itemsize
8
>>> a.size
15
>>> type(a)
<type 'numpy.ndarray'>
>>> b = np.array([6, 7, 8])
>>> b
array([6, 7, 8])
>>> type(b)
<type 'numpy.ndarray'>
```



### 创建数组

1. 利用 `Array` 函数常见数组

```python
>>> import numpy as np
>>> a = np.array([2,3,4])
>>> a
array([2, 3, 4])
>>> a.dtype
dtype('int64')
>>> b = np.array([1.2, 3.5, 5.1])
>>> b.dtype
dtype('float64')
>>> # 指定类型
>>> c = np.array([[1,2,3],[2,3,4]], dtype=complex)
```

2. 创建占位数组

```python
>>> # 以 0 为占位符
>>> np.zeros((2,3))
array([[0., 0., 0.],
       [0., 0., 0.]])

>>> # 以 1 为占位符,可通过 dtype 设置类型
>>> np.ones((2,2,3))
array([[[1., 1., 1.],
        [1., 1., 1.]],

       [[1., 1., 1.],
        [1., 1., 1.]]])

>>> # 创建未初始化的数组
>>> np.empty((2,3))
array([[1., 1., 1.],
       [1., 1., 1.]])
```

3. 创建数字序列

通过 `arange` 函数创建

```python
>>> np.arange(10,30,5)
array([10, 15, 20, 25])
>>> # 也可以用接受浮点型
>>> np.arange(0,2,0.2)
array([0. , 0.2, 0.4, 0.6, 0.8, 1. , 1.2, 1.4, 1.6, 1.8])
```

通过 `arange` 虽然可以创建浮点型数组,但是元素的精度不够,经常使用 `linspace` 函数代替

```python
>>> #等比例切割
>>> np.linspace(0,2,9)
array([0.  , 0.25, 0.5 , 0.75, 1.  , 1.25, 1.5 , 1.75, 2.  ])
```

4. See also

`array, zeros, zeros_like, ones_like, empty, empty_like, arange, linspace, numpy.random.rand, numpy.random.random, fromfunction, fromfile, numpy.random.shuffle`


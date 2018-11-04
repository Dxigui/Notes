# NumPy

## 介绍

`NumPy` 提供了多维数组对象,多种派生对象(掩码数组、矩阵),以及快速操作数组的函数及 API,包括数学、逻辑、数组形状变换、排序、选择、I/O、离散傅里叶变换，基本线性代数、基本统计运算、随机模拟等.

`Numpy` 数组和标准的 `Python List` 之间的重要区别:

* `NumPy`数组在创建时具有固定的大小,与 `Python` 的原生数组(可动态增长)不同,更改 `NumPy` 数组大小时会删除原数组,创建新数组.
* `NumPy` 数组元素都需要具有相同的数据类型
* `NumPy` 数组有助于大量数据进行高级数学和其他类型操作

NumPy的部分功能如下：

- ndarray，一个具有矢量算术运算和复杂广播能力的快速且节省空间的多维数组。
- 用于对整组数据进行快速运算的标准数学函数（无需编写循环）。
- 用于读写磁盘数据的工具以及用于操作内存映射文件的工具。
- 线性代数、随机数生成以及傅里叶变换功能。
- 用于集成由C、C++、Fortran等语言编写的代码的A C API。

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

> `array, zeros, zeros_like, ones_like, empty, empty_like, arange, linspace, numpy.random.rand, numpy.random.random, fromfunction, fromfile, numpy.random.shuffle`



### 基础运算

1. 

* 相同大小的多维数组可以相加减
* 行列相等的多维数组可以相乘除

2. 矩阵积

```python
>>> A @ B              # matrix product
array([[5, 4],
       [3, 4]])
>>> A.dot(B)           # another matrix product
array([[5, 4],
       [3, 4]])
```

3. 聚合

可以设定 `axis` 参数对指定轴进行操作(`axis=1` (行) or `axis=0` (列))

```python
>>> b = np.arange(12).reshape(3,4)
>>> b
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11]])
>>> b.sum(axis=0)               # 对每一列求和
array([12, 15, 18, 21])
>>>
>>> b.min(axis=1)               # 对每一行求最小值
array([0, 4, 8])
>>>
>>> b.cumsum(axis=1)            # 
array([[ 0,  1,  3,  6],
       [ 4,  9, 15, 22],
       [ 8, 17, 27, 38]])
>>> # 平均数 np.mean()
>>> # 方差 np.var()
>>> # 标准差 np.std() / np.sqrt(np.var())
```

### 通用函数

>`all, add, any, apply_along_aixs, argmax, argmin, argsort, average(取平均值), bincount, ceil(向上取整), clip, conj, corrcoef, cov, cross, cumprod, cumsum, diff, dot(矩阵积), floor(向下取整), fromfunction(通过函数生成数组), lnner, inv, lexsort, max(取最大值), maximum, mean, median, min(取最小值), minimum, nonzero, outer, prod, re, round, sort(排序), std, sum(求和), sqrt(平方根), trace, tanspose, var, vdot, vectorize, where`

### 切片,索引,迭代

1. 一维数组

一维数组的切片和 `Python` 一样

```python
>>> arr = np.arange(10)**3
>>> arr
array([  0,   1,   8,  27,  64, 125, 216, 343, 512, 729])
>>> # 替换元素
>>> arr[:6:2] = -1000
>>> arr
array([-1000,     1, -1000,    27, -1000,   125,   216,   343,   512,   729])
```

2. 多维数组

每个轴可以有一个索引,当提供比轴数更少的索引时,缺失的索引被认为是一个完整的切片

```python
>>> def f(x,y):
...     return 10*x+y
...
>>> b = np.fromfunction(f,(5,4),dtype=int)
>>> b
array([[ 0,  1,  2,  3],
       [10, 11, 12, 13],
       [20, 21, 22, 23],
       [30, 31, 32, 33],
       [40, 41, 42, 43]])
>>> b[2,3]
23
>>> b[0:5, 1]               # each row in the second column of b
array([ 1, 11, 21, 31, 41])
>>> b[ : ,1]                # equivalent to the previous example
array([ 1, 11, 21, 31, 41])
>>> b[1:3, : ]              # each column in the second and third row of b
array([[10, 11, 12, 13],
       [20, 21, 22, 23]])
>>> b[-1]                  # 负索引
array([40, 41, 42, 43])
```

`NumPy` 也可以使用三个点 `...` 表示完整索引,和 `:` 一样.

- `x[1,...]` 等于 `x[1,:]`。
- `x[...,3]` 等效于 `x[:,3]`。

```python
>>> b[...,1]
array([ 1, 11, 21, 31, 41])
```

3. see also

> `indexing,  newaxis, ndenumerate, indices`

4. 迭代

多维数组以轴迭代

```python
>>> for row in b:
        print(row)
[0 1 2 3]
[10 11 12 13]
[20 21 22 23]
[30 31 32 33]
[40 41 42 43]
```

迭代每一个元素

```python
>>> for element in b.flat:
        print(element)
0
1
2
3
10
11
12
13
20
21
22
23
30
31
32
33
40
41
42
43
```

## Shape Manipulation

1. 更改数组形状

```python
>>> a = np.floor(10*np.random.random((3,4)))
>>> a
array([[ 2.,  8.,  0.,  6.],
       [ 4.,  5.,  1.,  1.],
       [ 8.,  9.,  3.,  6.]])
>>> a.shape
(3, 4)
>>> # 将多维数组变为一维数组
>>> a.ravel()
array([ 2.,  8.,  0.,  6.,  4.,  5.,  1.,  1.,  8.,  9.,  3.,  6.])
>>> # returns the array with a modified shape
>>> a.reshape()
array([[ 2.,  8.],
       [ 0.,  6.],
       [ 4.,  5.],
       [ 1.,  1.],
       [ 8.,  9.],
       [ 3.,  6.]])
>>> # 翻转数组, 行==>列 列==>行
>>> a.T
array([[ 2.,  4.,  8.],
       [ 8.,  5.,  9.],
       [ 0.,  1.,  3.],
       [ 6.,  1.,  6.]])
>>> # resize 修改数组本身
>>> a.resize((2,6))
>>> a
array([[ 2.,  8.,  0.,  6.,  4.,  5.],
       [ 1.,  1.,  8.,  9.,  3.,  6.]])
```


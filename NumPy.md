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

5. Fancy indexing

花式索引将取出的数据复制到新数组中

```python
>>> arr = np.empty((8, 4))
>>> for i in range(8):
        arr[i] = i
>>> arr
array([[ 0.,  0.,  0.,  0.],
       [ 1.,  1.,  1.,  1.],
       [ 2.,  2.,  2.,  2.],
       [ 3.,  3.,  3.,  3.],
       [ 4.,  4.,  4.,  4.],
       [ 5.,  5.,  5.,  5.],
       [ 6.,  6.,  6.,  6.],
       [ 7.,  7.,  7.,  7.]])
>>> # 花式索引
>>> # 同时去多组
>>> arr[[4, 3, 0, 6]]
array([[ 4.,  4.,  4.,  4.],
       [ 3.,  3.,  3.,  3.],
       [ 0.,  0.,  0.,  0.],
       [ 6.,  6.,  6.,  6.]])
>>> # 负索引
>>> arr[[-3, -5, -7]]
array([[ 5.,  5.,  5.,  5.],
       [ 3.,  3.,  3.,  3.],
       [ 1.,  1.,  1.,  1.]])
>>> arr2 = np.aragne(32).reshape(8.4)
>>> arr
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11],
       [12, 13, 14, 15],
       [16, 17, 18, 19],
       [20, 21, 22, 23],
       [24, 25, 26, 27],
       [28, 29, 30, 31]])
>>> # 先取出 1,5,7,2 行,然后在其基础上操作
>>> arr[[1, 5, 7, 2]][:, [0, 3, 1, 2]]
array([[ 4,  7,  5,  6],
       [20, 23, 21, 22],
       [28, 31, 29, 30],
       [ 8, 11,  9, 10]])
```

6. 布尔型索引

生成数组

```python
>>> names = np.array(['Bob', 'Joe', 'Will', 'Bob', 'Will', 'Joe', 'Joe'])
>>> # 生成正太分布随机数
>>> data = np.random.randn(7, 4)
>>> names
array(['Bob', 'Joe', 'Will', 'Bob', 'Will', 'Joe', 'Joe'],
      dtype='<U4')
>>> data
array([[ 0.0929,  0.2817,  0.769 ,  1.2464],
       [ 1.0072, -1.2962,  0.275 ,  0.2289],
       [ 1.3529,  0.8864, -2.0016, -0.3718],
       [ 1.669 , -0.4386, -0.5397,  0.477 ],
       [ 3.2489, -1.0212, -0.5771,  0.1241],
       [ 0.3026,  0.5238,  0.0009,  1.3438],
       [-0.7135, -0.8312, -2.3702, -1.8608]])
```

跟算术运算一样,数组的比较运算也是矢量的

```python
>>> names == 'Bob'
array([ True, False, False,  True, False, False, False], dtype=bool)
```

将上面的数组用于数组索引, (`~`) 取反

```python
>>> # 布尔型索引的长度与轴长一致
>>> data[names == 'Bob']
array([[ 0.0929,  0.2817,  0.769 ,  1.2464],
       [ 1.669 , -0.4386, -0.5397,  0.477 ]])
>>> data[~(names == 'Bob')]
array([[ 1.0072, -1.2962,  0.275 ,  0.2289],
       [ 1.3529,  0.8864, -2.0016, -0.3718],
       [ 3.2489, -1.0212, -0.5771,  0.1241],
       [ 0.3026,  0.5238,  0.0009,  1.3438],
       [-0.7135, -0.8312, -2.3702, -1.8608]])
```

布尔型索引与切片混用

```python
>>> data[names == 'Bob', 2:]
array([[ 0.769 ,  1.2464],
       [-0.5397,  0.477 ]])

```

结合布尔算数运算符

```python
>>> data[(names == 'Bob') | (names == 'Will')]
array([[ 0.0929,  0.2817,  0.769 ,  1.2464],
       [ 1.3529,  0.8864, -2.0016, -0.3718],
       [ 1.669 , -0.4386, -0.5397,  0.477 ],
       [ 3.2489, -1.0212, -0.5771,  0.1241]])
```

赋值

```python
>>> data[names != 'Joe'] = 7
array([[ 7.    ,  7.    ,  7.    ,  7.    ],
       [ 1.0072,  0.    ,  0.275 ,  0.2289],
       [ 7.    ,  7.    ,  7.    ,  7.    ],
       [ 7.    ,  7.    ,  7.    ,  7.    ],
       [ 7.    ,  7.    ,  7.    ,  7.    ],
       [ 0.3026,  0.5238,  0.0009,  1.3438],
       [ 0.    ,  0.    ,  0.    ,  0.    ]])
```





## Shape Manipulation

### 更改数组形状

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

### 数组转置和轴对换

在 `NumPy` 中有三种内置的转置方法

* `T` 属性: 多用一一维或二维, 高维中想要更灵活的进行转换需要用到其他两个
* `transpose` 方法:接受由轴编号组成的元祖进行转换
* `swapaxes` 方法:接受由编号组成的元祖进行转置

1. `T`

```python
>>> arr4 = np.arange(12).reshape((4, 3))
>>> arr4
array([[ 0,  1,  2],
       [ 3,  4,  5],
       [ 6,  7,  8],
       [ 9, 10, 11]])
>>> arr4.T
array([[ 0,  3,  6,  9],
       [ 1,  4,  7, 10],
       [ 2,  5,  8, 11]])
```

2. `transpose`

`transponse()` 方法接受的编号就是数组 `shape` 的返回值的编号.

例如:

```python
>>> # 生成一个数组
>>> arr = np.arange(12).reshape(3,2,2)
>>> arr.shape
(3,2,2)
```

上面数组 `arr` 的 `shape` 为 `(3,2,2)` ,那么 `shape` 的编号为 `(0,1,2)` (可以与列表的索引做参考) , `0` 对应 `3` ; `1` 对应 `2` ; `2` 对应 `2`. 将 `(0,1,2)` 传入 `transponse()` 中

```python
>>> arr = np.arange(12).reshape(3,2,2)
>>> arr
array([[[ 0,  1],
        [ 2,  3]],

       [[ 4,  5],
        [ 6,  7]],

       [[ 8,  9],
        [10, 11]]])
>>> # 转换
>>> arr6.transpose((1,0,2))
array([[[ 0,  1],
        [ 4,  5],
        [ 8,  9]],

       [[ 2,  3],
        [ 6,  7],
        [10, 11]]])
```

在上面的实例中, 将原来的编号 `(0,1,2)` 转置成 `(1,0,2)`(`1` 和 `0` 转换) ,那么实际的 `shape` 则也进行了转置, 有 `(3,2,2)` 变成 `(2,3,2)`. 

```python
>>> # 1 和 2 转换
>>> arr6.transpose((0,2,1))
array([[[ 0,  2],
        [ 1,  3]],

       [[ 4,  6],
        [ 5,  7]],

       [[ 8, 10],
        [ 9, 11]]])
```

3. `wrapaxes` 

`swapaxes()` ,和 `transpose()` 接受的参数是一样的,不过不像 `transpose()` 需要把整个编号传入,只需传入需要转置的编号.

```python
>>> # 装置 0 和 1
>>> arr = np.arange(12).reshape(2,2,3)
>>> arr
array([[[ 0,  1,  2],
        [ 3,  4,  5]],

       [[ 6,  7,  8],
        [ 9, 10, 11]]])
>>> arr.swapaxes(1,0)
array([[[ 0,  1,  2],
        [ 6,  7,  8]],

       [[ 3,  4,  5],
        [ 9, 10, 11]]])
```


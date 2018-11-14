# Pandas

 `Pandas` 中两种重要的数据结构 `Series` 和 `DataFrame`

* `Series` : 类似一维数组由一组数据以及一组与之相关的数据标签组成
* `DataFrame` : 表格型的数据结构,含有这一组有序的列,每列可以是不同的类型(数值,字符串,布尔值).既有行索引,又有列索引

1. `series`
2. `DataFrame`

可接受的参数

![](https://github.com/Dxigui/Notes/blob/master/img/dataframe_recv.png)





## 数据读取

读取函数

![](https://github.com/Dxigui/Notes/blob/master/img/pandas_io.png)

一般 `read_csv/read_table` 使用最多

`read_csv/read_table` 常用参数

* `nrows` 设定读取的行数
* `chunksize` 设定读取行数,返回一个可迭代对象 `TextParsers`,

![](https://github.com/Dxigui/Notes/blob/master/img/pd_csv_table_args.png)

![](https://github.com/Dxigui/Notes/blob/master/img/pd_csv_table_args2.png)

读取 `csv` 文件

```python
>>> import pandas as pd
>>> pd.read_csv('./example/test.csv')
	a	b	c	d	message
0	1	2	3	4	hello
1	5	6	7	8	world
2	9	10	11	12	foo
>>> # 设置分隔符 sep 可以传入正则表达式 如 '\s+'
>>> pd.read_csv('./example/test.csv', sep=',')
	a	b	c	d	message
0	1	2	3	4	hello
1	5	6	7	8	world
2	9	10	11	12	foo
>>> # 设置分配默认列名
>>> pd.read_csv('./example/test2.csv', header=None)
   0   1   2   3      4
0  1   2   3   4  hello
1  5   6   7   8  world
2  9  10  11  12    foo
>>> # 设置自定义列名
>>> pd.read_csv('./example/test2.csv', names=['a', 'b', 'c', 'd', 'message'])
   a   b   c   d message
0  1   2   3   4   hello
1  5   6   7   8   world
2  9  10  11  12     foo
>>> # 层次化索引,传入列编号和列名
>>> # test3.csv
key1,key2,value1,value2
one,a,1,2
one,b,3,4
one,c,5,6
one,d,7,8
two,a,9,10
two,b,11,12
two,c,13,14
two,d,15,16
>>> pf3 = pd.read_csv('./example/test3.csv', index_col=['key1', 'key2'])
           value1  value2
key1 key2                
one  a          1       2
     b          3       4
     c          5       6
     d          7       8
two  a          9      10
     b         11      12
     c         13      14
     d         15      16
>>> pf3.loc['one']
	value1	value2
key2		
a	1	2
b	3	4
c	5	6
d	7	8
>>> # 跳过文本的某一些行数,不是下标
>>> pd.read_csv('./example/test3.csv', shiprows=[1,2,4])
  key1 key2  value1  value2
0  one    c       5       6
1  two    a       9      10
2  two    b      11      12
3  two    c      13      14
4  two    d      15      16
>>> # 缺失值处理, Pandas 识别如 NA/NULL 等,并用 NAN 填充
>>> pf4 = pd.read_csv('./example/test4.csv')
>>> pf4
  something  a   b     c   d message
0       one  1   2   3.0   4     NaN
1       two  5   6   NaN   8   world
2     three  9  10  11.0  12     foo
>>> # 查看元素是否有缺失
>>> pd.isnull(pf4)

```

### 逐块读取文本文件

读取大文件时设置只显示部分

```python
>>> # 设置
>>> pd.options.display.max_rows = 10
>>> result = pd.read_csv('examples/ex6.csv')
>>> result
           one       two     three      four key
0     0.467976 -0.038649 -0.295344 -1.824726   L
1    -0.358893  1.404453  0.704965 -0.200638   B
2    -0.501840  0.659254 -0.421691 -0.057688   G
3     0.204886  1.074134  1.388361 -0.982404   R
4     0.354628 -0.133116  0.283763 -0.837063   Q
...        ...       ...       ...       ...  ..
9995  2.311896 -0.417070 -1.409599 -0.515821   L
9996 -0.479893 -0.650419  0.745152 -0.646038   E
9997  0.523331  0.787112  0.486066  1.093156   K
9998 -0.362559  0.598894 -1.843201  0.887292   G
9999 -0.096376 -1.012999 -0.657431 -0.573315   0
[10000 rows x 5 columns]
If you want to only read a small
>>> # 可以通过 nrows 进行指定
>>> pd.read_csv('examples/test6.csv', nrows=5)
        one       two     three      four key
0  0.467976 -0.038649 -0.295344 -1.824726   L
1 -0.358893  1.404453  0.704965 -0.200638   B
2 -0.501840  0.659254 -0.421691 -0.057688   G
3  0.204886  1.074134  1.388361 -0.982404   R
4  0.354628 -0.133116  0.283763 -0.837063   Q
>>> # chunksize 迭代取出
>>> ch = pd.read_csv('examples/ex6.csv', chunksize=1000)
>>> # usecols 指定读取列
>>> pd.read_csv('examples/ex6.csv', usecols=[])
```

### 将数据写到文本

`to_csv` 写入 `csv` 文件

```python
>>> data
  something  a   b     c   d message
0       one  1   2   3.0   4     NaN
1       two  5   6   NaN   8   world
2     three  9  10  11.0  12     foo
>>> # 写入 csv
>>> data.to_csv('example/test6.csv')
>>> # 缺失值默认输入
>>> data.to_csv('example/test6.csv', na_rep='NULL')
```

### JSON 数据

`JSON` 数据是一种网络中传输的数据格式,比表格文本灵活

1. 通过 `Python` 的 `JSON` 模块转换成字典,然后在转 `DataFrame`

```python
>>> import json
>>> result = json.loads(data)
>>> result
{'name': 'Wes',
 'pet': None,
 'places_lived': ['United States', 'Spain', 'Germany'],
 'siblings': [{'age': 30, 'name': 'Scott', 'pets': ['Zeus', 'Zuko']},
  {'age': 38, 'name': 'Katie', 'pets': ['Sixes', 'Stache', 'Cisco']}]}
>>> # 转 DataFrame
>>> p_data = pd.DataFrame(result['sibling'], columns=['name', 'age'])
```

2. 直接用 `pandas.read_json` 读取 `JSON` 文件

```python
>>> data = pd.read_json('./example/test7.json')
```

### XML和HTML：Web信息收集

`pandas`有一个内置的功能，`read_html`，它可以使用 `lxml` 和`Beautiful Soup`自动将 `HTML` 文件中的表格解析为 `DataFrame` 对象.

```python
>>> tables = pd.read_html('examples/fdic_failed_bank_list.html')
```

### 二进制数据格式

实现数据的高效二进制格式存储最简单的办法之一是使用 `Python` 内置的 `pickle` 序列化. pandas对象都有一个用于将数据以 `pickle` 格式保存到磁盘上的 `to_pickle` 方法

```python
>>> frame = pd.read_csv('./example/test8.csv')
>>> # 存储为二进制文件
>>> frame.to_pickle('/example/frame_pickle')
>>> # 读取二进制文件
>>> pd.read_pickle('/example/frame_pickle')
```

`Pandas` 内置支持两个二进制数据格式: **HDF5**和**MessagePack** 

1. `HDF5` 格式

`HDF5`(hierarchical data format **层次型数据结构**) 是一种存储大规模科学数组数据的非常好的文件格式。它可以被作为 `C` 标准库，带有许多语言的接口，如`Java、Python`和`MATLAB`等。每个`HDF5`文件都含有一个文件系统式的节点结构，它使你能够存储多个数据集并支持元数据。与其他简单格式相比，`HDF5`支持多种压缩器的即时压缩，还能更高效地存储重复模式数据。对于那些非常大的无法直接放入内存的数据集，`HDF5` 就是不错的选择，因为它可以高效地分块读写。

`Python` 可以通过 `PyTables` 或 `h5py` 库直接访问 `HDF5` 文件. `Pandas` 也提供了接口.

```python
>>> # pd.HDFStore(path, mode=None, complevel=None, complib=None, fletcher32=False, **kwargs)
>>> # path: 路径
>>> # mode: 读写模式 ('a':文件存在时添加或追加写入, 'w':创建一个新文件,文件存在时会删除旧文件, 'r':只读, 'r+':和'a'功能一样,但是文件必须要已经创建的, default 'a')
>>> # 
>>> farme = pd.Dataframe({'a': np.random.randn(100)})
>>> store = pd.HDFStore('./all/example/mydata.h5')
>>> store['obj1'] = frame
>>> store['obj1_col'] = frame['a']
>>> store
<class 'pandas.io.pytables.HDFStore'>
File path: ./all/example/mydata.h5
>>> store['obj1']
	a
0	0.184441
1	-1.059121
2	1.302739
3	-0.005336
4	0.134014
...	...
95	0.161548
96	0.264454
97	-1.586978
98	-0.233901
99	-0.152625
100 rows × 1 columns
>>> store['obj1_col']
0     0.184441
1    -1.059121
2     1.302739
3    -0.005336
4     0.134014
        ...   
95    0.161548
96    0.264454
97   -1.586978
98   -0.233901
99   -0.152625
Name: a, Length: 100, dtype: float64
>>> type(store['obj1'])        # DataFrame 
<class 'pandas.core.frame.DataFrame'>
>>> type(store['obj1_col'])    # Series
<class 'pandas.core.series.Series'>
```

`HDFStore` 支持两种存储模式，`fixed` 和 `table`。后者通常会更慢，但是支持使用特殊语法进行查询操作

```python
>>> store.put('obj2', frame, format='table')
>>> # 读取 HDF 文件
>>> # 读取指定键/指定范围的数据
>>> pd.read_hdf('./all/example/mydata.h5', 'obj2', where=['index < 5'], mode='r+')

		   a
0	0.184441
1	-1.059121
2	1.302739
3	-0.005336
4	0.134014
```

> HDF5不是数据库。它最适合用作“一次写多次读”的数据集.对于数据分析问题都是 IO 密集型,使用 HDF5 能有效提高效率

### 读取 Excel 文件

`Pandas` 的 `ExcelFile` 类和 `pandas.read_excel` 函数都可以读取 Excel 2003 或以上中的表格数据

```python
>>> # 读取数据
>>> xlsx = pd.ExcelFile('./all/example/exl.xlsx')
>>> pd.read_excel(xlsx, 'Sheet1')
>>> frame = pd.read_excel('./all/example/exl.xlsx', 'Sheet1')
>>> # 写入数据
>>> # 先创建一个 ExcelWriter 对象
>>> # 用 to_excel 写入
>>> writter = pd.ExcelWritter('./all/example/exl2.xlsx')
>>> frame.to_excel(writter, 'Sheet1')
>>> writter.save()
```

### WEB API 交互



### 数据库交互

从表中选取数据时，大部分Python SQL驱动器（PyODBC、psycopg2、MySQLdb、pymssql等）都会返回一个元组列表：

```python
>>> cur = con.execte('SELECT * FROM test')
>>> rows = cur.fetchall()
>>> rows
[('Atlanta', 'Georgia', 1.25, 6),
 ('Tallahassee', 'Florida', 2.6, 3),
 ('Sacramento', 'California', 1.7, 5)]

```

可以将这个元组列表传给DataFrame构造器，但还需要列名（位于光标的description属性中）

```python
>>> cur.descritpion
(('a', None, None, None, None, None, None),
 ('b', None, None, None, None, None, None),
 ('c', None, None, None, None, None, None),
 ('d', None, None, None, None, None, None))
>>> pd.DataFrame(rows, columns=[x[0] for x in cur.description])
             a           b     c  d
0      Atlanta     Georgia  1.25  6
1  Tallahassee     Florida  2.60  3
2   Sacramento  California  1.70  5
```



pandas有一个read_sql函数，可以让你轻松的从SQLAlchemy连接读取数据。

```python
>>> import sqlalchemy as sqla
>>> db = sqla.create_engine('sqlite:///mydata.sqlite')
>>> pd.read_sql('SELECT * FROM test', db)
             a           b     c  d
0      Atlanta     Georgia  1.25  6
1  Tallahassee     Florida  2.60  3
2   Sacramento  California  1.70  5
```



## 数据准备和清洗

### 处理缺失数据

一些缺失值处理函数

![](https://github.com/Dxigui/Notes/blob/master/img/pd_missing_value_func.png)

1. `Series` 对象

```python
>>> string_data = pd.Series(['aardvark', 'artichoke', np.nan, 'avocado'])
>>> string_data
0     aardvark
1    artichoke
2          NaN
3      avocado
dtype: object
>>> # 是否存在缺失值 返回一个同大小的布尔类型
>>> string_data.isnull()
0    False
1    False
2     True
3    False
dtype: bool
>>> # 删除去除缺失值的行后的新 Series
>>> string_data.dropna()
0     aardvark
1    artichoke
3      avocado
dtype: object
>>> # 通过 method/value 填充 NA/NAN 的值 
>>> string_data.fillna(value='Jon')
0     aardvark
1    artichoke
2          Jon
3      avocado
dtype: object
```

2. 过滤 `DataFrame` 对象

```python
>>> data = pd.DataFrame([[1., 6.5, 3.], [1., NA, NA],
                    [NA, NA, NA], [NA, 6.5, 3.]])
>>> # 过滤所有含 NAN 的行
>>> cleaned = data.dropna()
>>> data
     0    1    2
0  1.0  6.5  3.0
1  1.0  NaN  NaN
2  NaN  NaN  NaN
3  NaN  6.5  3.0
>>> cleaned
     0    1    2
0  1.0  6.5  3.0
>>> # 传入 how='all' 过滤整行全为 NAN 的行
>>> data.dropna(how='all')
     0    1    2
0  1.0  6.5  3.0
1  1.0  NaN  NaN
3  NaN  6.5  3.0
```

`fillna` 函数参数

* `value` 用于填充缺失值的标量值或字典对象
* `method` 插值方式 ,默认 `ffill`
* `axis` 填充的轴
* `inplace` 设置是否产生副本
* `limit` 可以连续填充的最大数量

### 移除重复数据

1. `data.duplicated` 

`DataFrame` 的 `duplicated` 方法返回一个布尔型 `Series`，表示各行是否是重复行（前面出现过的行）

````python
>>> data = pd.DataFrame({'k1': ['one', 'two'] * 3 + ['two'],
                         'k2': [1, 1, 2, 3, 3, 4, 4]})
>>> data
    k1  k2
0  one   1
1  two   1
2  one   2
3  two   3
4  one   3
5  two   4
6  two   4
>>> data.duplicated()
0    False
1    False
2    False
3    False
4    False
5    False
6     True
dtype: bool
````

2. `data.duplicates()`

```python
>>> # 根据参数 keep 选择删除那些行
>>> data.duplicates(['k1', 'k2'], keep='last')
    k1  k2  v1
0  one   1   0
1  two   1   1
2  one   2   2
3  two   3   3
4  one   3   4
6  two   4   6
```

### 利用函数或映射进行数据转换

`Series` 的 `map` 方法可以接受一个函数或含有映射关系的字典型对象

```python
>>> data = pd.DataFrame({'food': ['bacon', 'pulled pork', 'bacon',
                                 'Pastrami', 'corned beef', 'Bacon',
                                 'pastrami', 'honey ham', 'nova lox'],
                      'ounces': [4, 3, 12, 6, 7.5, 8, 3, 5, 6]})
>>> data 
          food  ounces
0        bacon     4.0
1  pulled pork     3.0
2        bacon    12.0
3     Pastrami     6.0
4  corned beef     7.5
5        Bacon     8.0
6     pastrami     3.0
7    honey ham     5.0
8     nova lox     6.0
>>> meat_to_animal = {
  'bacon': 'pig',
  'pulled pork': 'pig',
  'pastrami': 'cow',
  'corned beef': 'cow',
  'honey ham': 'pig',
  'nova lox': 'salmon'
}
>>> # 用 str.lower() 将 Series 元素转为小写
>>> lowercased = data['food'].str.lower()
>>> # map 映射(字典)
>>> data['animal'] = lowercased.map(meat_to_animal)
>>> data
          food  ounces  animal
0        bacon     4.0     pig
1  pulled pork     3.0     pig
2        bacon    12.0     pig
3     Pastrami     6.0     cow
4  corned beef     7.5     cow
5        Bacon     8.0     pig
6     pastrami     3.0     cow
7    honey ham     5.0     pig
8     nova lox     6.0  salmon
>>> # map 映射(函数)
>>> data['food'].map(lambda x: meat_to_animal[x.lower()])
0       pig
1       pig
2       pig
3       cow
4       cow
5       pig
6       cow
7       pig
8    salmon
Name: food, dtype: object
```

### 替换值

`data.replace` 替换元素

```python
>>> data = pd.Series([1., -999., 2., -999., -1000., 3.])
>>> data
0       1.0
1    -999.0
2       2.0
3    -999.0
4   -1000.0
5       3.0
>>> # replace 中用参数 value 替换 to_replace 并返回一个新参数, value 和 to_replace 可以是列表/字典/正则/字串/Series/int/float/None
>>> # list: data.replace([a, b], c) or replace([a, b], [c, d])
>>> # dict: data.repalce({a:c, b:d})
>>> data.replace(-999, np.nan)
0       1.0
1       NaN
2       2.0
3       NaN
4   -1000.0
5       3.0
dtype: float64
```

### 重命名轴索引

和 `Series` 中的值一样,轴标签也可以通过 `map` 进行函数或映射进行转换

```python
>>> d2 = pd.DataFrame(np.arange(12).reshape((3, 4)),
                    index=['Ohio', 'Colorado', 'New York'],
                     columns=['one', 'two', 'three', 'four'])
>>> # 创建函数
>>> transform = lambda x: x.upper()
>>> # map 进行转换
>>> d2.index = d2.index.map(transform)
>>> d2
one  two  three  four
OHIO    0    1      2     3
COLO    4    5      6     7
NEW     8    9     10    11
```

`rename` 转换的同时创建新数据,不修改原数据

```python
>>> d2.rename(index=str.title, columns=str.upper)
one  two  peekaboo  four
INDIANA    0    1         2     3
COLO       4    5         6     7
NEW        8    9        10    11
```

### 离散化和面元划分

1. `cut`

`pandas.cut` 将连续数据进行离散化或拆分为面元(bin),返回一个 `Categorical` 对象

```python
cut(x, bins, right=True, labels=None, retbins=False, precision=3,include_lowest=False, duplicates='raise')
```

可以传递一个数组或列表到 `labels` 参数,设置离散名称.`precision` 设置浮点型保留的小数位,`right` 为 `True` 左开右闭,为 `False` 左闭右开.

通过设置 `bins` 参数,将 `x` 分割, 当 `bins` 传入的是整数而不是确切的边界时, `cut` 函数会根据数据的最小值和最大值计算等长区间.

```python
>>> data = np.random.randn(20)
>>> # 传入 4 时分四份等长区间,可以传入具体数值
>>> # 如 [-2, -1, 0, 1, 2, 3]
>>> cats = pd.cut(data, 4, precision=2)
[(-0.56, 0.61], (-1.73, -0.56], (0.61, 1.77], (-0.56, 0.61], (-0.56, 0.61], ..., (-1.73, -0.56], (-0.56, 0.61], (-1.73, -0.56], (-1.73, -0.56], (0.61, 1.77]]
Length: 20
Categories (4, interval[float64]): [(-1.73, -0.56] < (-0.56, 0.61] < (0.61, 1.77] < (1.77, 2.93]]
>>> # codes 属性显示 data 中的每个数据属于那一个区间,每个元素对应的是区间的下标
>>> cats.codes
array([1, 0, 2, 1, 1, 2, 3, 2, 2, 1, 1, 1, 0, 1, 2, 0, 1, 0, 0, 2],
      dtype=int8)
>>> # value_counts() 计算每个分类的元素个数,返回 Series
>>> pd.value_counts(cats)
(-1.73, -0.56]    5
(-0.56, 0.61]     8
(0.61, 1.77]      6
(1.77, 2.93]      1
dtype: int64
 >>> # labels 设置名称
 >>> group_names = ['A', 'B', 'C', 'D']
 >>> pd.cut(data, 5, labels=group_names)
 [B, A, C, B, B, ..., A, B, A, A, C]
Length: 20
Categories (4, object): [A < B < C < D]
```

2. `qcut` 类似 `cut` 函数,而 `qcut` 会等分的切割所有数据

```python
>>> data = np.random.randn(1000)
>>> cats = pd.qcut(data, 4)
>>> cats
[(-3.33, -0.657], (0.00481, 0.69], (0.69, 3.824], (-3.33, -0.657], (-3.33, -0.657], ..., (0.00481, 0.69], (-3.33, -0.657], (0.00481, 0.69], (-0.657, 0.00481], (0.69, 3.824]]
Length: 1000
Categories (4, interval[float64]): [(-3.33, -0.657] < (-0.657, 0.00481] < (0.00481, 0.69] < (0.69, 3.824]]
>>> pd.value_counts(cats)
(0.69, 3.824]        250
(0.00481, 0.69]      250
(-0.657, 0.00481]    250
(-3.33, -0.657]      250
dtype: int64
 >>> # 自定义分位 (0-1 之间的数字,表示每个区间数据数)
 >>> pd.qcut(data, [0, 0.1, 0.6, 0.9, 1.])
 [(-3.33, -1.195], (-1.195, 0.257], (1.259, 3.824], (-1.195, 0.257], (-1.195, 0.257], ..., (0.257, 1.259], (-3.33, -1.195], (0.257, 1.259], (-1.195, 0.257], (0.257, 1.259]]
Length: 1000
Categories (4, interval[float64]): [(-3.33, -1.195] < (-1.195, 0.257] < (0.257, 1.259] < (1.259, 3.824]]
>>> pd.value_counts(cats)
(-1.195, 0.257]    500
(0.257, 1.259]     300
(1.259, 3.824]     100
(-3.33, -1.195]    100
dtype: int64
```

### 检测和过滤异常值

利用数组运算实现过滤异常值

```python
>>> # 生成一个正态分布的 DataFrame
>>> data = pd.DataFrame(np.random.randn(1000, 4))
>>> data.describe()
>>> # 找出某列绝对值大于 3 的值
>>> col = data[2]
>>> col[np.abs(col) > 3]
127    3.953111
525    3.279284
595    3.022792
748   -4.068894
864   -3.602331
990    3.335121
Name: 2, dtype: float64
>>> # 选出全部绝对值大于 3 的行,用 any
>>> data[(np.abs(data) > 3).any(1)]
```

替换过滤出来的值

```python
>>> # 将绝对值大于 3 的值替换
>>> # np.sign 广播到每个值,判断值是否大于/小于/等于 0,并返回1/-1/0
>>> data[np.abs(data) > 3] = np.sign(data) * 3
```

### 排列和随机采样

利用 `numpy.random.permutation` 函数实现对 `Series` 或 `DataFrame` 的排列,

```python
>>> df = pd.DataFrame(np.arange(20).reshape((5, 4)))
>>> sampler = np.random.permutation(5)
>>> df.take(sampler)
>>> # 默认不替换原数据,可用 replace 设置
>>> da.sample(n=3)
```

### 计算指标/哑变量



## 字符串操作

### Python 内置对字符串的处理



### 正则



### pandas 的矢量化字符串函数



## 数据规整: 聚合/合并/重塑

### 层次化索引

层次索引(hierarchical indexing)让一个轴上有多个索引级别,能以低纬度刑事处理高纬度数据.

```python
>>> data = pd.Series(np.random.randn(9),
                     index=[['a', 'a', 'a', 'b', 'b', 'c', 'c', 'd', 'd'],
                            [1, 2, 3, 1, 3, 1, 2, 2, 3]])
>>> data
a  1   -1.019705
   2    0.737992
   3    1.063738
b  1    1.874544
   3   -1.679447
c  1   -0.614820
   2   -0.789583
d  2   -0.485948
   3   -1.960032
dtype: float64
>>> # 用 index 属性可以查看到带有 MultiIndex 索引的 Series 格式
>>> data.index
MultiIndex(levels=[['a', 'b', 'c', 'd'], [1, 2, 3]],
           labels=[[0, 0, 0, 1, 1, 2, 2, 3, 3], [0, 1, 2, 0, 2, 0, 1, 1, 2]])
```

对于层次化索引对象,可以使用部分索引,来选取数据子集

```python
>>> # 外层索引
>>> data['b']
1    1.874544
3   -1.679447
dtype: float64
>>> data['b':'c']
b  1    1.874544
   3   -1.679447
c  1   -0.614820
   2   -0.789583
dtype: float64
>>> data[['b', 'd']]
b  1    1.874544
   3   -1.679447
d  2   -0.485948
   3   -1.960032
dtype: float64
    
>>> # 内层索引
>>> data.loc[:, 2]
a    0.737992
c   -0.789583
d   -0.485948
dtype: float64
```

层次化索引多用于数据重塑和基于分组的操作(透视表生成).

```python
>>> # 通过 unstack 方法重新将数据排到一个 DataFrame
>>> data.unstatck()
          1         2         3
a -1.019705  0.737992  1.063738
b  1.874544       NaN -1.679447
c -0.614820 -0.789583       NaN
d       NaN -0.485948 -1.960032
>>> # 逆运算 DataFrame to hierarchical indexing
>>> data.unstack().stack()
```

`DataFrame` 中的每条轴(行/列)都可以有分层索引,每层都可以有名字

```python
>>> # 行索引/列索引同时分层
>>> frame = pd.DataFrame(np.arange(12).reshape((4, 3)),
                         index=[['a', 'a', 'b', 'b'], [1, 2, 1, 2]],
                         columns=[['Ohio', 'Ohio', 'Colorado'],
                                  ['Green', 'Red', 'Green']])
>>> frame
     Ohio     Colorado
    Green Red    Green
a 1     0   1        2
  2     3   4        5
b 1     6   7        8
  2     9  10       11
>>> # 命名
>>> frame.index.names = ['key1', 'key2']
>>> frame.columns.names = ['state', 'color']
>>> frame
state      Ohio     Colorado
color     Green Red    Green
key1 key2                   
a    1        0   1        2
     2        3   4        5
b    1        6   7        8
     2        9  10       11
```

### 重排与分级排序

`swaplevel` 重新调整某轴上各级别顺序

`sort_index` 根据单个级别中的值对数据进行排序

```python
>>> # swaplevel 可以传入等级索引或等级名称
>>> frame.swaplevel('key1', 'key2')

>>> # sort_index 可以传入等级索引或等级名称
>>> frame.sort_idnex(level=1)

>>> frame.swaplevel(0, 1).sort_index(level='key2')
```

### 根据级别统计

许多对 `DataFrame`  和 `Series` 进行统计时都有一个 `level` 选项,根据 `level` 进行统计

```python
>>> # 继上面 frame 进行求和
>>> # 行
>>> frame.sum(level='key2')
state  Ohio     Colorado
color Green Red    Green
key2                    
1         6   8       10
2        12  14       16
>>> # 列
>>> frame.sum(level='color', axis=1)
color      Green  Red
key1 key2            
a    1         2    1
     2         8    4
b    1        14    7
     2        20   10
```

### 使用 DataFrame 的列进行索引

`set_index` 方法将列变成行索引

```python
>>> frame2 = pd.DataFrame({'a': range(7), 'b': range(7, 0, -1),
                           'c': ['one', 'one', 'one', 'two', 'two',
                                 'two', 'two'],
                           'd': [0, 1, 2, 0, 1, 2, 3]})
>>> frame2
>>> # 将列设置成索引,drop 参数指定是否保留列
>>> frame3 = frame2.set_index(['c', 'd'])
>>> frame3
       a  b
c   d      
one 0  0  7
    1  1  6
    2  2  5
two 0  3  4
    1  4  3
    2  5  2
    3  6  1
```

`reset_index` 与 `set_index` 功能相反,将层次化索引移到列

### 合并数据集

`Pandas` 对象中的数据可以进行合并

* `pandas.merage` : 可以根据一个或多个键将不同的 `DataFrame` 中的行连接,和 `SQL` 中的 `join` 操作类似
* `pandas.concat` 可以沿一条轴将多个对象堆叠到一起
* 实例方法 `combine_first` : 可以将重复数据拼接在一起,用一个对象中的值填充另一个对象中的缺失值

1. **类数据库的 DataFrame 合并**

```python
>>> df1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'a', 'b'],
                        'data1': range(7)})
>>> df2 = pd.DataFrame({'key': ['a', 'b', 'd'],
                        'data2': range(3)})
>>> # merge 通过 on 参数指定合并的键
>>> # how 参数指定合并方式,有内联(inner=>键的交集)/外联(outer=>键的并集)/左右连(left/right=>使用左右表的键), 默认内联
>>> pd.merge(df1, df2, on='key')
   data1 key  data2
0      0   b      1
1      1   b      1
2      6   b      1
3      2   a      0
4      4   a      0
5      5   a      0
>>> # 多对多连接产生的是行的笛卡尔积,即左右两边相同的合并键的积,
>>> pd.merge(df1, df2, on='key', how='left')
  key  data1  data2
0   b      0    1.0
1   b      1    1.0
2   a      2    0.0
3   c      3    NaN
4   a      4    0.0
5   a      5    0.0
6   b      6    1.0
```

两个对象的列名不相同时,可以分别进行指定

```python
>>> df3 = pd.DataFrame({'lkey': ['b', 'b', 'a', 'c', 'a', 'a', 'b'],
                        'data1': range(7)})
>>> df4 = pd.DataFrame({'rkey': ['a', 'b', 'd'],
                        'data2': range(3)})
>>> # left_on/right_on 指定不同列名进行合并
>>> pd.merge(df3, df4, left_on='lkey', rkey='rkey')
   data1 lkey  data2 rkey
0      0    b      1    b
1      1    b      1    b
2      6    b      1    b
3      2    a      0    a
4      4    a      0    a
5      5    a      0    a
```

多个键进行合并,返回的键组合取决于**合并方式**

```python
>>> left = pd.DataFrame({'key1': ['foo', 'foo', 'bar'],
                     'key2': ['one', 'two', 'one'],
                     'lval': [1, 2, 3]})
>>> right = pd.DataFrame({'key1': ['foo', 'foo', 'bar', 'bar'],
                      'key2': ['one', 'one', 'one', 'two'],
                      'rval': [4, 5, 6, 7]})
>>> # 多键合并, on 传入一个列表,
>>> pd.merge(left, right, on=['key1', 'key2'], how='outer')
  key1 key2  lval  rval
0  foo  one   1.0   4.0
1  foo  one   1.0   5.0
2  foo  two   2.0   NaN
3  bar  one   3.0   6.0
4  bar  two   NaN   7.0
```

`merge` 参数

![](https://github.com/Dxigui/Notes/blob/master/img/merge_args2.png)

![](https://github.com/Dxigui/Notes/blob/master/img/merge_args3.png)

2. **索引合并**

当 `DataFrame` 中的连接键在 `index` 中时,可以传入 `left_index=True` 或 `right_index=True`(或者两个都传入),以说明以那侧索引做连接键

* 列和索引合并: `pd.merge(left, right, left_on='key', right_index=True`
* 多列和层次索引合并: `pd.merge(left, right, left_on=['key1', 'key2'], right_index=True`
* 索引和索引: `pd.merge(left, right, how='outer', left_index=True, right_index=True)`

3. **轴向连接**

在 `NumPy` 中可以通过 `np.concatenation` 实现轴连接.

`Pandas` 中用 `pd.concat` 进行轴连接

* **对于 Series** 对象

`pd.concat` 通过指定 `axis` 决定产生新的 `Series(xies=0)` 还是 `DataFrame(axis=1)` ,

`join` 参数指定连接方式 `inner/outer` 默认 `outer`

`keys` 参数在时可以抽象出一个层次索引 `pd.concat([s1, s2, s3], axis=1, keys=['one','two', 'three'])` ,同样可以通过 `axis` 指定行列

* **对于 DataFrame 对象**

对于 `DataFrame` 这些规则同样适用

```python
>>> df1 = pd.DataFrame(np.arange(6).reshape(3, 2), index=['a', 'b', 'c'],
                       columns=['one', 'two'])
>>> df2 = pd.DataFrame(5 + np.arange(4).reshape(2, 2), index=['a', 'c'],
                       columns=['three', 'four'])

>>> pd.concat([df1, df2], axis=1 keys=['level1', 'level2'])
  level1     level2     
     one two  three four
a      0   1    5.0  6.0
b      2   3    NaN  NaN
c      4   5    7.0  8.0
>>> # 如果传入一个字典,那么字典的键会当做 keys 选项
>>> pd.concat({'level1': df1, 'level2': df2}, axis=1)
  level1     level2     
     one two  three four
a      0   1    5.0  6.0
b      2   3    NaN  NaN
c      4   5    7.0  8.0
```

如果 `DataFrame` 没有行索引,是 `Pandas` 默认的,连接时会出现行索引相同的问题,这时需要设置 `ignore_index=True` 

![](https://github.com/Dxigui/Notes/blob/master/img/pd_concat.png)

### 合并重叠数据

`NumPy` 中的 `where`  也可以实现两个 `Series` 合并

```python
>>> a = pd.Serise()
>>> b = pd.Series()
>>> np.where(pd.isnull(a), b, a)
```

`combine_first`

### 重塑和轴向旋转

1. **重塑层次化索引**
   * `stack` 方法: 将数据的列转成行
   * `unstack` 方法: 将数据的行转为列






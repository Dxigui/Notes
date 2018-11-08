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
>>> # 跳过文本的某一些行数
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



## 数据清洗和准备

## 处理缺失数据

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

![](/home/dxigui/git_repositories/notes/Notes/img/pandas_io.png)

一般 `read_csv/read_table` 使用最多

`read_csv/read_table` 常用参数

* `nrows` 设定读取的行数
* `chunksize` 设定读取行数,返回一个可迭代对象 `TextParsers`,

![](/home/dxigui/git_repositories/notes/Notes/img/pd_csv_table_args.png)

![](/home/dxigui/git_repositories/notes/Notes/img/pd_csv_table_args2.png)




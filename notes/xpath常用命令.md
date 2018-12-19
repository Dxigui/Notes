## XPath 常用命令

XPath 是一门在 XML 文档中查找信息的语言,XPath 可用来在 XML 文档中对元素和属性进行遍历.

XPath 是 W3C 标准.



### XPath 节点选取

```xml
# 示例 XML
<?xml version="1.0" encoding="ISO-8859-1"?>

<bookstore>

<book>
  <title lang="eng">Harry Potter</title>
  <price>29.99</price>
</book>

<book>
  <title lang="eng">Learning XML</title>
  <price>39.95</price>
</book>

</bookstore>
```



1. 常用的路径表达式

| 表达式   | 描述                                 |
| -------- | ------------------------------------ |
| nodename | 选取此节点的所有子节点               |
| /        | 从根节点选取                         |
| //       | 从匹配选择的当前节点选择文档中的节点 |
| .        | 选取当前节点                         |
| ..       | 选取当前节点的父节点                 |
| @        | 选取属性                             |

示例:

| 路径表达式      | 结果                                                         |
| --------------- | ------------------------------------------------------------ |
| bookstore       | 选取 bookstore 元素的所有子节点                              |
| /bookstore      | 选取根元素 bookstore,如果某路径的起始是 / 表示该元素的绝对路径 |
| bookstore/book  | 选取属于 bookstore 的子元素的所有 book 元素                  |
| //book          | 选取所有 book 子元素, 不管他们它文档中的位置                 |
| bookstore//book | 选择属于 bookstore 元素的后代所有 book 元素,而不管他们位于 bookstore 之下的什么位置 |
| //@lang         | 选取名为 lang 的所有属性                                     |

2. Predicates (谓语)

用来查找某个特定的节点或者包含某个指定的值的节点,谓语都嵌在方括号中.

| 路径表达式                         | 结果                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| /bookstore/book[1]                 | 选取属于 bookstore 子元素的第一个 book 元素                  |
| /bookstore/book[last()]            | 选取属于 bookstore 子元素的最后一个 book 元素                |
| /bookstore/book[last()-1]          | 选取属于 bookstore 子元素的倒数第二个 book 元素              |
| /bookstore/book[position()<3]      | 选取最前面的两个属于 booksotre 元素的子元素的 book 元素      |
| //title[@lang]                     | 选取所有拥有名为 lang 的属性的 title 元素                    |
| //title[@lang='eng']               | 选取所有 title 元素,且这些元素拥有值为 eng 的 lang 属性      |
| /bookstore/book[price>35.00]       | 选取 bookstore 元素的所有 book 元素,且其中的 price 元素的值须大于 35.00 |
| /bookstore/book[price>35.00]/title | 选取 bookstore 元素中的 book 元素的所有 title 元素,且其中 price 的值须大于 35.00 |

3. 通配符

| 通配符 | 描述               |
| ------ | ------------------ |
| *      | 匹配任何元素节点   |
| @*     | 匹配任何属性节点   |
| node() | 匹配任何类型的节点 |

4.  | 运算符

| 路径表达式                       | 结果                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| //book/title \| //book/price     | 选取 book 元素的所有 title 和 price 元素                     |
| //title \| //price               | 选取文档中所有 title 和 price 元素                           |
| /bookstore/book/title \| //price | 选取属于 bookstore 元素的 book 元素的所有 title 元素,以及文档中所有 price 元素 |

### XPath 轴

轴可以定义相对于当前节点的节点集

| 轴名称             | 结果                                                     |
| ------------------ | -------------------------------------------------------- |
| ancestor           | 选取当前节点的所有先辈（父、祖父等）。                   |
| ancestor-or-self   | 选取当前节点的所有先辈（父、祖父等）以及当前节点本身。   |
| attribute          | 选取当前节点的所有属性。                                 |
| child              | 选取当前节点的所有子元素。                               |
| descendant         | 选取当前节点的所有后代元素（子、孙等）。                 |
| descendant-or-self | 选取当前节点的所有后代元素（子、孙等）以及当前节点本身。 |
| following          | 选取文档中当前节点的结束标签之后的所有节点。             |
| namespace          | 选取当前节点的所有命名空间节点。                         |
| parent             | 选取当前节点的父节点。                                   |
| preceding          | 选取文档中当前节点的开始标签之前的所有节点。             |
| preceding-sibling  | 选取当前节点之前的所有同级节点。                         |
| self               | 选取当前节点。                                           |

1. 轴结合步语法

   语法格式: `轴名称::节点测试[谓语]`

示例:

| 示例                   | 结果                                     |
| ---------------------- | ---------------------------------------- |
| child::book            | 选取所有属性当前节点的子元素的 book 节点 |
| attribute::lang        | 选取当前节点的 lang 属性                 |
| child::*               | 选取当前节点的所有子元素                 |
| attribute::*           | 选取当前节点的所有属性                   |
| child::text()          | 选取当前节点的所有文本子节点             |
| child::node()          | 选取当前节点的所有子节点                 |
| descendant::book       | 选取当前节点的所有 book 后代             |
| ancestor::book         | 选取当前节点的所有 book 先辈             |
| ancestor-or-self::book | 选区当前节点的所有 book 先辈以及当前节点 |
| child::*/child::price  | 选取当前节点的所有 price 孙节点          |

### XPath 运算符

| 运算符 | 描述           | 实例                      | 返回值                                                       |
| ------ | -------------- | ------------------------- | ------------------------------------------------------------ |
| \|     | 计算两个节点集 | //book \| //cd            | 返回所有拥有 book 和 cd 元素的节点集                         |
| +      | 加法           | 6 + 4                     | 10                                                           |
| -      | 减法           | 6 - 4                     | 2                                                            |
| *      | 乘法           | 6 * 4                     | 24                                                           |
| div    | 除法           | 8 div 4                   | 2                                                            |
| =      | 等于           | price=9.80                | 如果 price 是 9.80，则返回 true。如果 price 是 9.90，则返回 false。 |
| !=     | 不等于         | price!=9.80               | 如果 price 是 9.90，则返回 true。如果 price 是 9.80，则返回 false。 |
| <      | 小于           | price<9.80                | 如果 price 是 9.00，则返回 true。如果 price 是 9.90，则返回 false。 |
| <=     | 小于或等于     | price<=9.80               | 如果 price 是 9.00，则返回 true。如果 price 是 9.90，则返回 false。 |
| >      | 大于           | price>9.80                | 如果 price 是 9.90，则返回 true。如果 price 是 9.80，则返回 false。 |
| >=     | 大于或等于     | price>=9.80               | 如果 price 是 9.90，则返回 true。如果 price 是 9.70，则返回 false。 |
| or     | 或             | price=9.80 or price=9.70  | 如果 price 是 9.80，则返回 true。如果 price 是 9.50，则返回 false。 |
| and    | 与             | price>9.00 and price<9.90 | 如果 price 是 9.80，则返回 true。如果 price 是 8.50，则返回 false。 |
| mod    | 计算除法的余数 | 5 mod 2                   | 1                                                            |

### XPath 函数

[XPath 函数](http://www.w3school.com.cn/xpath/xpath_functions.asp)


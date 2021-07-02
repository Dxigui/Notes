# JavaScript

1. 什么是 JavaScript

   JavaScript 是一种运行在客户端的脚本语言

   组成：

   * ECMAScript: js 语法
   * DOM: 页面文档对象模型
   * BOM: 浏览器对象模型

2. 输出

   prompt 接受用户输入

   document.write() 写入 HTML 输出

   innerHTML 写入 HTML 元素

3. 变量



4. 关键词 
   * `var`  用于声明变量
   * console` 调用控制台
   * typeof 确定变量类型：typeof 会把对象、数组或 Null 返回 object；函数返回 function；undefined 返回 undefined；比较两个变量是否为同一类型用 **==** ；**`===`**  三个等号为变量的值比较，看是否相等



5. 数据类型

   字符串；数值；布尔值；数组；对象；Null

   

   ##### 字符串转义：`\`

   *  `\n ` 换行
   * `\\` 转义反斜杠
   * `\'` 转义单引号
   * `\"` 转义双引号
   * `\t` tab 缩进
   * `\b` 空格

   注意：

   `var s = 939 + "name"`  ` s = "939name"` 其他数据类型与字符串合并时会把数字转为字符串后合并

   字符串拼接：+

   ##### 数据类型转换

   * 变量.tostring() | String(变量)    转字符串

   * parseInt(变量)   转数值类型，只能转成整数，忽略小数点后的值，同时含数字和字母时，只会转数字

   * parseFloat(变量) 转数值类型，能转浮点型，同时也会去字符

     `parseInt('123ps') >> 123`

   * 算术运算 ` - *` 减和乘      `'123' - 0 >> 123`

   * Boolean(变量); 转布尔值 变量为 `'', 0, NaN, Null, undedined` 5个时为 False，其他为 True
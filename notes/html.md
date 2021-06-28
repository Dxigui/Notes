1. Web 标准的构成

   主要包括结构，表现和行为三方面

   结构：结构用于对 网页元素 进行整理和分类，HTML

   表现：表现用于设置网页元素的版式，颜色，大小等外观样式, CSS

   行为：行为是王爷模型的定义及交互的编写，Javascript

2. `<!DOCTYPE>` 文档类型的声明标签

3. 标签

   标题标签：`<h1>`到`<h6>`

   段落标签：`<p>`

   换行标签：`<br />`单标签，没有段落间距

   注释标签：`<!-- 内容 -->`

   3.2 文本格式化,突出文字重要性

   ​	文本加粗：`<strong>,<b>`

   ​	文字倾斜：`<em>,<i>`

   ​	删除线：`<del>,<s>`

   ​	下划线： `<ins>,<u>`

   3.3 

   ​	盒子标签：`<div>,<span>` 

   3.4 图像标签 `<img src="" />`

   ​	单标签，src 是必须属性，指定图像路径

   ​	alt 属性：替换文本，当图片不能显示时

   ​	title 属性： 提示文本，

   ​	width 属性：像素高度

   ​	height 属性：像素宽度

   ​	border 属性：边框

   3.5 超链接标签：`<a>` 

   ​	href 属性：必须属性，目标地址

   ​	target 属性：目标窗口打开方式，`_self` 当前页面打开；`_blank` 新页面打开

   3.6 锚点链接 

   ​	超链接 href 属性的值为目标标签的 id 值，`<a href="#mubiaoid">`` <h1 id="mubiaoid”>`

   3.7 特殊字符

   ​	空格： &nbsp；

   ​	小于号：&lt；

   ​	大于号： &gt；

   3.8 表格标签

   ​	`<table>`：表标签

   ​		align 属性：表格对其方式，center，left，right

   ​		border 属性：边框

   ​		cellpadding 属性：单元格中文字和单元格距离

   ​		cellspacing 属性：单元格与单元格的距离

   ​		width 属性：单元格宽度

   ​		height 属性：单元格高度

   ​	`<tr>` : 行，表标签内嵌标签

   ​	`<td>` : 列，行标签内嵌标签

   ​	`<th>`: 表头标签

   ​	`<thead>`和`<tbody>` : 表格的头部区域和主体部分

   ​	跨行合并单元格：rowspan，最上侧单元格为目标单元格，写合并代码

   ​	跨列合并单元格：colspan，最左侧单元格为目标单元格，写合并代码

   3.9 有序列表，无序列表，自定义列表

   	1. 无序列表：`<ul>;<li>`
   	2. 有序列表：`<ol>;<li>`
   	3. 自定义列表: `<dl> `父标签, `<dt>` 列表头, `<dd>` 列表内容
   	去列表前面符号 list-style: none;

   3.10 表单

   ​	`form`标签：action url 地址；method 提交方法 get/post；name 名称

   ​	label 标签：为 input 元素定义标注，用于绑定表单元素，通过 id 绑定

   ​		` <label for='sex'> 男 </label> <input type='radio' id='sex'>` 

   ​	input 表单元素：单标签，根据 type 属性修改表单内容

   ​	select：下拉表单元素

   ​	textarea：文本域

   ​	1.type 属性

   ​		text：文本框，任何内容

   ​		password：密码

   ​		radio：单选按钮

   ​		checkbox：复选框

   ​		submit：提交按钮

   ​		reset：重置按钮

   ​		button：可点击按钮，配合 js

   ​		file：文件

   ​		

   ​	2.name 属性：定义 input 元素名称

   ​	3.value 属性：设置 input 默认值

   ​	4.maxlength 属性：输入的最长字符长度， 值为整数

   ​	5.checked 属性：单选或复选默认选择，checked=“checked”

   ​		

4.  相对路径和绝对路径

5. 
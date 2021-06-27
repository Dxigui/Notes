 

1. 内部样式, 行内样式, 外部样式

   内部样式放在 html 页面中的 head 标签中,也称嵌入式.行内样式直接在标签中添加 css 样式,只能修改当前标签样式, 权重最高. 单独使用 CSS 文件,HTML 页面使用 link 标签调用.

2. Emmet 语法

   * 生成多个标签 > 标签 * 数量 > p*3
   * 直接定义类名或 id 标签 > 标签.(#)类名(id 名) > p.(#)nav
   * 生成多个时在类名后乘数字 > .类名$*5 > .demo$ * 5 . $ 限定从 1 开始并自增
   * 标签里面生成内容 > 标签{内容} > p{这是内容}
   * 格式化代码 shift + alt + f

3. CSS 选择器

   1. 基础选择器

      标签选择器, 类选择器, id 选择器 和 通配符选择器

   2. 复合选择器

      由两个或多个选择器,通过不同方式组合而成,能更准确,更高效选择目标元素,包含*后代选择器* ,*子选择器* ,**并集选择器**, **伪类选择器**

      * 后代选择器

      * 子选择器: 大于号 元素 > 元素 ; div > p

      * 并集选择器:同时对多个元素修改样元素可以是任何选择器; 选择器, 选择器   div, .nav li

      * 伪类选择器: 冒号

        链接伪类选择器: a:link(为访问的链接);a:visited(访问过的链接); a:hover(鼠标经过的链接); a:active(鼠标点击未弹起链接)

        :focus 选取获得焦点的元素选择出,一般用于表单中 input 元素

4. 元素显示模式

   **块元素**和**行内元素**

   1. 块元素

      独占一行,能被修改高度,宽度,行边距,是一个容器, <p> <h1> 中不能放 <div>

   2. 行内元素

      <a> ; <strong> ; <b> ; <em> ; <i> ; <del> ; <s> ; <ins> ; <u> ; <span> 

      一行可以多个行内元素,无法设置宽高,只能放文本或其他行内元素,

   3. 行内块元素

      同时具备块元素又有行内元素特点: <img /> <input /> <td>

   4. 元素转换

      行内元素转换成块元素: display: block;

      块元素转换成行内元素: display: inline;

      行内元素转行内块: display: inline-block;

5. CSS 背景

   1. 背景颜色

      background-color: transparent/颜色值 ; 背景颜色透明或具体颜色 

   2. 背景图片

      background-image: none | url(url)

   3. 背景平铺

      background-repeat: no-repeat | repeat | repeat-x| repeat-y

   4. 图片位置

      background-position: 方位名词 | 具体像素

   5. 背景图固定

      background-attachment: scroll | fixed;  滚动 | 固定

   6. 复合写法

      background: 背景颜色 | 地址 | 平铺 | 图像滚动 | 图片位置

   7. 背景色半透明

      background: rgba(0, 0, 0, 0.4); a 为透明度 1~0 之间

6. CSS 三大特性

   1. 层叠性

      给相同选择器设置多个样式时会出现**覆盖**,冲突时遵循就近原则,与结构越近的覆盖远的

   2. 继承性

      子元素继承父元素

   3. 优先级

      * 选择器相同: 就近原则
      * 不同选择器看权重: !important > 行内样式 > id 选择器 > 类/伪类选择器 > 元素选择器 > 继承/ * .  eg: color: red!important; 继承的权重是零.复合选择器的**权重会叠加**

7. 盒子模型

   border 边框, padding 内边距, margin 外边距, content 内容

   1. border

      * border-style: solid (实线) | dashed (虚线) | dotted (点线)
      * border-color: 颜色;
      * border-width: 4px; 

      复合 border: 1px solid #fff; 没顺序要求

   2. 
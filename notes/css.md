 

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

        链接伪类选择器: a:link(未访问的链接);a:visited(访问过的链接); a:hover(鼠标经过的链接); a:active(鼠标点击未弹起链接)

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

      盒子会和边框叠加,

      * border-style: solid (实线) | dashed (虚线) | dotted (点线)
      * border-color: 颜色;
      * border-width: 4px; 

      复合 border: 1px solid #fff; 没顺序要求

      * border-collapse: collapse; 合并相邻边框

   2. padding

      padding-left/right/top/buttom: 10px;

      复合

      * padding: 5px; 上下左右都是 5px
      * padding: 5px 10px; 上下 5px; 左右 10px
      * padding:5px 10px 20px; 上 5px 左右 10px 下 20px
      * padding: 5px 10px 20px 30px; 上 右 下 左

   3. margin

      margin-top/left/buttom/right: 10px;

      复写和 padding 一样; 外边距可以使块级盒子**水平居中** ,但盒子必须要有高度且**左右外边框**都设置成 auto; eg: margin: 0 auto;

      父元素中套嵌子盒子时,会出现塌陷(父子盒子同时给外边距时,父元素和子元素的边距会重叠,并且外边距大小取决于外边距大的). 解决方法

      * 给父元素定义边框
      * 给父元素定义内边框
      * 给父元素添加 overflow: hidden;

   4. 圆角边框

      border-radius: 像素 | 百分比;

   5. 盒子阴影

      box-shadow: h-shadow(水平阴影必须) v-shadow(垂直阴影必须) blur(模糊距离可选) spread(阴影尺寸可选) color(颜色可选);

      不占用空间

   6. 文字阴影

      text-shadow:h-shadow(水平阴影必须) v-shadow(垂直阴影必须) blur(模糊距离可选)  color(颜色可选);
   
8. 浮动

   传统网页布局三种方式: **标准流(文档流/普通流)**;**浮动**; **定位**; 一个网页基本包含这三种布局方式

   * 标准流: 标签按照规定好得默认方式排列

     * 块级元素会独占一行,

       div; hr; p; h1~h6; ul; ol; dl; form; table

     * 行内元素按顺序从左至右排列,遇到父元素边缘自动换行

       span; a; i; em;

   * 浮动

     用于创建浮动框,将其移动到一边,直到触及边缘或另一个浮动框边缘

     选择器 {float: none | left | right;}

     + 特性

       1. 浮动元素会**脱离标准流**(俗称脱标)

       2. 浮动元素会在一行内显示元素并顶部对齐

       3. 浮动元素会具有行内块元素特性

          任何元素都可以浮动, 浮动后具有行内块元素相似特性, 行内元素变行内块, 块变行内块

          块级盒子如果没设置宽度,浮动后得大小根据内容来定

          浮动的盒子中间没有间隙,紧挨一起

          配合标准流的父级盒子使用, 用父级元素约束浮动盒子, 父盒子一般不给高度,

          浮动只会影响后面的标准流, 不会影响前面的标准流

     + 清除浮动

       + 选择器 {clear: both | left |  right} ;本质是**闭合浮动** ,让浮动只在父盒子中生效, 让没有设置高度的父盒子包裹浮动的子盒子

       + 额外标签法也称隔墙法, W3C 推荐做法

         在浮动元素末尾添加空标签, 并设置 clear: both 样式

       + 父级加 overflow 属性

         代码简洁, 但是无法显示溢出部分

       + 父级加 after 元素

         >.clearfix:after {
         >
         >​	content: "";
         >
         >​	display: block;
         >
         >​	height: 0;
         >
         >​	clear: both;
         >
         >​	visibility: hidden;
         >
         >}
         >
         >.clearfix {	

         > /* IE 6,7 兼容 */
         >
         >​	*zoom: 1;
         >
         >}
         >
         >

       + 父级加双伪元素

         >.clearfix:before,
         >
         >.clearfix;after {
         >
         >​	content: "";
         >
         >​	display:table;
         >
         >}
         >
         >.clearfix:after {
         >
         >​	clear: both;
         >
         >}
         >
         >.clearfix {
         >
         > *zoom: 1;
         >
         >}

       

9.  CSS 属性书写顺序

   1. 布局定位属性: display/position/float/clear/visibility/overflow

   2. 自身属性: width/height/margin/padding/border/background
   3. 文本属性: color/gont/text-decoration/text-align/vertical-align/white-space/break-word
   4. 其他属性(CSS3): content/cersor/border-radius/box-shadow/text-shadow/background:linear0gradient...

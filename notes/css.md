 **DAY1**

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

      独占一行,能被修改高度,宽度,行边距,是一个容器, `<p> <h1>` 中不能放 `<div>`

   2. 行内元素

      `<a> ; <strong> ; <b> ; <em> ; <i> ; <del> ; <s> ; <ins> ; <u> ; <span> `

      一行可以多个行内元素,无法设置宽高,只能放文本或其他行内元素,

   3. 行内块元素

      同时具备块元素又有行内元素特点: `<img /> <input /> <td>`

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

      background: rgba(0, 0, 0, 0.4); a 为透明度 1~0 之间background:

   8. radial-gradient() 函数

      用径向渐变创建"图像",其中心有中心点定义

      >background: radial-gradient(shape size at position, start-color, ... , last-color);

      * shape : 确定圆的类型: 默认为 ellipse(椭圆) , circle 圆形
      * size: 定义渐变的大小;
      * position: 定义渐变位置
      *  start-color, ... , last-color: 定义起止颜色, 起止必须有,中间可以定义更多颜色

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
   3. 文本属性: color/font/text-decoration/text-align/vertical-align/white-space/break-word
   4. 其他属性(CSS3): content/cursor/border-radius/box-shadow/text-shadow/background:linear-gradient...

## DAY3

10. 定位

    定位 = 定位模式 + 边偏移

    **定位模式**用于指定一个元素在文档中的定位方式

    **边偏移** 则决定该元素的最终位置

    

    * 定位模式

      position: static(静态定位) | relative(相对定位) | absolute(绝对定位) | fixed(固定定位)

    * 边偏移

      top | bottom | left | right: 像素;

    1.  静态定位相当于标准流

    2.  相对定位: 相对于自己原来的位置来移动, 原位置继续占有,其他元素不能占有

    3. 绝对定位: 相对父元素移动,绝对定位的盒子不能用 margin:auto 来水平居中

       * 没有父元素或父元素没有定位则以浏览器为准定位

       * 父元素有定位,子元素则定位以父元素为准,父元素没有定位,则以最近的一级带有定位元素为准
       * 绝对定位不占有原来位置

    **子绝父相** :子元素绝对定位时,父元素用相对定位

    4. 固定定位: 固定在浏览器可视窗口, 以浏览器可视窗口定位
       * 和父元素没关系
       * 不随滚动条滚动
       * 不占有原来位置

    5. 粘性定位 : 以浏览器窗口为定位标准

       position: sticky;

       * 占原先位置
       * 必须添加一个 top/left/right/bottom

    6. 定位叠放次序 

       z-index: 正负整数;

       数字越大,元素的定位位置越高,数值最大的在最上面; 如果没有设置,则后来居上,

    7. 定位特殊性

       * 行内元素添加绝对或相对定位,可以设置宽高,和浮动类似
       * 块级元素加绝对或相对定位,如果不设置宽高,盒子为内容宽高
       * 浮动元素, 绝对定位(固定定位),不会出现外边距重合(塌陷)
       * 浮动会覆盖下面标准流盒子,但是不会覆盖盒子中的内容(文字/图片); 但绝对定位(固定定位)会压住标准流所有内容

11. 元素显示和隐藏

    让一个元素在页面中隐藏或显示出来

    * display 显示隐藏
    * visibility 显示隐藏
    * overflow 溢出显示隐藏

    1. display 

       display: none(隐藏元素) | block(显示元素);  **display 隐藏元素后,不在占有原来位置**

    2. visibility

       visibility: visible(元素可视) | hidden(元素隐藏) ; **隐藏元素后,继续占有原来位置**

    3. overflow

       overflow: visible | hidden | auto | scroll

高级技巧

12. 精灵图

    有效减少服务器请求,减少服务器压力

    通过 background-position 实现

13. 字体图标 iconfont

    网页中一些轻量小图标可以使用字体图标. 本质是**文字**

    * 轻量级: 比图像小, 一旦加载立马渲染, 减少服务器请求
    * 灵活性强: 本质是文字,可以改颜色,产生阴影,透明效果等
    * 兼容性强

    icomoon / 阿里 iconfont

14. 三角形实现

    定义一个空盒子,给空盒子加边框

    >div {
    >
    >​	width: 0;
    >
    >​	height: 0;
    >
    >​	line-height: 0;
    >
    >​	font-size: 0;
    >
    >​	border: 5px solid transparent;  /*定义一个 5px 边框并透明 */
    >
    >​	border-top-color: red; /* 根据三角形方向选择 top/left/right/bottom */
    >
    >}
    >
    >

15. 用户界面

    1. 更改鼠标样式

       ​	选择器 { corsor: default | pointer(小手) | move(移动) | text(文本) | not-allowed(禁止) }

    2. 防止拖拽文本域

       ​	textarea {resize: none}

    3. 取消表单轮廓

       ​	input { outline: none}

    4. vertical-line

       ​	让元素垂直对齐方式, 设置图片和文字对齐方式, 只对块和行内块元素有效

       ​	选择器 { vertical-line: bottom(底线对齐) | middle (垂直居中,)}

    5. 图片底部默认空白缝隙问题

       ​	给图片添加 vertical-line: top | bottom | middle

       ​	将图片转为块元素

16. 溢出文字省略号显示

    1. 单行文本

    >/* 三步完成
    >
    >1.让文字强制显示为一行 */
    >
    >white-apace: nowrap;  (默认 normal 自动换行)
    >
    >2.超出部分隐藏
    >
    >overflow: hidden;
    >
    >3.用省略号代替超出部分
    >
    >text-overflow: ellipsis;
    >
    >

    2. 多行文本

    > overflow: hidden;
    >
    > text-overflow: ellipsis;
    >
    > 弹性伸缩盒子模型显示
    >
    > display: -webkit-box;
    >
    > 限制在一个块元素显示的文本的行数
    >
    > -wibkit-line-clamp: 2;
    >
    > 设置或检索伸缩盒对象的子元素的排列方式
    >
    > -webkit-box-orient: vertical;

17. 常见布局

    1. margin 负值

       边框重叠,

    2. 文字围绕浮动元素

    3. 行内块

    4. 直角三角形

       >div {
       >
       >​	width: 0;
       >
       >​	height: 0;
       >
       >​	border-color: transparent red transparent transparent;
       >
       >​	border-width: 10px 5px 0 0;
       >
       >​	border-style: solid;
       >
       >}

18. HTML5 和 CSS3 

    1. HTML5 的新语义化标签

       * header 头部标签
       * nav 导航栏标签
       * article 内容标签
       * section 定义文档某区域
       * aside 侧边栏标签
       * footer 尾部标签

    2. HTML5 新增多媒体标签

       * audio 音频
       * video 视频   <video src="" controls="controls"></video>

    3. HTML5 新增 input 类型

       * type=email 限制输入必须为邮箱
       * url 限制为 URL 类型
       * date 限制作为日期类型
       * time 限制为时间类型
       * month 限制为月类型
       * week 周
       * number 限制为数字
       * tel 手机号码
       * search 搜索框
       * color 生成一个颜色选择表单

    4. HTML5 新增表单属性

       * required="required"  表单拥有该属性表示其内容不能为空,必填
       * **placeholder**="提示文本" 表单的提示信息,存在默认值将不显示
       * autofocus="autofocus" 自动聚焦属性, 页面加载完成自动聚焦到指定表单
       * **multiple**="multiple" 可以多选文件提交
       * autocomplete="off/on" 显示提交历史, off(关)/on(开)

    5. CSS3  新增属性选择器

       选择 HTML 标签中的属性,例: <input value="">  >>>  input[value] {color: red}

       **属性选择器和类选择器,伪类选择器权重一样**

       * E[att] 选择具有 att 属性的 E 元素
       * E[att="val"] 选择具有 att 属性且属性值等于 val 的 E 元素
       * E[att^="val"] 匹配具有 att 属性且值以 val 开头的 E 元素
       * E[att$="val"] 匹配具有 att 属性且值以 val 结尾的 E 元素
       * E[att*="val"] 匹配具有 att 属性且值中含有 val 的 E 元素

    6. 结构伪类选择器

       * E:first-child 匹配父元素中的第一个子元素

       * E:last-child 匹配父元素中的最后一个子元素

       * E:nth-child(n) 匹配父元素的第 n 个元素或多个特定的子元素

         n : n  可以是数字,关键字和公式

         1. 关键字: even 偶数, odd 奇数
         2. 公式: E:nth-child(n| 2n | 2n+1 | 5n | n+5 |-n+5      n 从 0 开始直到所有元素个数
         3. 数字: 具体第 n 个元素

       * E:first-of-type

       * E:last-of-type

       * E:nth-of-type(n)  结果和 nth 一样

       区别:

       ​	E:nth-child(n), 会把所有盒子排列,   执行时先看 :nth-child(n) 然后看 E 是否匹配

       ​	E: nth-of-type(n) , 吧指定元素盒子排列, 执行时先看 E 指定的元素, 再看第几个子元素

    7. 伪元素选择器

       ::before 创建一个元素在父元素前面

       ::after  创建一个元素在父元素后面

       语法: elment::before | after{} ; elment 为父元素
       必须要有 content 属性, **权重和标签选择器一样**

    8. CSS3 新盒子模型

       CSS3 通过 box-sizing 来制定盒子模型, E {box-sizing: content-box | border-box}

       content-box 和以前一样, 盒子大小为 width + padding + border

       border-box 盒子大小为 width, padding 和 border 不会撑大盒子

    9. CSS3 滤镜

       filter

    10. CSS3 calc 函数

        可以进行 + - * /  (加减乘除)

    11. CSS3 过度效果

        transition: 要过渡的属性 花费的时间 运动曲线(默认ease) 何时开始(单位s 默认0)





**DAY4**

19. 网页 LOGO SEO 优化

    div>h1>a{内容(一般为网站名称)}; 同时给 a 标签一个 title 属性

    a 中内容隐藏: overflow:hidden; 或者 text-indent:-299px; +overflow:hidden;

20. tab-list>tab-content 



##### DAY5

21. 2D转换之位移

    transform 移动**不会影响其他元素**, 对行内元素无效; 配合 transition 过渡

    `transform: translate(x, y);`  x y 可以是数值, 也可以是百分比,百分比是相对自身宽高

22. 2D 转换之旋转



​		`transform: rotate(旋转度数deg); `

​		`transform-origin: x y;` 设置旋转中心点



23. 2D 转换之放大

    不会影响对他元素

​		`transform: scale();`

24. 动画

    先定义动画, 然后调用动画

    1. 定义动画

       >@keyframs move{
       >
       >/* 开始状态  0% 和 100% 为动画序列*/
       >
       >0% {
       >
       >​	transform: translateX(0px);
       >
       >}
       >
       >/* 结束状态 */
       >
       >100% {
       >
       >​	transform: translateX(1000px);
       >
       >}
       >
       >}

    2. 使用动画

       >
       >
       >div {
       >
       >animation-name: move;
       >
       >animation-duration: 2s;
       >
       >}

    3. 动画序列

       * from to
       * 0% 100% : 可以是两个阶段,也可以多个阶段; 0% 25% 50% 75% 100%, 形成一个闭环

    4. 属性

       * @keyframs 定义动画并规定动画名
       * animation
       * animation-name : 动画名称
       * animation-duration : 动画完成时间
       * animation-timing-function : 动画速度曲线,默认 ease; steps(步数) 动画完成所需步数
       * animation-delay : 动画何时开始
       * animation-iteration-count : 动画重复次数; 无限循环 infinite
       * animation-direction : 动画是否逆方向播放
       * animation-fill-mode : 动画结束后状态, 默认 backwards(返回起始状态), forwards(保持最后状态)
       * animation-paly-status : 动画暂停和启动,可以配合类选择器 :hover

25. 3D 转换

    父元素定义 perspective: 像素; 才能出现 3d 效果, 相当于视距效果

    1. 3D 移动 translate3d

       * transform: translateX() translateY () translateZ();
       * transform: translate3d (x, y, z);

    2. 3D 旋转 rotate3d() 沿轴选择

       * transform: rotateX(deg) rotateY(deg) rotateZ(deg); 
       * transform: rotate3d(x, y, z,deg);  xyz 定义旋转轴, deg 定义旋转角度

    3. 3D 呈现 transform-style

       控制 3d 效果的开启或关闭;  preserve-3d 开启 3d 环境;默认关闭;給父级添加

##### DAY6

26. 二倍图
    1. background-size: px px | conver |contain ;   
    2. 特殊样式
       * -webkit-box-sizing
       * -webkit-top-highlight-color: transparent;  点击链接高亮清除
       * -webkit-appearance: none;  清除移动端浏览器默认样式
       * img, a {-webkit-touch-callout:none}  禁止长安页面时弹出菜单

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
   * typeof 确定变量类型：typeof 会把对象、数组或 Null 返回 object；函数返回 function；undefined 返回 undefined;



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
   
6. 运算符

   1. 算术运算符

      ` + - * / % `   % 取余

   2. 递增和递减运算符

      `++ --` 

      * 前置自增 : 先自增
      * 后置自增 : 先返回原值再自增

   3. 比较运算符

      ` > ; < ; >= ; <= ; == ; != ; === ; !==`  **==** 可以自动转数值(`12 == '12' 返回ture`) ` === 和 !== ` 必须值和数据类型相等

   4. 逻辑运算符

      ` && ; || ; ! `   短路运算     

   5. 赋值运算符

      ` += ; -= ; *=`  

   6. 运算符优先级

      `()  >> ++;--;! >> *; / ;% >> +;- >> >; >=; <; <= >> ==; !=; ===; !== >> && >> || >> = ` 

7. 流程控制

   1. if else

   2. 三元表达式

      ` 条件表达式 ? 表达式1 : 表达式2;`

      条件表达式为真 返回表达式 1 ,条件表达式为假 返回表达式 2

   3. switch 

      > switch(表达式){
      >
      > ​	case value1:
      >
      > ​		执行语句;
      >
      > ​		break;
      >
      > ​	case value2:
      >
      > ​		执行语句;
      >
      > ​		break;
      >
      > ​	default:
      >
      > ​		执行语句;
      >
      > }
      >
      > // 表达式的返回值和 value 比较,相等则执行, 必须是值和数据类型都相等
      >
      > // break 当 switch 执行到 break 时不再执行后面语句并结束 witch 语句, 没有 break 时,会在执行完 case 后继续执行下一个 case;

   4. 循环

      **for 循环**  ; **while 循环** ; **do while 循环**

      * do while:

        >do{
        >
        >循环体
        >
        >}while(条件表达式)
        >
        >// 先执行循环体, 再进行条件判断, do while 至少循环一次

      * continue / break
   
8. 数组

   1. 创建

      * new 创建: `var arr = new Array();`  创建一个空数组
      * 数组字面量创建: `var arr = [];`  

   2. slice()

      和字符串中的 substring() 一样, 截取数组中的元素,不改变原数组

   3. push() 和 pop()

      * push() 向数组末尾添加若干元素
      * pop() 把数组最后一个元素删除

   4. unshift() 和 shift()

      * unshift() 往数组头部添加若干元素
      * shift() 把数组第一个元素删除

   5. sort()

      对数组排序

   6. reverse()

      把整个数组反转

   7. splice()

      >```javascript
      >var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
      >// 从索引2开始删除3个元素,然后再添加两个元素:
      >arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
      >arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
      >// 只删除,不添加:
      >arr.splice(2, 2); // ['Google', 'Facebook']
      >arr; // ['Microsoft', 'Apple', 'Oracle']
      >// 只添加,不删除:
      >arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
      >arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
      >```

   8. concat()

      把当前数组和另一个数组连接起来,并且不修改当前数组,而是返回一个新的数组

      >var arr = [1, 2, 3];
      >
      >var added = arr.concat([5,6,7]);

   9. join()

      把当前数组中的每个元素都用指定的方法串联起来,返回连接后的字符串

      >var arr = ['A', 'B', 'C', 1, 2, 3];
      >
      >arr.join('-');

9. 对象

   键值对

   1. Map

      创建 Map : `var m = new Map();` 和对象一样的键值对结构,实现快速查询,可以创建空 Map ,Map 里传入一个二维数组来创建 Map 键值

      创建空的 Map 后,通过 set() 添加: ` m.set('bob', 23);`  `m.has(key);` 查询键; `m.get(key);` 获取 key 的值; `m.delete(key);` 删除 key;

   2. Set

      创建 Set : `var s = new Set();`  Set 是不含 value 的 key 集合,

      s.add(key)

      s.delete(key)

   Map 和 Set 都是 ES6 提出, 是能 iterable 类型,可以通过 for ... of 循环遍历

   >for (var i of m) {
   >
   >​	console.log(i);
   >
   >}

   iterable 内置方法 forEach ,它接受一个函数,每次迭代就自动回调该函数

   >var a = new Array();
   >
   >a.forEach(function(element, index, array){
   >
   >​	console.log(element+index)
   >
   >})
   >
   >// element 指向当前元素的值
   >
   >// index 指向当前索引
   >
   >// array 指向 Array 对象本身
   >
   >

   >var s = new Set();
   >
   >s.forEach(function(element sameElement, set){
   >
   >// Set
   >
   >})
   >
   >// Map
   >
   >var m = new Map();
   >
   >m.forEach(function(value, key, map){
   >
   >})

10. 函数

    1. 获取函数所有传入的参数

    ​	arguments 关键字, 只能在函数内使用, 获取所有调用者传入的参数; 类似于一个数组

    2. rest 获取传入的额外参数

    > function foo(a, b, ...rest) {
    >
    > }

    3. 变量作用域

       * **局部作用域**和**全局作用域**

         唯一全局作用域 window, 创建的全局变量会绑定到 window 上, 成为 window 的属性,可以通过 window.var ; 这会造成不同文档相同全局变量相冲突,且难以发现, 减少冲突的办法可以创建一个唯一全局变量,将自己的所有变量和函数全部绑定到这个全局变量中;

         >// 唯一全局变量
         >
         >var MYAPP = [];
         >
         >// 其他变量
         >
         >MYAPP.name = 'myapp';
         >
         >MYAPP.varsion = 1.0;
         >
         >// 其他函数
         >
         >MYAPP.foo = function () {
         >
         >​	return 'foo';
         >
         >};

         let 和 const 和 var 一样定义变量

         let 可以申明一个**块级作用域**

         const 可以申明一个常量,也是具有块级作用域

         let 和 const 关键字都是 ES6 引入

       * 变量提升和函数提升

         js 函数定义时,会先扫描整个函数,并把所有变量提升到当前函数顶部(**当前作用域**), 但是只提升变量的申明, 不会提升变量的赋值, 所以定义函数首先将变量定义.

         

       * 解构赋值

         ES6 引入, 能直接对多个变量赋值, 如果对应的属性不存在,则被赋值为 undefined ;可以通过赋值默认值的方式避免不存在的属性返回 undedined

         >// 数组
         >
         >var [x, y, z] = ['a', 'b', 'b'];
         >
         >// 多维 层次一样
         >
         >var [x, [y, z]] = ['a',['b', 'c']];
         >
         >// 忽略某些元素
         >
         >var [, , z] = ['a', 'b', 'c'];
         >
         >// 对象 key 赋值
         >
         >var {x, y, z} = {'a':1, 'b': 2, 'c':3};
         >
         >// 对象的嵌套和多维数组一样, 保持层次一样
       
    4. 构造函数

       

11. 方法

    给对象中绑定函数,称这个对象的方法

    >// 对象中绑定方法
    >
    >var xiaoming = {
    >
    >​	name = '小明',
    >
    >​	birth: 1995,
    >
    >​	age: function () {
    >
    >​		var y = new Date().getFullYear();
    >
    >​		return y - this.birth;  // this 关键字始终指向当前对象(xiaoming 变量), 所以可以拿到
    >
    >​											// 小明的属性, this.birth 等于 xiaoming.birth ;
    >
    >​	}
    >
    >};
    >
    >// this 指向问题: 对象中的函数定义在对象外面时, this 指向会出现两种情况, 

    1. apply() 和 call()

       apply 可以规定 this 指向, apply() 接受两个参数, 第一个是 this 要绑定的变量,第二个是函数本身的参数,是一个数组

       call() 和 apply() 作用相同,区别在于 apply() 把函数参数以**数组** 传入, call() 把参数依次按顺序传入

12. 高阶函数

    函数调用函数

    1. map() 方法

       variable.map(pow);  pow 为函数本身

    2. reduce()

    3. filter()

       arr.filter(func); 传入一个函数, 并依次作用在每个元素上, 根据返回值是 true or false 来判断是否保留元素

    4. sort() 

       sort() 排序是按 ASCII 码大小进行排序

       可以传入自定义排序条件

    5. every()

    6. find()

       查找符合条件的第一个元素, 没有返回 undefined

    7. findIndex()

       和 find() 差不多,如果没找到返回 -1

    8. forEach()

13. 闭包

    函数作为函数的返回值返回

14. 箭头函数

    * 单参数

    > x => x * x;

    * 多参数

    > (x, y) => x * x + y * y

    * 可变参数

    > (x, y, ...rest) => {}

## DOM



1. DOM 操作

   * document.getElementsById()
   * document.getElementsByTagName()
   * document.getElementsByClassName()
   * document.querySelector() 返回指定选择器的一个元素; 类 .类名 ; id #id;
   * document.query Selector All() 

2. 事件三要素

   事件包含 **事件源,事件类型,事件处理程序**

3. 修改元素内容

   ​	innerText 和 innerHTML 都能读取和修改元素内容, innerText 会忽略元素标签,空格和换行

   * innerHTML
   * innerText

4. 修改元素样式

   js 修改的样式是行内样式,权重高

   * element.style
   * element.className
   
5. 获取属性的值

   * Element.属性
   * Element.getAttribute() 获取自定义属性
   * Element.getset  获取元素的所有自定义属性集合,date 开头

6. 修改属性值

   * Element.setAttribute('属性', '值')
   * Element.属性 = 值
   * 
   * Element.removeAttribute(属性)

7. 节点操作

   * parentNode
   * childNodes 会获取所有的子元素节点和子文本节点, 通过 childNode.nodeType 判断节点类型
   * children 只获取子元素节点\
   * firstElementChild
   * nextElementSibling  兄弟节点
   * previousElementSibling
   * createElement(element) 创建节点
   * appendChild(element)  插入到元素后面
   * insertBefore() 插入到元素前面
   * node.removeChild(child) 删除元素
   * node.cloneNode() 克隆 ;括号为空或者为 false, 只拷贝元素标签, true,克隆内容和子节点
   * document.write() 创建元素, 如果页面文档流加载完毕,在调用会导致页面重绘

   兼容问题分装兼容函数

   > function nextElementSibling(element) {
   >
   > ​	var el = element;
   >
   > ​	while (el = el.nextSibling) {
   >
   > ​		if (el.nodeType === 1) {
   >
   > ​			return el;
   >
   > ​		}
   >
   > ​	}
   >
   > ​	return null;
   >
   > }

8. 注册事件

   element.addEventListener(type, listener[, usecaptrue])

   type : 事件类型, 字符型, 不用加 on 如 click(点击); focus(焦点)

   listener: 函数

   事件监听 addEventListener 可以对一个元素添加多个相同事件类型

   element.removeEventListener(type, listener) 移除注册事件

9. DOM 事件流

   三阶段: **事件捕获阶段, 目标阶段,冒泡阶段** 

10. 事件对象

    element.onclick = function(event){}

11. 阻止事件

    element.addEventListener   注册可以用 event.preventDefault() 方法

    element.onclick 事件注册方式可以 三种方法 event.preventDefault()/return false / e.returnValue

12. 阻止冒泡

    e.stopPropagation() 正常

    e.cancelBubble = true;  低版本 ie 浏览器

13. 事件委托

    不再给每个节点设置单独事件监听,将事件监听器放在父节点上,利用冒泡原理影响到每个子节点上
    
14. 键盘事件

    onkeyup / onkeydown / onkeypress 

    * onkeypress  按键按下时执行, 不支持功能键



## BOM

浏览器对象模型(browser object model)

1. BOM构成

   window 对象是浏览器的顶级对象

   load / DOMContentLoaded

   load : 要等网页内容全部加载完毕才执行

   DOMContentLoaded : 只要 DOM 加载完就执行, 不用等所有内容,加载更快

2. 定时器

   setTimeout(callback, time) 方法 : time 单位是毫秒

   clearTimeout() 停止定时器

   setInterval(callback, time)  循环调用,间隔 time 时间

   clearInterval()

   

15. js 执行队列

    同步和异步

16. location 对象

    * location.href : 返回整个 URL
    * location,host : 返回域名
    * location.prot : 返回端口
    * location.pathname : 返回路径
    * location.search : 返回参数
    * location.hash : 返回片段 #后面类容,

17. navigator



18. 元素偏移量 offset

    offset 可以等到任意样式表中的样式值,获取的值没有单位, offset 是只读属性,不能赋值, 和 style 比, style 可以给元素写入样式, 但是 style 只能获取行内样式 

    offsetTop 

    offsetLeft

    offsetWidth

    offsetParent



## TIPS

1.  == 和 ===

   ```
   一般使用双等来判断（==），如果还需要类型相同那么就用三等（===）。
   说一下这两个的区别：
   == equality 等同，=== identity 恒等。
   ==， 两边值类型不同的时候，要先进行类型转换，再比较。 
   ===，不做类型转换，类型不同的一定不等。 
   下面分别说明： 
   先说 ===，这个比较简单。下面的规则用来判断两个值是否===相等： 
   1、如果类型不同，就[不相等] 
   2、如果两个都是数值，并且是同一个值，那么[相等]。
   3、如果两个都是字符串，每个位置的字符都一样，那么[相等]；否则[不相等]。 
   4、如果两个值都是true，或者都是false，那么[相等]。 
   5、如果两个值都引用同一个对象或函数，那么[相等]；否则[不相等]。 
   6、如果两个值都是null，或者都是undefined，那么[相等]。 
   再说 ==，根据以下规则： 
   1、如果两个值类型相同，进行 === 比较。 
   2、如果两个值类型不同，他们可能相等。根据下面规则进行类型转换再比较： 
   a、如果一个是null、一个是undefined，那么[相等]。 
   b、如果一个是字符串，一个是数值，把字符串转换成数值再进行比较。 
   c、如果任一值是 true，把它转换成 1 再比较；如果任一值是 false，把它转换成 0 再比较。 
   d、任何其他组合，都[不相等]。
   ```
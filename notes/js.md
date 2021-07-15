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
    
15. 正则

    2 种创建方式

    > var re1 = /\d+/;
    >
    > var re2 = new RegExp('\\d+');
    >
    > re1.test();   // test(str) 方法测试字符串是否匹配

    匹配规则

    * \* 任意个字符
    * \+ 至少一个字符
    * ? 0 个或者 1 个字符
    * $
    * ^
    * \s
    * \w
    * \d
    * () 分组, exec(str) 方法可以返回一个包含所有分组的数组, 没有返回 null
    * [] 中括号表示范围,
    * {n} n 个字符
    * {n, m} n-m 个字符 

    字符串包含多种分割符号时,用正则去匹配分割符更灵活

    >// 切分多空格字符串
    >
    >'a d 3   e'.split(/\s+/); //['a', 'd', '3', 'e']
    >
    >// 切分多符号
    >
    >'a d, 3 e'.split(/[\s\,]+/); //['a', 'd', '3', 'e']
    >
    >'a d, 3 ;;e'.split(/[\s\,\;]+/); //['a', 'd', '3', 'e']

    #### 贪婪匹配

    正则默认贪婪匹配, 尽可能的多匹配字符, 通过 ? 限制,变为非贪婪模式

    > var re = /^(\d+)(0*)$/; 
    >
    > // 第一组至少以一个数字开头的匹配规则会尽可能地匹配数字
    >
    > re.exec('203200'); // ['203200', '203200', '']  
    >
    > var re2 =  /^(\d+?)(0*)$/;
    >
    > // 限制贪婪
    >
    > re.exec('203200'); // ['203200', '2032', '00']  

    #### 特殊标志

    * g : 全局匹配,每次执行 exec() 会更新 lastIndex 属性,根据 lastIndex 属性继续开始匹配,直到没有结果返回 null 为止
    * i : 忽略大小写
    * m : 执行多行匹配

    >var re1 = /\d+/g; 等价于 var re2 = new RegExp('\\\d+', 'g');
    >
    >```javascript
    >var s = 'JavaScript, VBScript, JScript and ECMAScript';
    >var re=/[a-zA-Z]+Script/g;
    >
    >// 使用全局匹配:
    >re.exec(s); // ['JavaScript']
    >re.lastIndex; // 10
    >
    >re.exec(s); // ['VBScript']
    >re.lastIndex; // 20
    >
    >re.exec(s); // ['JScript']
    >re.lastIndex; // 29
    >
    >re.exec(s); // ['ECMAScript']
    >re.lastIndex; // 44
    >
    >re.exec(s); // null，直到结束仍没有匹配到
    >```

#### 面向对象

prototype 是函数的属性,是一个指针指向一个对象

\__proto__ 是一个对象的内置属性,用于 js 中寻找原型链 



#### 创建类和实例

>1. 通过对象类型创建类和实例
>
>// 创建对象
>
>var Student = {
>
>​      name: 'name',
>
>​      age: 19,
>
>​      run: function() {
>
>​        console.log(this.name + 'running....');
>
>​      }
>
>​    };
>
>// Object.create 创建一个基于 Student 的空类
>
>// 用 createStudent(name) 函数来创建以 Student 为原型的实例
>
>​    function createStudent(name) {
>
>​      let s = Object.create(Student);
>
>​      console.log(s.__proto__);
>
>​      s.name = name;
>
>​      return s;
>
>​    }
>
>​    var xiaoming = createStudent('xiaoming');
>
>​    console.log(xiaoming);
>
>2. 构造函数创建实例和类
>
>function Students(name) {
>
>​      this.name = name,
>
>​        this.hello = function() {
>
>​          console.lgo('hello &{name}');
>
>​        }
>
>​    }
>
>​    var ming = new Students(ming);
>
>​    console.log(ming);
>
>3. 将 hello 属性移动到实例的共享原型上,
>
>function Cat(name) {
>
>​      this.name = name;
>
>​    }
>
>Cat.prototype.hello = function() {
>
>​      return 'Hello, ' + this.name + '!';
>
>​    };
>
>4. class 创建类
>
>// ES6 
>
>class Student {
>
>​	constructor(name) {
>
>​		this.name = name;
>
>}
>
>​	hello() {
>
>​		console.log('Hello, '+ this.name);
>
>}
>
>}
>
>var xiaoming = new Student('xiaoming');

#### 原型继承



#### class 继承

class 创建类后,继承也是 class 关键字和 extends

>// extends 申明原型链对象来自 Student
>
>class PrimariStudent extends Student { 
>
>​	constructor(name, grade) {
>
>​		super(name);  // super 调用父类的构造方法
>
>​		this.grade = grade;
>
>}
>
>​	myGrade() {
>
>​		console.log('Hello, ' + this.grade);
>
>}
>
>}
>
> 



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
   * insertBefore(newElement, referenceElement) 插入新元素到 referenceElement 元素前面
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
    
15. AJAX

    异步请求

    >```javascript
    >function success(text) {
    >	var textarea = document.getElementById('response-info');
    >	textarea.value = text;
    >}
    >function fail(code) {
    >	var textarea = document.getElementById('response-info');
    >	textarea.value = text;
    >}
    >var request = new XHMHttpReuqeust();
    >// 当 readState 的值改变时, function 回调函数就会被调用
    >request.onreadstatechange = function() {
    >	if (request.readState === 4) {
    >		//
    >		if (request.status === 200) {
    >			//
    >			return success(request.responseText);
    >		} else {
    >			//
    >			return fail(request.status);
    >		}
    >	} else {
    >		// HTTP 请求还在继续
    >	}
    >}
    >request.open('GET', url);
    >request.send();
    >```

    ##### readyState 状态码

    XMLTttpRequest.readyState 属性返回一个 XMLHttpRequest 代理当前所处状态

    * 0 : 代理被创建, 但尚未调用 open() 方法
    * 1 : open() 方法已经被调用
    * 2 : send() 方法一被调用, 并且头部和状态yijinghuode
    * 3 : 下载中, responseText 属性以获得部分数据
    * 4 : 下载完成

    ##### 跨域请求

    浏览器因为同源请求的限制, 默认情况下只有同源才能请求, 要实现跨域请求

    1. 通过 Flash 插件发送 HTTP 请求

    2. 通过在同源域名下架设一个代理服务器来转发, javaScript 负责把请求发送到代理服务器, 代理服务器再把结果返回

    3. JSONP 请求, 只能用于 GET 请求,并且要求返回 JavaScript, 这种跨域实际利用的是浏览器允许跨域引用 JavaScript 资源

       > ```html
       > <body>
       >     <p id="info">Price : </p>
       >     <button type="button" class="btn" onclick="getPrice()">shuaxin</button>
       > 
       >     <script>
       >         // 动态创建一个在 head 中的 script,并将 src 设置为目标 url
       >         // 利用浏览器引用外域 JavaScript 资源,实现跨域请求资源
       >         function getPrice() {
       >             let head = document.getElementsByTagName('head')[0];
       >             let js = document.createElement('script');
       >             js.src = 'http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice';
       >             head.appendChild(js);
       >         }
       > 		// 回调函数处理返回的数据
       >         function refreshPrice(data) {
       >             console.log(typeof data, data);
       >             let p = document.getElementById('info');
       >             p.innerText = '当前价格: ' + data['0000001'].name + ':' + data['0000001'].price;
       >         }
       >     </script>
       > </body>
       > ```

    4. CORS

       HTML5 新跨域方法, 是 HTML5 规范定义的如何跨域访问资源

       跨域资源共享(CORS) 是一种基于 HTTP 头的机制, 允许服务器除了它自己以外的其他 origin(域,协议,端口) 访问

16. Promise



17. Canvas

    通过 JavaScript 绘制动画;游戏画面;数据可视化;图片编辑;实时视频处理

    在 canvas 标签内定义宽高, 如果在标签里面添加其他内容, 不支持 canvas 的浏览器会忽略掉 canvas 并渲染里面的内容, 如果浏览器支持 canvas 那么浏览器会忽视 canvas 里面的内容

    >```html
    ><canvas id="demo" width="150px" height="150px">
    >	<p>
    >        你的浏览器不支持
    >    </p>
    ></canvas>
    ><script>
    >    function draw() {
    >        // 获取 canvas 元素
    >        const canvas = document.getElementById('demo');
    >        // 获得渲染上下文和绘画功能, 如果浏览器不支持, 则不能创建成功
    >        // 
    >        if (canvas.getContext) {
    >            const ctx = canvas.getContext('2d');     
    >        } else {
    >            alert('浏览器不支持 canvas');
    >        }
    >    }
    ></script>
    >```

    ##### 绘制矩形

    >```javascript
    ><script>
    >    function draw() {
    >        // 获取 canvas 元素
    >        const canvas = document.getElementById('demo');
    >        // 获得渲染上下文和绘画功能, 如果浏览器不支持, 则不能创建成功
    >        // 
    >        if (canvas.getContext) {
    >            const ctx = canvas.getContext('2d');
    >            // 填充的颜色
    >            ctx.fillStyle = 'yellow';
    >            // fillRect(x, y, width, height)
    >            // 绘制一个距 x 轴 25px,距 y 轴 25px 的矩形,其宽高 100px
    >            ctx.fillRect(25, 25, 100, 100);
    >            // clearRect(x, y, width, height)
    >            // 清除指定矩形区域,始其变透明
    >            ctx.clearRect(45, 45, 60, 60);
    >            // 绘制一个矩形边框
    >            ctx.skrokeRect(50, 50, 50, 50);
    >        } else {
    >            alert('浏览器不支持 canvas');
    >        }
    >    }
    ></script>
    >```

    ##### 绘制路径

    * beginPath();  新建一条路径
    * moveTo(x, y); 路径起始点,改变 xy 可以更改坐标,让绘制点发生改变
    * lineTo(x, y); 规定 moveTo 起始点后,由 lineTo 绘制线, xy 确定终点坐标
    * stroke(); 用线条来绘制图形轮廓
    * fill(); 填充路径的内容区域生成失心图形, 调用 fill() 后自动闭合,不再需要 closePath()
    * close Path(); 闭合路径,绘制命令重新指向上下文 ctx

    > ```javascript
    > function draw() {
    >     const canvas = document.getElementById('demo');
    >     console.log(canvas);
    >     if (canvas.getContext) {
    >         const ctx = canvas.getContext('2d');
    >         ctx.fillStyle = 'yellow';
    >         ctx.beginPath();
    >         ctx.moveTo(75, 50);
    >         ctx.lineTo(100, 75);
    >         ctx.lineTo(100, 25);
    >         ctx.stroke();
    >         ctx.closePath();
    >         // 调用 fill() 将绘制一个实心三角形
    >         // ctx.fill();
    >     } else {
    >         alert('不支持')
    >     }
    > 
    > }
    > ```

    设置线条属性

    > lineWidth = value; 线宽
    >
    > lineCap = type; 线条末端样式 默认 butt, 还有 round 和 square
    >
    > lineJoin = type; 线条与线条结合处的样式 默认 miter, 还有 round 和 bevel
    >
    > miterLimit = value; 限制两条线相交时交接处最大长度
    >
    > setLineDash(segments); 设置当前虚线样式
    >
    > lineDashOffset = value;  设置虚线样式的起始偏移量

    ##### 圆弧

    `arc(x, y, radius, startAngle, endAngel, anticlockwise)`

    画一个以 (x,y) 为圆心, radius 为半径的圆(圆弧), 从 startAngel 开始, endAngle 结束, 按照 anticlockwise 给定方向(默认为 false:顺时针; true 逆时针)来生成, 

    >**注意：`arc()`函数中表示角的单位是弧度，不是角度。角度与弧度的js表达式:**
    >
    >**弧度=(Math.PI/180)\*角度。**

    示例

    > ```javascript
    > function draw() {
    >     const canvas = document.getElementById('demo');
    >     if (canvas.getContext) {
    >         const ctx = canvas.getContext('2d');
    >         ctx.fillStyle = 'yellow';
    >         for (var i = 0; i < 4; i++) {
    >             for (var j = 0; j < 3; j++) {
    >                 let
    >                 	x = 25 + j * 50,
    >                 	y = 25 + i * 50,
    >                 	radius = 20,
    >                     startAngle = 0,
    >                     endAngle = Math.PI + (Math.PI * j) / 2,
    >                 	anticlockwise = i % 2 == 0 ? false : true;
    >                 ctx.arc(x, y, radius, startAngle, endAngle, anticlockwise);
    >                 if (i > 1) {
    >                     ctx.stroke();
    >                 } else {
    >                     ctx.fill();
    >                 }
    >             }
    >             
    >         }
    >     }
    > }
    > ```

    ##### 二次贝塞尔曲线和三次贝塞尔曲线

    * quadraticCurveTo(cp1x, cp2y, x, y); 绘制二次贝塞尔曲线, cp1x,cp1y 为一个控制点, x y 为结束点
    * bezierCurveTo(cp1x, xp1y, cp2x, xp2y, x, y); 绘制三次贝塞尔曲线, cp1x,xp1y, 为控制点一, cp2x,cp2y,为控制点二, x y 为结束点

    >```javascript
    >function draw4() {
    >    var canvas = document.getElementById('demo');
    >    if (canvas.getContext) {
    >        let ctx = canvas.getContext('2d');
    >        // 二次贝塞尔曲线
    >        ctx.beginPath();
    >        ctx.moveTo(75, 25); // 起始点
    >        ctx.quadraticCurveTo(25, 25, 25, 62.5);
    >        ctx.quadraticCurveTo(25, 100, 50, 100);
    >        ctx.quadraticCurveTo(50, 120, 30, 125);
    >        ctx.quadraticCurveTo(60, 120, 65, 100);
    >        ctx.quadraticCurveTo(125, 100, 125, 62.5);
    >        ctx.quadraticCurveTo(125, 25, 75, 25);
    >        ctx.stroke();
    >    }
    >}
    >
    >function draw5() {
    >    var canvas = document.getElementById('demo');
    >    if (canvas.getContext) {
    >        var ctx = canvas.getContext('2d');
    >        ctx.fillStyle = 'red';
    >        //三次贝塞尔曲线画一个心形
    >        ctx.beginPath();
    >        ctx.moveTo(75, 40);
    >        ctx.bezierCurveTo(75, 37, 70, 25, 50, 25);
    >        ctx.bezierCurveTo(20, 25, 20, 62.5, 20, 62.5);
    >        ctx.bezierCurveTo(20, 80, 40, 102, 75, 120);
    >        ctx.bezierCurveTo(110, 102, 130, 80, 130, 62.5);
    >        ctx.bezierCurveTo(130, 62.5, 130, 25, 100, 25);
    >        ctx.bezierCurveTo(85, 25, 75, 37, 75, 40);
    >        ctx.fill();
    >    }
    >}
    >```

    ##### Path2D 对象

    >new Path2D(); // 创建一个空的 Path 对象
    >
    >new Path2D(path); // 克隆 Path 对象

    利用 Path2D 创建的对象去调用绘画命令, 绘制的图画会被缓存和记录, 通过 fill(path) 或 stroke(path) 调用后,才会显示在 canvas 幕布上

    ##### 色彩

    >fillStyle = color; 图形填充颜色
    >
    >strokeStyle = color;  图形轮廓颜色
    >
    >globalAlpha = transparencyValue; canvas 里所有图形透明度, 数值 1~0 
    >
    >fillStyle = 'rgba()'

    ##### 渐变 gradients

    >creatLinnearGradient(x1, y1, x2, y2);

    渐变起点 (x1,y1),终点(x2,y2)

    >createRadialGradient(x1,y1,r1,x2,y2,r2);

    (x1,y1) 为原点, 半径 r1 的圆, (x2,y2) 为原点, 半径 r2 的圆

    > addColorStop(position, color);

    position 为 0~1之间(相当于大小的百分比位置)

    示例

    > ```javascript
    > function draw6() {
    >     const ctx = document.getElementById('demo').getContext('2d');
    >     // 创建 creatLinnearGradient 渐变
    >     const lingrad = ctx.createLinearGradient(0, 0, 0, 150);
    >     lingrad.addColorStop(0, '#00ABEB');
    >     lingrad.addColorStop(0.5, '#fff');
    >     lingrad.addColorStop(0.5, '#26C000');
    >     lingrad.addColorStop(1, '#fff');
    > 
    >     const lingrad2 = ctx.createLinearGradient(0, 50, 0, 95);
    >     lingrad2.addColorStop(0.5, '#000');
    >     lingrad2.addColorStop(1, 'rgba(0,0,0,0)');
    > 
    >     // 将渐变赋值给填充和边框
    >     ctx.fillStyle = lingrad;
    >     ctx.strokeStyle = lingrad2;
    >     // 创建边框和填充位置和大小
    >     ctx.fillRect(10, 10, 130, 130);
    >     ctx.strokeRect(50, 50, 50, 50);
    > }
    > ```

    ##### 图案样式 Patterns

    > createPattern(image, type)

    type : repeat, rpeat-x, repeat-y, no-repeat

    用 onload 事件判断图片是否加载完成, 加载完成后再 createPattern

    ##### 阴影 Shadows

    > shadowOffsetX = float;
    >
    > shadowOffsetY = float;
    >
    > shadowBlur = float;
    >
    > shadowColor = color;

    ##### 绘制文本

    > fillText(text, x, y [, maxWidth]);

    在指定的(x,y) 后填充指定文本

    > strokeText(text, x, y [, maxWidth]);

    在指定(x,y) 位置绘制文本边框

    样式

    > font = value;

    绘制文本样式, 包括字体大小和字体类型

    > textAlign = value;

    文本对齐方式, 默认 start, 还有 end, left, right 和 center

    > textBaseline = value;

    基线对齐选项, 默认 alphabetic, 还有 top, hanging, middle, ideographic, bottom

    > direction = value;

    文本方向,默认 inherit, 还有 ltr, rtl

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

5. navigator

   获取浏览器信息

   * navigator.appName; 浏览器名称
   * navigator.appVersion; 浏览器版本
   * navigator.language; 浏览器设置的语言
   * navigator.platform; 操作系统类型
   * navigator.userAgent; 浏览器设定的 User-Agent 字符串



18. 元素偏移量 offset

    offset 可以等到任意样式表中的样式值,获取的值没有单位, offset 是只读属性,不能赋值, 和 style 比, style 可以给元素写入样式, 但是 style 只能获取行内样式 

    offsetTop 

    offsetLeft

    offsetWidth : 返回的数值包含边框 padding

    offsetParent

19. client



20. screen

    screen 对象表示屏幕的信息

    * screen.width; 屏幕宽度
    * screen.height; 屏幕高度
    * screen.colorDepth; 屏幕颜色位数



21. mouseenter 和 mouseover

    都是鼠标事件,mouseover 鼠标经过自身盒子会触发,经过子盒子也会触发, mouseenter 经过子盒子时不会触发, 因为mouseenter 不会冒泡 

## TIPS

1.  == 和 ===

   ```text
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


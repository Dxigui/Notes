## EMCAScript

### let 和 const

let 声明的变量只能 let 命令所在的代码块内有效. const 声明一个只读的常量,一旦声明就不能更改.

### let

let 除了代码块中有效外, let 不能进行重复声明, 而 var 可以对同一变量重复声明

let 不能和 var 一样变量提升

### const

const 声明时必须要初始化, 否则出现 SyntaxError 语法错误

const 声明复杂数据类型时(object, function, array), 只能保证标量指向的内存地址中的实际指向数据的指针不变, 而指针指向的数据结构无法控制

### 解构赋值

#### 数组解构

解构模式有匹配结果,且结果为 undedined 时,会触发默认返回结果

> // 右边所有值都为空 undedined ,左边全是为默认值
>
> let [a = 1, [b = a]] = [, []];  // a = 1; b = 1;
>
> // 第二变量为空 , 默认值
>
> let [a = 1, [b = a]] = [2, []]; // a = 2; b = 1;
>
> let [a = 1, [b = a]] = [2, [3]]; // a = 2; b = 3;

剩余运算符

> let [a, ...b] = [1, 2, 3]; // a = 1; b = [2, 3];

#### 对象解构

基本和数组差不多

### Symbol

新增原始数据类型, 和 Number; String; Bolean; Object; Array ;null; undefined 一样

#### 创建

Symbol 创建时不能用 new 关键字, 接受一个字符串参数, 主要作用是为新创建的 Symbol 提供描述

> let sy = Symbol('test');
>
> console.log(sy); // Symbol(test);

相同描述字符串参数返回的值也不相等,

> let sy1 = Symbol('test');
>
> sy === sy1; // false

Symbol 数据类型通常作为对象的属性名,当作为属性名时,取其 value 时不能用 `.` 点运算符, 要用 `[]` 中括号,且该属性为共有属性. 同时也不会被 `for...in 和 for...of` 循环取到,即不会出现在循环中, 也不会被 `Object.keys() ; Object.getOwnPropertyNames()`返回,如果要读一个 Symbol 属性, 可以通过 `Object.getOwnPropertySymbols() ; Reflect.ownKeys()` 取到

> let obj = {};
>
> obj.a = 1;
>
> obj[sy] = 2;
>
> console.log(obj); // {a:1,Symbol(test):2}
>
> // for 循环, 只能取到 a
>
> for (let i in obj) {
>
> ​	console.log(i); // a
>
> }
>
> //
>
> Object.getOwnPropertySymbols(obj);  // [Symbol(test):2]    typeof 为 object
>
> Reflect.ownKeys(obj);  // ["a", Symbol(test)]

#### Symbol.for() 和 Symbol.keyFor()

//

### Map 和 Set

#### Map

1. Map 和 Object 的区别

   * Object 的键只能字符串或 Symbol, Map 的键可以为任意值
   * Map 中的键值是有序的(FIFO), Object 的键无序
   * Map 可以用 size 属性看键值数量
   * Object 键名可能和本身的原型或原型链上的键名冲突

2. for of 迭代

3. forEach(callback(v,k)) 迭代

4. map 与 array 转换

   > var kvArray = [["key1", "value1"], ["key2", "value2"]];
   >
   >  // Map 构造函数可以将一个 二维 键值对数组转换成一个 Map 对象
   >
   >  var myMap = new Map(kvArray);
   >
   > // 使用 Array.from 函数可以将一个 Map 对象转换成一个二维键值对数组 
   >
   > var outArray = Array.from(myMap);

5. 克隆与合并

   > // 克隆
   >
   > let map1 = new Map(map);
   >
   > // 合并
   >
   > let map1 = new Map();
   >
   > let  map2 = new Map();
   >
   > let map3 = new Map(...map1, ...map2);

#### Set

特殊值

* +0 与 -0 恒等; +0 === -0;
* undefined 与 undefined 恒等
* NaN 与 NaN 不恒等

数组和 Set 转换

> let s = new Set();
>
> let arr = [...s];

数组去重

> let s = new Set(new Array());
>
> [...s];

### 字符串



### 对象

#### 拓展运算 `...`

`...` 拓展运算可以取出对象所有可遍历属性并拷贝到新对象

#### 方法

1. Object.is();  
2. Object.assign();
3. Object.setPrototypeOf
4. Object.getPrototypeOf



### 数组

### 新的数组创建

1. Array.of(args);



2. Array.from(arraryLike[, mapFn[, thisArg]]);

   将类数组对象或可迭代对象转换为数组

   参数: 

   * arraryLike : 数组或类数组

   * mapFn : 可选参数, map 函数处理 arraryLike 每个元素后创建数组

   * thisArg : 可选,用于指定 map 函数执行时的 this 对象

     > // 定义 map 函数
     >
     > let myMap = {
     >
     > ​	do : function(n) {
     >
     > ​		return n * 2;
     >
     > }
     >
     > }
     >
     > // Array.from()
     >
     > Array.from([1,2,3], function(n) {return this.do(n);}, myMap);

   还可转换 Map Set 对象以及字符串

#### 扩展方法

1. find(function);

   根据 function 函数提供的规则查找数组中的值,找到返回, 没有返回 undefined, 多个符合条件的值则返回第一个

2. findIndex(function)

   返回符合条件的索引

3. fill(value, starindex, endindex)

   根据索引开始填充值, 会替代原值, endindex 默认末尾索引

   > [1,2,3].fill(2,0);  //[2,2,2]

4. entries()

5. arr.flat() 

   多维数组转一维数组

6. arr.flatMap(function)

### 函数

#### 函数参数

1. 默认参数
2. 不定参数   `...arg`

#### 箭头函数

箭头函数没有 `this arguments super new.target` 绑定, 

tips:

对象中定义函数方法时,函数中包含 this, 箭头头函数中 this 会被绑定到全局变量 window 上,以及监听某事件时,监听函数有 this 时,都不推荐用箭头函数



### 迭代器



> ```js
> const person = {
>     color: 'yellow',
>     name: [
>         'xiaoming',
>         'xiaohong',
>         'xiaotong'
>     ],
>     // 给对象添加迭代器
>     [Symbol.iterator]() {
>         let index = 0;
>         // Symbol.iterator 必须返回一个对象
>         return {
>             // 给迭代器添加 next() 方法, next 方法返回的是一个对象
>             // 箭头函数让 this 指向 person
>             // 如果不用箭头函数,则在函数外面添加 let _this = this, 函数里面 this 修改成 _this
>             next: () => {
>                 if (index < this.name.length) {
> 
>                     let result = {
>                         value: this.name[index],
>                         done: false
>                     };
>                     index++;
>                     return result;
>                 } else {
>                     return {
>                         value: undefined,
>                         done: true
>                     };
>                 }
> 
>             }
>         };
>     }
> }
> for (let v of person) {
>     console.log(v);
> }
> ```

#### 生成器

异步任务

> // 创建
>
> function * gen(){
>
> ​	yield '生成器'
>
> }
>
> // 调用 next() 方法 和 for of
>
> let iter = gen();
>
> iter.next();
>
> 

### Promise

Promise 对象的几种状态

* pending: 初始状态,即正在执行, 不处于 fulfilled 或 rejected
* fulfilled : 成功的完成了操作
* rejected : 失败
* settled : Promise 处于 fulfilled 或者 rejected 二者中的任意状态

### 模块化

ES6 之前模块化规范: CommonJS / AMD / CMD

ES6 数据导出 export

ES6 数据导入 import * as m from filepath;


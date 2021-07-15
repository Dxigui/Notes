## JavaScript 面向对象编程

#### 封装

1. 构造函数

   构造函数是一个内部使用 this 的普通函数, 对构造函数使用 new 就能生成实例, 并且 this 会绑定到实例对象

   >```javascript
   >// 创建一个构造函数
   >
   >function Student(name, height) {
   >      this.name = name;
   >      this.height = height;
   >	  this.class = 1;
   >   	  this.run = function() {
   >	       console.log('running');
   >
   >	  };
   >    }
   >
   >// new 创建一个实例, 并将构造函数的 this 指向实例
   >var xiaoming = new Student('小明', 172);
   >console.log(xiaoming.name, xiaoming.height); // '小明', 172
   >```

   

   由 `xiaoming.__proto__`   可以找到其原型对象, `__proto__` 是对象寻找原型对象的非标准方法

   而函数的 `prototype` 也是指向其原型对象的内置属性

   >```javascript
   >// 构造函数和 new 创建的实例指向同一个原想对象
   >
   >typeof xiaoming; // "object"
   >typeof Student; // "function"
   >xiaoming.__proto__  === Student.prototype; // true
   >```

   判断实例对象是否属于某原型对象

   > ```javascript
   > xiaoming instanceof Student; // true
   > ```

   原型对象有一个 `constructor` 内置属性, 指向其构造函数, 那么实例也可以拿到原型对象的 constructor 属性

   > ```javascript
   > xiaoming.constructor === Student; // true
   > Student.prototype.constructor === Student; // true
   > 
   > // 关于 constructor 属性
   > // construct 属于原型对象(Student.prototype)独有属性
   > Student.prototype.hasOwnProperty('constructor'); // true
   > xiaoming.hasOwnProperty('constructor'); // false
   > // Student 函数由 Function 构造
   > Student.constructor; // f Function()
   > // Student 本身没有 constructor 属性,而是通过原型链向上寻找或着继承获得
   > Student.hasOwnProperty('constructor'); // false
   > // Student 的原型对象是 Function.prototype
   > Student.__proto__ === Function.prototype; // true
   > // Function.prototype 有 constructor 属性,所以 Student 可以使用
   > Function.prototype.hasOwnProterty('constructor'); // true
   > ```

2. prototype 模式

   用普通构造函数封装时, 其固有属性或方法在多个实例对象中不共享, 每次创建一个实例都会重新开辟空间, 导致资源浪费

   >```javascript
   >// 给 Student 构造函数添加一个班级和 run 方法
   >xiaohong = new Student('小红', 158);
   >xiaohong.run == xiaoming.run; // false
   >```
   
   通过构造函数的 `prototype` 属性, 指向一个原型对象, 这个对象中的属性和方法都会被构造函数的实例继承, 把不变的属性和方法定义到 `prototype` 对象上, 优化运行效率
   
   >```javascript
   >// 将 Student 中的 run 方法定义到 prototype 对象中
   >Student.prototype.run = function() {
   >   console.log('running');
   >}
   >
   >xiaoming.run === xiaohong.run; // true
   >```
   
   prototype 验证方法
   
   * isPrototypeOf()
   
     判断原型对象和实例之间的关系
   
     >```javascript
     >Student.prototyepe.isPrototypeOf(xiaoming); // true
     >```
   
   * hasOwnProperty()
   
     判断属性属于本身还是继承
   
     >```javascript
     >xiaoming.hasOwnProperty("name");
     >```
   
   * in
   
     判断实例是否有某属性
   
     >```javascript
     >"name" in xiaoming; // true
     >```

#### 继承

对象之间继承就是将子对象的原型指向父对象的原型, 那么父对象原型上的属性和方法就能被子对象继承

1. 构造函数绑定

   通过 call() 和 apply() 方法,将父对象的构造函数绑定在子对象上

   > ```js
   > // 父对象构造函数
   > function Person() {
   > }
   > Person.prototype.color = 'yellow';
   > 
   > function Student(name, height) {
   >     // 通过 apply 将 this 指向到 Student
   >     Person.apply(this, arguments);
   >     this.name = name;
   >     this.height = height;
   > }
   > ```

2. prototype 模式

   修改原型对象的指向,最常见方法

   > ```js
   > function Student(name, height) {
   > 	this.name = name;
   > 	this.height = height;
   > }
   > // 将 Student 的原型对象指向 Person 父对象的实例
   > Student.prototype = new Person;
   > // 修改 Student 原型对象的 constructor
   > // 如果不修改,那么 Student 的原型对象的构造函数将会指向 Person
   > Student.prototype.constructor = Student;
   > 
   > var xiaoming = new Student('小明', 172);
   > 
   > ```

3. 改良 prototype 

   加入一个中间空函数作为中间介, 让中间函数的原型对象指向父对象的原型并不修改 constructor

   子对象和原来 prototype 模式一样指向中间函数 F 的实例

   > ```js
   > // 函数封装
   > function extend(Child, Parent) {
   >     // 创建一个空的中间函数
   >     const F = function() {};
   >     // 中间函数的原型对象指向父对象 Parent 的原型对象
   >     F.prototype = Parent.prototype;
   >     // 子对象的原型对象指向 F 的实例
   >     Child.prototype = new F();
   >     // 修改子对象原型对象的构造函数,让它重新指向 Child 构造函数
   >     Child.prototype.constructor = Child;
   >     // 在子对象打开一条直接到父对象原型的通道
   >     Child.uber = Parent.prototype;
   > }
   > 
   > ```

4. 拷贝继承

   将父对象的所有属性和方法拷贝到子对象

   > ```js
   > function extend(Child, Parent) {
   > 	const p = Parent.prototype;
   > 	const c = Child.prototype;
   > 	for (let i in p) {
   > 		c[i] = p[i];
   > 	}
   > 	c.uber = p;
   > }
   > extend(Student, Peson);
   > 
   > ```

5. 非构造函数的深拷贝继承

   > ```js
   > function deepCopy(c, p) {
   >     let c = c || {};
   >     // in 中 p 为数组返回索引 i 为 p 中值的索引
   >     for (let i in p) {
   >         // 判断 p[i] 是否为数组或对象
   >         if (typeof p[i] === 'object') {
   >             c[i] = (p[i].constructor === Array) ? [] : {};
   >             // 递归调用
   >             return deepCopy(c[i], p[i]);
   >         } else {
   >             c[i] = p[i];
   >         }
   >     }
   >     return c;
   > }
   > ```
   >
   > 

## JavaScript 面向对象编程

#### 封装

1. 构造函数

   构造函数是一个内部使用 this 的普通函数, 对构造函数使用 new 就能生成实例, 并且 this 会绑定到实例对象

   >```javascript
   >// 创建一个构造函数
   >
   >function Student(name, height) {
   >
   >      this.name = name;
   >
   >      this.height = height;
   >
   >	  this.class = 1;
   >
   >     this.run = function() {
   >
   >	       console.log('running');
   >
   >	  };
   >    }
   >
   >// new 创建一个实例, 并将构造函数的 this 指向实例
   >
   >var xiaoming = new Student('小明', 172);
   >
   >console.log(xiaoming.name, xiaoming.height); // '小明', 172
   >```

   

   由 `xiaoming.__proto__`   可以找到其原型对象, `__proto__` 是对象寻找原型的非标准方法

   而函数的 `prototype` 也是指向其原型对象的内置属性

   >```javascript
   >// 构造函数和 new 创建的实例指向同一个原想对象
   >
   >typeof xiaoming; // "object"
   >
   >typeof Student; // "function"
   >
   >xiaoming.__proto__  === Student.prototype; // true
   >```

   判断实例对象是否属于某原型对象

   > ```javascript
   > xiaoming instanceof Student; // true
   > ```

   实例对象和原型对象都有一个 `constructor` 内置属性, 指向其构造函数

   > ```javascript
   > xiaoming.constructor === Student; // true
   > 
   > Student.prototype.constructor === Student; // true
   > ```

2. prototype 模式

   用普通构造函数封装时, 其固有属性或方法在多个实例对象中不共享, 每次创建一个实例都会重新开辟空间, 导致资源浪费

   >```javascript
   >// 给 Student 构造函数添加一个班级和 run 方法
   >
   >xiaohong = new Student('小红', 158);
   >
   >xiaohong.run == xiaoming.run; // false
   >```
   
   通过构造函数的 `prototype` 属性, 指向一个原型对象, 这个对象中的属性和方法都会被构造函数的实例继承, 把不变的属性和方法定义到 `prototype` 对象上, 优化运行效率
   
   >```javascript
   >// 将 Student 中的 run 方法定义到 prototype 对象中
   >
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
   
   * in
   
     判断实例是否有某属性
   
     >```javascript
     >"name" in xiaoming; // true
     >```

#### 继承


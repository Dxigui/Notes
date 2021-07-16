## jQuery

### 选择器

jQuery 选择器返回的是 jQuery 对象,类似数组,没查找到返回空 `[]`;

jQuery 对象和 DOM 对象之间可以相互转化:

> var div = $('#test');
>
> var divDom = div.ger(0);    // 获取第一个 DOM 元素
>
> var another = $(divDom);  // 重新把 DOM 包装为 jQuery 对象

#### ID 查找

> $('#test');

#### tag 查找

> var ps = $('p');
>
> ps.length;

#### class查找

> // 单个 class
>
> var test = $('.test');
>
> // 多个 class, 没有空格
>
> var test = $('.test1.test2')

#### 按属性查找

> var test = $('[name=test]');
>
> // 当属性值有空格或特殊符号,用双引号括起来
>
> var test = $('[name="test a"]');
>
> var test = $('[class="test test2 test-1"]');

#### 组合查找

> // 标签和属性组合
>
> var test = $('input[name=email]');
>
> // tag 和 class
>
> var test = $('div.test');

#### 多项选择器

> // 同时查找多个元素
>
> $('p, div');
>
> $('p.red, div.test');

#### 层级选择器

多层选择通过**空格隔开**

> $('div.test p');
>
> $(div.test ul li.test');

#### 子选择器

必须为父子节点关系, **大于号>** 

> $('div.test>p.test');

#### 过滤器

一般不单独使用,通常附加在定位元素上
> $('ul.test li:first-child');
> $('ul.test li:last-child');
> $('ul.test li:nth-child(2)');
> $('ul.test li:nth-child(even)');  // 序号为偶数的元素
> $('ul.test li:nth-child(odd)');   // 序号为奇数的元素

#### 表单相关
针对表单元素的特殊选择器
* :input :
* :file :
* :checkbox :
* :radio :
* :focus :
* :checked :
* :enabled :
* :disabled :

#### 查找
通过 $ 定位到一个节点后,这个节点为开始节点进行查找
1. 往下 : find()
2. 往上 : parent()
3. 同级节点往左 : prev()
4. 同级节点往右 : next()
	> var div = $('div#test');
	> var p = div.find('.test2');
	> var parentDiv = div.parent('.test3');
	> var prevDiv = div.prev('div.test4');
	> var nextDiv = div.next('div.test5');
#### 过滤


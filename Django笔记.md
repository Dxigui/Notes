# Django 笔记

## Django 中常用命令

### 新建 Django Project

```django
django-admin.py createproject project_name
```

### 新建 app

```django
django-admin.py createapp app_name
```

### 创建数据表，清空数据库

```django
# 创建更改文件
python manage.py makemigrations
# 将生成的py文件应用到数据库
python manage.py migrate
#
python manage.py flush
```

### 使用开发服务器

```django
python manage.py runserver [options]
# options 可选参数，可以定义端口和 IP
```

### 创建超级管理员

```django
# 创建
python manage.py createsuperuser
# 修改
python manage.py changepassword username
```

### 导出数据，导入数据

```django
python manage.py dumpdata appname > appname.json
python manage.py loaddata appname.json
```

### Django 项目环境终端

```django
python manage.py shell
```

### 数据库命令行

```django
python manage.py dbshell
```

## Django 中的视图和网址

视图函数和 URL 处理函数间的设计理念是使用 **松耦合**  原则，尽量降低两者之间的相互影响，或者说消除两者之间的影响，在一边进行修改后而不用再对另外一边进行相应的修改，提升了项目的维护性。

在使用 `django-admin.py startproject projectname` 创建一个项目后，会出现一个项目目录

```python
# Django 版本不同目录可能会有差异
projectname
├── manage.py
└── projectname
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

在项目创建后需要新建新的应用可以用 `python manage.py startapp appname`  命令实现

```python
appname/
├── __init__.py
├── admin.py
├── migrations/
├── models.py
├── tests.py
└── views.py
```

`appname `  文件和 manage.py 文件同属于顶级目录，在这两个创建的文件夹中有 views.py 是试图，urls.py 是 url 处理文件。新定义应用名 `appname`  需要添加到 settings.py 配置文件中的 INSTALL_APPS 中，将新应用添加到 settings.py 后，Django 就可以检索到 app 中的模板文件和静态文件。

定义一个简单的视图 appname/views.py

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

from django.http import HttpResponse
from django.http import HttpResponseRedirect
from django.shortcuts import render
from django.urls import reverse

def index(request):
    return HttpResponse("Hello world!")

# render 方法对模板 index2.html 渲染
# 并返回一个相应对象
def index2(request):
    return render(request, 'index2.html')

# HttpResponseRedirect 重定向
# reverse 接收 URLconf 中的 name 作为第一个参数
# reverse 就能获取到 name 对应的 url
# 减少 URL 更改需要修改的代码
# 在模板中的 url 标签和 reverse 功能差不多
def index3(request):
    return HttpResponseRedirect(
        reverse('index3', [args=(a, b)])
    )

# 视图函数接收多个参数
# 与 URLconf 中的 url 对应
def index4(request, a, b):
    return render(request, 'index4.html')
```

视图函数的参数必须是以 request 为第一个传入，函数返回一个HttpResponse 响应对象，与其对应的 URLconf 为

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

from django.conf.urls import url
from django.contrib import admin
from appname import index as appname_index

# 为 url 设置 name
# 在 name='index4' 中的 url 有三段
# 对应的 index4 视图函数中传入的参数为三个
urlpatterns = [
    url(r'^$', appname_index.index, name='index'),
    url(r'^index2/$', appname_index.index2,                                   name='index2'),
    url(r'^index3$', appname_index.index3,
                      name='index3'),
    url(r'^index4/(\b+)/(\b+)/', appname_index.index4,
                      name='index4'),
    url(r'^admin/$', admin.site.urls),
]
```

视图中的 `render  render_to_response  redirect `  的使用







## Django 中模板系统

Django 使用模板系统来实现 Python 代码和页面设计的分离，Django 模板中包含了页面设计的*语言和变量* 。



### 模板系统简介

首先创建一个 Template 对象，该对象在 django.template 模块中，然后通过 Context 类向 Template 对象中的变量传递数据，Context 同在 django.template 模块下；最后用 render() 函数对 Template 进行渲染。

```python
#!/usr/bin/env python3

# 导入 Tempalte 
```

从上面的示例可以看出，Context 中参数是一个字典，且数据类型是字符串；Template 对象中的变量是由两个大括号包裹，除了简单的变量外，模板中也可有 `if/if...else` `for` `filter` `include ` `extends` 模板标签构成。

```html
<!-- 创建一个含多种类型的变量 -->
<html>
    <head>
        <title>
            <!-- 普通变量 -->
            Welcome to online shopping {{ name }}           </title>
    </head>
        
    <body>
        <p>
            <!-- extends 继承模板 -->
            {% extends 'base.html' %}
        </p>
        <p>
            <!-- for 循环，使用 % 包裹，由 for 循环体                      endfor 三部分组成，endfo 关闭标签-->
            <!-- for 循环中可以设置一个特殊的 forloop 模板                  变量，来表示当前循环的执行次数 1 开始 -->
            You can select {% for cmd_name in n_list %}
            <li>
                {{ forloop.counter }}:{{ cmd_name }}                 </li>
            {% endfor %}
        </p>
        <p>
            <!-- if 语句，if 为Ture执行，False跳过 也要                    enif 结束,可以接受 and/or/not-->
            Search commodity {% if cmdy_name %}
            <span>Find it.</span>
            {% endif %}
        </p>
        <p>
            <!-- filter 过滤器 通过管道符号 | 来调用 -->
            The commodity production date 
            {{ pro_date | date:"F j, Y"}}.
        </p>
        <p>
            <!-- include 用于在模板中导入其他模板 -->
            {% include 'template/index.html%}
        </p>
        
    </body>
</html>
```

模板系统能处理多种数据结构，如 list dictionary 自定义对象（类）

### 传递字典

```python
person = {'name': 'Sally', 'age': '45'}
t_project = Template('{{ person.name }} is {{ person.age                          }} years old.')
c_pass = Context({'person': person})
print(t_project.render(c_pass))
```

### 传递列表，按索引取值

```python
fruit = ['apple', 'banana', 'orange']
t_project = Template('Item 2 is {{ fruit.2 }}')
c_pass = Context({'fruit': fruit})
print(t_project.render(c_pass))
```

### 类的传递

```python
# 模板对象中不能在方法调用中使用括号
# 也不能调用需要传参的方法
class Person(object):
    def __init__(self, f_name, l_name):
        self.f_name, self.l_name = f_name, l_name
t_project = Template('Hello, {{ Person.f_name }} {{                           Person.l_name}}')
c_pass = Context({'Person': Person('John', 'Sam')})
print(c_project.render(c_pass))
```

在上面列表传递中用到了 `.` 字符，在模板对象中，可以通过 `.` 来实现多层调用。

```python
person = {'name': 'Sally', 'age': '19'}
t_project = Template('{{ person.name.upper }} is {{                              person.age }} years old.')
c_pass = Context({'person': person})
print(t_project.render(c_pass))
```

local()

### 过滤器



### 自定义过滤器和标签

1. 在 app 中创建一个 templatetags 文件夹
2. 在此文件夹中创建一个新文件
3. 修改新文件
4. 定义新标签后再模板中引用新标签

```python
# app/templatetags/myTag.py

from django import template
from django.utils.safestring import mark_safe

register = template.Library()

# 自定义过滤器
# 自定义过滤器只能传入一个参数，多用在控制语句中
@register.filter
def filter_multi(x, y):
    return x*y

# 自定义标签
# 定义了一个需传入三个参数并计算三个参数之积的标签
# 不能用在控制语句中
@register.simple_tag
def simple_tags(x, y, z):
    return x*y*z
```

```html
# 模板中导入
{% load myTag %}

# 使用
# 自定义过滤器
{{ age|filter_multi:3 }}

# 自定义标签
{% simple_tags 2 3 4 %}
```

### 模板继承

block 和 extends 



## Model

### 显示 SQL 语句

* 在 settings.py 中配置 LOGGING，显示 SQL 语句

```python
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'handlers': {
        'console': {
            'level': 'DEBUG',
            'class': 'logging.StreamHandler',
        }
    },
    'loggers': {
        'django.db.backends': {
            'handlers': ['console'],
            'level': 'DEBUG',
        },
    }
}
```

* 使用第三发模块

[Django Debug Toolbar](http://django-debug-toolbar.readthedocs.io/en/stable/installation.html)





### 数据库操作



* 单表查询

```python
# 定义一个 Student 表
# 查询所有数据
# 他返回的是一个 QureySet 对象，是一个可迭代对象
# [obj, obj, obj]
stu = Student.objects.all()
# 查询指定的字段 如 id name
# 返回的也是一个 QuerySet 对象
# 不过里面时一个包含字典的 list
# <QerySet [{'id': 1, 'name': 'a'}, {'id': 2, 'name': 'b'}]>
stu = Student.objects.all().values('id', 'name')
# 和上面的查询是一样的，返回的值的数据类型不一样
# 返回一个包含 tuple 的 list
# <QuerySet [(1,'a'), (2, 'b')]>
stu = Student.objects.all().values_list('id', 'name')

# 通过 for 循环遍历出每个对象，再通过 . 或其他方式
# 取出具体的值，根据具体的数据结构
```

* 连表查询 ===> ForeignKey    重点双下划线 __

```python
# 在 Student 表中添加一个外键 s_id，关联班级表 Class
# 通过 __ 双下划线来进行连表查询
# 示例通过双下划线查询 Class 表的 id 和 name
Student.objects.filter(t_id__id=1)
Student.objects.filter（t_id__name='1班'）

# 多级连表查询，当有多个外键时，可以使用多个双下划线
Student.objects.filter(t_id__name__age='18')

# 反向查询
# 通过 Class 表查询 Student 表中的数据
# Class 表中没有 ForeignKey 字段，所以通过
# student_set 来实现反向查 询，注意是小写
# 默认是 小写表名加 _set,也可以通过 related_name
# 自定义查询语句，方法是在定义外键时
# 在后面加上 related_name='自定义名' 参数
obj = Class.objects.objects.filter(name='1班').first()
obj.student_set.all()
```

* 连表查询 ====> ManyToMany      多对多

```python
# 创建一个新的 Teacher 表
# 并在 Class 表加个 m2m 的字段，建立多对多关系
# 多对多关系需要创建第三张表来进行查询
# 不过 Django 中不需要自己创建
# Django 中通过 ManyToMany 来实现第三张表
# 先选取 Class 的 id 或其他字段，
obj = Class.objects.filter(id=1).first()
# 然后通过 m2m 字段对 Theacher 表中与 Class id=1
# 有关系数据进行操作
# 添加  // 给 id=1 Class 添加 id=1 的 Teacher
# 可以一次性添加多条记录
obj.m.add(1)
obj.m.add([2, 3])
# 删除  // 删除 id=1 的 Class 的老师的 id
obj.m.remove(1)
obj.m.remove([2, 3])
# 清空  // 清空 id=1 的 Class 的老师
obj.m.claer()
# 重置  // 重置 id=1 的 Class 的老师
obj.m.set([2, 4, 6])
# 查询 
obj.id    // Class id
obj.name  // Class name
obj.m2m   // 第三张表
obj.m2m.all() // 获得一个包含 Class id=1 的老师的				 // QuerySet 对象
```



* 修改数据库

```python
# 通过 update 对数据库进行修改
Student.objects.filter(id=1).update(name='wangbaba')
```

* 删除数据库记录

```python 
# 通过 delete 对数据库进行删除操作
Student.objects.filter(id=1).delete()
```

### 在 model 增加 Manager 方法 -----进阶

* 增加 Manager 方法来给模块添加表级功能

在我们实际开发中，代码经常会出现重复编写。在 Django 的数据库存取过程中多次出现重复的查询语句，出现代码冗余是一种不好的现象。 我们可以通过在 model 中添加 Manager 方法来减少重复代码

```python
# models.py
# 为 Book 模型定义一个 title_count()方法
# 实现对数据的统计

from django.db import models

class BookManager(models.Manager):
    def title_count(self, keyword):
        return self.filter(title__icontains=keyword).count()
    
class Book(models.Model):
    title = models.CharField(max_length=100)
    authors = models.ManyToManyField(Author)
    publisher = models.ForeignKey(Publisher)
    publication_date = models.DateField()
	num_pages = models.IntegerField(blank=True,
                                   null=True)
    objects = BookManager()
	
    def __str__(self):
        return self.title
    
# 使用
>>> Book.objects.title_count('django')
// 32

```

在上面的代码中定义了 `BookManager` 类，继承 `django.db.model.manager `  ，类中定义了一个方法，实现了对数据的统计；而在 `Book` 模型中添加了一个 objects 属性在是 `BookManager（） `  的实例，如果我们没有创建 `objects`  它也将被自动创建。这样我们就对查询进行了封装，减少重复编码。

在上面的例子中，`BookManager（） `  返回的具体数值，通过 `Manager.get_query_set()` 方法实现 `BookManager()` 返回是一个 QuerySet 对象

```python
# models.py
# 

class DahlBookManager(models.Manager):
    def get_query_set(self):
        return super(DahlBookManager,
                     self).get_query_set().filter(
        author = 'Roald Dahl')
    
class Book(models.Model):
    # ...
    
    objects = models.Manager()
    dahl_objects = DahlBookManager()
    
# 使用
Book.dahl_objects.all()
Book.dahl_objects.filter(title='d')
```

注意：

* 在 Book 模型中，多了一个 Manager 实例 objects ，这样可以避免 dahl_objects 覆盖原生的 objects，导致 Query Set 对象只有 dahl_objects 可用
* get_query_set() 返回的是一个 QuerySet 对象，所以可以使用一切 QuerySet 方法。



### 模型方法

在模型中除了数据表字段外，还可以给模型定义自定义方法，实现在模型中集中业务逻辑

```python
from django.contrib.localflavor.us.models import USStateField
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)
    birth_date = models.DateField()
    address = models.CharField(max_length=100)
    city = models.CharField(max_length=50)
    state = USStateField() # Yes, this is U.S.-centric...

    def baby_boomer_status(self):
        "Returns the person's baby-boomer status."
        import datetime
        if datetime.date(1945, 8, 1) <= self.birth_date <= datetime.date(1964, 12, 31):
            return "Baby boomer"
        if self.birth_date < datetime.date(1945, 8, 1):
            return "Pre-boomer"
        return "Post-boomer"

    def is_midwestern(self):
        "Returns True if this person is from the Midwest."
        return self.state in ('IL', 'WI', 'MI', 'IN', 'OH', 'IA', 'MO')

    def _get_full_name(self):
        "Returns the person's full name."
        return u'%s %s' % (self.first_name, self.last_name)
    full_name = property(_get_full_name)
```









### 注意

* Django1.0 和 Django2.0

```python
# 外键参数
fk = models.ForeignKey(ClassName, on_delete=models.CASCADE)
```





## Admin

admin 数据库的一个后台管理工具

创建超级用户后，在 admin.py 中进行数据库注册

```python
# app/admin.py
from django.contrib import admin
from app import models

admin.site.register(models.Objectname)
```

可以给后台添加更丰富的功能，而且这些功能都是 Django 自带的

```python
# app/admin.py
# 现有一个叫 Book 的 ORM 类，对其添加功能

class BookAdmin(admin.ModelAdmin):
    # 让每个数据显示更多的信息，如 name、id、price、pub_date 等，id 为第一权限，name 为第二权限
    list_display = ('id', 'name', 'price', 'pub_date')
    # 设置可以尽心编辑的内容
    list_editable = ('name', 'price')
    # 在多对多时，实现其搜索，后面的参数必须是多对多模式
    # filter_horizontal = ('author',)
    # 分页，2 表示每页两个记录
    list_per_page = 2
    # 实现搜索，指定搜索范围，
    search_fields = ('id', 'name')
    # 制定条件进行筛选
    list_filter = ('pub_date',)
    # 
    ordering = ('price')
    
# 最后和 Book 一起注册
admin.site.register(Book,Book Admin）
```



## cookie 和 session

cookie 是一组键值对字典，实现登录验证，弥补了 HTTP 无状态。

当客户端发起请求时，服务端会发送个客户端一个唯一的 cookie 值，在下次客户端再次请求时，服务端就会验证 cookie ，如果真确则通过，常用于用户登入。

```python 
# urls.py 配置 url

# app/views.py 创建试图处理函数
def login(request):
    print(COOKIE, request.COOKIES)
    if request.method == 'POST':
        if name = 'name' and pwd = 'pwd':
        	# 给响应添加一个 cookie 值
            # 给 cookie 设置生命周期
        	red_response = redirect('/index/')
        	red_response.set_cookie('key','value',
                                    max_age=60)
        	return red_response
	return render(request, 'blog/login.html')

# 验证 cookie 通过则登录成功
def index(request):
    if request.COOKIES.get('key', None) == 'value':
        return render(request, 'blog/index.html')
    else:
        return redirect('/login/')
```

上面实现了一个简单的 cookie ，但是单一个 cookie 来回收发麻烦，而且有被窃取的危险。

所以出现了 session，session 和 cookie 配合使用。session 也是一个键值对，键是一个字符串，值是一些用户的信息，他也是个键值对，服务器个通过 cookie 给用户发送的是 session 的键，当用户再次请求服务器时，携带这个键一起，然后由服务器进行识别，session 可以存储在缓存和数据库中，为了减轻数据库压力，session 一般生命周期是 15 天，当然也可以自定义时间。

```python
# urls.py 配置 url

# app/views.py 创建试图处理函数
def login(request):
    print(SESSION, request.session)
    if request.method == 'POST':
        if name = 'name' and pwd = 'pwd':
            # 给 session 值添加键值对
	        request.session['user'] = name
            request.session['is_login'] = True
            return redirect('/index/')
	return render(request, 'blog/login.html')

# 验证 session 通过则登录成功
def index(request):
    if request.session.get('is_login', None):
        return render(request, 'blog/index.html')
    else:
        return redirect('/login/')
```



## 遇到的问题

### NO module named ‘MySQLdb‘

解决方法：

在 python3 中不支持 MySQLdb 了，而 pymysql 代替了它，所以下载 pymysql

```python
pip install pymysql
```

在下载完后还需要修改 djagno/db/mysql/base.py 文件，在     from django.utils.safestring import SafeBytest,SafeTest 下面加上  import pymysql

pymysql.install_as_MySQLdb()
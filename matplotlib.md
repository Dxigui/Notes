# matplotlib

`matplotlib` 库主要是将数据可视化,可以导出常见的矢量(vector)和光栅(raster)图: PDF/SVG/JPG/PNG/BMP/GIF 等

## matplotlib API 入门

导入

```python
>>> import matplotlib.pyplot as plt
>>> import numpy as np
>>> import pandas as pd
```

## Figure 和 Subplot

### `plt.figure()`

`matplotlib` 的图像都位于 `Figure` 中

```python
>>> # 创建一个 Figure 对象
>>> fig = plt.figure()
```

`figure` 参数

```python
num : 整数或者字符串,可选,默认: None
     如果没有传入,则创建一个新的 figure ,figure 的 number 将被增加,可以通过 number 属性访问
     如果提供了该参数,将已经存在的该 figure id 则置为活跃状态,并返回它的引用,如果没有则创建并返回
     如果 num 为字符创,figure 的窗口标题改为 'num'
    
figsize : 元祖型整数,可选,默认: None
     设置 gigure 的宽高
dpi : 整数,可选,默认: None
     设置 figure 的解析度,默认为 figure.dpi
clear : 布尔类型,可选,默认: False
     如果为 True,图像将一直存在,直到被清除
```

### `add_subplot`

可以通过 `add_subplot` 画多张图

```python
>>> fig = plt.figure()
>>> # 创建一个 2x2 的图组(即最多 4 张图),并设定该图像编号
>>> ax1 = fig.add_subplot(2, 2, 1)
>>> # 创建其他几个,注意 jupyter 中想要所有图片
>>> # 在同一个窗口创建需要在同一个命令窗口运行
>>> ax2 = fig.add_subplot(2, 2, 2)
```

### `subplot` 

`subplot` 可以创建一个新的 `Figure` 对象,并且以 `numpy` 数组形式返回 `subplot` 对象

```python
>>> fig, axes = plt.subplots(2, 2)
>>> axes 

Figure 1
array([[<matplotlib.axes._subplots.AxesSubplot object at 0x7feb52fe78d0>,
        <matplotlib.axes._subplots.AxesSubplot object at 0x7feb52983c50>],
       [<matplotlib.axes._subplots.AxesSubplot object at 0x7feb529b5320>,
        <matplotlib.axes._subplots.AxesSubplot object at 0x7feb5295a9b0>]],
      dtype=object)
```

参数:

* `nrows` : `subplot` 的行数
* `ncols` : `subplot` 的列数
* `sharex` : 所有 `subplot` 应该使用相同的 X 轴刻度
* `sharey` : 所有 `subplot` 应该使用相同的 Y 轴刻度
* `subplot_kw` : 用于创建 `subplot` 的关键字字典

### 调整 `subplot` 周围的间距

默认情况下 `subplot` 外围以及 `subplot` 之间都有间距,可以通过 `subplots_adjust` 修改

```python
# subplots_adjust(left=None, bottom=None, right=None, top=None, wspace=None, hspace=None)
# wspace 和 hspace 用于控制宽高的百分比,可作用 subplot 键的间距

>>> # 将间距缩短成 0
>>> fig, axes = plt.subplots(2, 2, sharex=True, sharey=True)
>>> for i in range(2):
        for j in range(2):
            axes[i, j].hist(np.random.randn(500), bins=50, color='pink', alpha=0.8)
>>> plt.subplots_adjust(wspace=0, hspace=0)
```

### 颜色及线型

`plot` 函数接受 X/Y 坐标轴,同时接受颜色,线的类型,点的类型

颜色/线型/标记类型可以进行组合使用

**colors 参数**

        The following color abbreviations are supported:
    
        =============    ===============================
        character        color
        =============    ===============================
        ``'b'``          blue
        ``'g'``          green
        ``'r'``          red
        ``'c'``          cyan
        ``'m'``          magenta
        ``'y'``          yellow
        ``'k'``          black
        ``'w'``          white
        =============    ===============================
**markers 参数**

        =============    ===============================
        character        description
        =============    ===============================
        ``'.'``          point marker
        ``','``          pixel marker
        ``'o'``          circle marker(圆形)
        ``'v'``          triangle_down marker(倒三角形)
        ``'^'``          triangle_up marker(三角形)
        ``'<'``          triangle_left marker(左三角形)
        ``'>'``          triangle_right marker(右三角形)
        ``'1'``          tri_down marker(三分标记)
        ``'2'``          tri_up marker
        ``'3'``          tri_left marker
        ``'4'``          tri_right marker
        ``'s'``          square marker(正方形)
        ``'p'``          pentagon marker(五边形)
        ``'*'``          star marker(星星)
        ``'h'``          hexagon1 marker(六边形)
        ``'H'``          hexagon2 marker
        ``'+'``          plus marker(＋型)
        ``'x'``          x marker(x 型)
        ``'D'``          diamond marker(方形(旋转90°))
        ``'d'``          thin_diamond marker(菱形)
        ``'|'``          vline marker(| 型)
        ``'_'``          hline marker(_ 型)
        =============    ===============================
**linestyles 参数**

        =============    ===============================
        character        description
        =============    ===============================
        ``'-'``          solid line style(实线)
        ``'--'``         dashed line style(虚线)
        ``'-.'``         dash-dot line style(点划线)
        ``':'``          dotted line style(点线)
        =============    ===============================
Example format strings::

            'b'    # blue markers with default shape
            'ro'   # red circles
            'g-'   # green solid line
            '--'   # dashed line with default color
            'k^:'  # black triangle_up markers connected by a dotted line
### 刻度,标签和图例

* `plt.xlim([0, 10])`: X 轴范围,作用 AxesSubplot 
* `ax.get_xlim/ax.set_xlim` : 同理,不过式作用子图(subplot 对象)上, 跟灵活

### 设置标题,轴标签,刻度,刻度标签

1. 自定义轴的刻度

* `set_xticks`/`set_yticks` : 设置刻度的位置
* `set_xticklabels`/`set_ytickslabels` : 设置刻度标签

```python
>>> fig, axes = plt.subplots()
>>> axes.plot(np.random.randn(1000).cumsum())
>>> ticks = axes.set_xticks([0, 250, 500, 750, 100])
>>> labels = axes.set_xtickslabel(['one', 'two', 'three', 'four', 'five'],
                                 rotation=30,fontsize='small')
>>> # sotation 设置刻度标签倾斜 30°
>>> print(ticks)
[<matplotlib.axis.XTick object at 0x7feb5109cd68>, <matplotlib.axis.XTick object at 0x7feb5109c6d8>, <matplotlib.axis.XTick object at 0x7feb51239cc0>, <matplotlib.axis.XTick object at 0x7feb51056eb8>, <matplotlib.axis.XTick object at 0x7feb51061550>]
>>> print(labels)
[Text(0,0,'one'), Text(250,0,'two'), Text(500,0,'three'), Text(750,0,'four'), Text(1000,0,'five')]
```

2. 设置轴名称,设置图标题

* `set_title` :设置图标题

* `set_xlabel`/`set_ylabel` : 设置轴名称

```python
>>> axes.set_title('Average Price')
>>> axes.set_xlabel('Price')
```

3. 添加图例(legend)

图例(legend)是识别图标元素的重要工具

* 通过添加 `subplot` 时传入 `label` 参数

```python
>>> axes.plot(np.random.randn(100).cumsum(), 'k', label='defaul')
>>> # 设置图例位置
>>> axes.legend(loc='best')
```

### 注解以及在 subplot 上绘图

在指定的坐标处添加文字/图形/箭头等注解

1. 添加文字

`axes.text` 方法可以给图添加文字注解

```python
>>> # x/y 
>>> axes.text(x, y, 'content', family='monospace', fontsize=10)
```

2. 添加箭头

`axes.arrow` 

3. 添加标签

`axes.annotate` 可以在指定的 X 和 Y 坐标绘制标签

3. 添加图形

创建一个 shp 对象,然后通过 `axes.add_patch(shp) 添加倒 subplot 中

```python
>>> fig = plt.figure()
>>> axes = fig.add_subplot(1, 1, 1)
>>> # 第一个参数是图片添加的位置
>>> cric = plt.Circle((o.7, 0.2), 0.15, color='b', alpha=0.3)
>>> axes.add_patch(cric)
```

### 将图片保存到文件

图片通过 `plt.savefig` 保存

```python
>>> plt.savefig('example.png', dpi=400, bbox_inches='tight')
```

`savefig` 参数

![](/home/dxigui/git_repositories/notes/Notes/img/plt_savefig_args.png)

### matplotlib 配置

通过 `plt.rc` 修改 `matplotlib` 的全局变量

# 使用 Pandas 和 Seaborn huitu

`Pandas` 中的 `Series` 和 `DataFrame` 都自带 `plot` 绘图方法,可以简化图形绘制,实际上是 `Pandas` 调用 `matplotlib` 进行绘图

## 线形图

###  `Series` 绘制简单线形图

```python
>>> se = pd.Series(np.random.randn(10).cumsum(), index=np.arange(0, 100, 10))
>>> se.plot()
```

`Series` 中的 `index` 参数会被传到 `matplotlib` 来绘制 X 轴,使用 `use_index=False` 禁用该功能,然后通过 `xticks/yticks` 和 `xlim/yxlim` 对 X/Y 轴进行详细的设置

**Series plot 参数** 

![](/home/dxigui/git_repositories/notes/Notes/img/pd_plot_args1.png)

![](/home/dxigui/git_repositories/notes/Notes/img/pd_plot_args2.png)

2. `DataFrame` 绘制

在 `DataFrame` 会将 `columns` 参数中的列名当做 `subplot` 中的图例

```python
>>> df = pd.DataFrame(np.random.randn(10, 4).cumsum(0),
                      columns=['A', 'B', 'C', 'D'],
                      index=np.arange(0, 100, 10))
>>> df.plot()
```

**DataFrame plot 参数**

![](/home/dxigui/git_repositories/notes/Notes/img/pd_plot_args3.png)


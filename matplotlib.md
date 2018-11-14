# matplotlib

`matplotlib` 库主要是将数据可视化,可以导出常见的矢量(vector)和光栅(raster)图: PDF/SVG/JPG/PNG/BMP/GIF 等

## matplotlib API 入门

导入

```python
>>> import matplotlib.pyplot as plt
>>> import numpy as np
>>> import pandas as pd
```

### Figure 和 Subplot

1. `matplotlib`

`matplotlib` 的图像都位于 `Figure` 中

```python
>>> # 创建一个 Figure 对象
>>> fig = plt.figure()
```


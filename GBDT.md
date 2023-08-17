# GBDT

[GBDT的原理、公式推导、Python实现、可视化和应用 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/280222403)

### 一、基础概念

- CART回归树
- 集成学习==>Boosting
- 梯度下降



<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801204825634.png" alt="image-20230801204825634" style="zoom:67%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801204800702.png" alt="image-20230801204800702" style="zoom: 67%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801204936559.png" alt="image-20230801204936559" style="zoom:67%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801205009371.png" alt="image-20230801205009371" style="zoom:67%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801205031727.png" alt="image-20230801205031727" style="zoom:67%;" />



### 二、算法原理

#### 1.基础：提升树 BDT

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801205127181.png" alt="image-20230801205127181" style="zoom:67%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801205207894.png" alt="image-20230801205207894" style="zoom:67%;" />



#### 2.重要思想：GBDT 用梯度代替残差

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801205305928.png" alt="image-20230801205305928" style="zoom:67%;" />

#### 3.算法过程



<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801205346914.png" alt="image-20230801205346914" style="zoom:67%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801205415549.png" alt="image-20230801205415549" style="zoom:67%;" />



### 三、GBDT VS 随机森林

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801204626714.png" alt="image-20230801204626714" style="zoom:70%;" />



### 四、代码

```python
"""
@des：基于 sklearn 实现 GBDT 可视化
"""
import numpy as np
import pydotplus
from sklearn.ensemble import GradientBoostingRegressor

X = np.arange(1, 11).reshape(-1, 1) # -1表示该行或列可以是任意长度
y = np.array([5.56, 5.70, 5.91, 6.40, 6.80, 7.05, 8.90, 8.70, 9.00, 9.05])

gbdt = GradientBoostingRegressor(max_depth=4, criterion ='friedman_mse').fit(X, y)

# 预测
x_test = np.array([2.2, 3.3, 4.4]).reshape(-1,1)
y_predit = gbdt.predict(x_test)
print(y_predit)

from IPython.display import Image
from pydotplus import graph_from_dot_data
from sklearn.tree import export_graphviz

# 访问梯度提升树(GBDT)模型中的特定基本决策树：这里以第6棵树为例
sub_tree = gbdt.estimators_[5, 0] #表示访问GBDT模型中第6棵树的第一个基本决策树
dot_data = export_graphviz(sub_tree, out_file=None, filled=True, rounded=True, special_characters=True, precision=2)

# 生成决策树的可视化文件
# 如果feature_name和class_name包含中文，使用方法2
# 1.将dot_data写入到txt文件中
f = open('dot_data.txt', 'w')
f.write(dot_data)
f.close()

# 2.修改原来dot_data.txt中的字体及编码格式，并将其另存为一个新的dot_data_new.txt文件
import re
f_old = open('dot_data.txt', 'r')
f_new = open('dot_data_new.txt', 'w', encoding='utf-8')
for line in f_old:
    if 'fontname' in line:
        font_re = 'fontname=(.*?)]'
        old_font = re.findall(font_re, line)[0]
        line = line.replace(old_font, 'SimHei')
    f_new.write(line)
f_old.close()
f_new.close()

# 3.调用os.system系统函数来使用graphviz插件从而生成可视化文件
# -Tpdf表示生成PDF格式的文件，-Tpng表示生成PNG格式的图片文件
import os
os.system('dot -Tpdf dot_data_new.txt -o 决策树模型.pdf')
# os.system('dot -Tpng dot_data_new.txt -o 决策树模型.png')
```

【第六棵决策树的可视化结果】：

![image-20230801204433075](https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230801204433075.png)




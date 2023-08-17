##  Matplotlib

直方图，条形图，饼图，散点图



### 图的构成

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809190924513.png" alt="image-20230809190924513" style="zoom: 50%;" />

坐标轴(axis)、坐标轴名称(axis label)、坐标轴刻度(tick)、坐标轴刻度标签(tick label)、网格线(grid)、图例(legend)、标题(title)

##### 显示中文

```python
plt.rcParams['font.family']=['STFangsong']
#或
plt.rcParams['font.sans-serif']=['SimHei']
```

显示负号

```python
plt.rcParams['axes.unicode_minus']=False
```

设置标题`title`

```python
import matplotlib.pyplot as plt

plt.title("title")		#设置标题
plt.show()				#显示图片
```

`figure `：画布

```python
fig = plt.figure()
```

`axes`：绘图区域

一个figure可以有多个subplot，那么每一个subplot就是一个axes

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809193022260.png" alt="image-20230809193022260" style="zoom:50%;" />





##### `figure`画布

```python
fig = plt.figure(figsize=(6,3))		#创建一个宽为6，高为3的画布
```

##### `Axis `坐标轴

```python
plt.xlim(0,6)			#x轴坐标轴
plt.ylim((0, 3))		#y轴坐标轴
plt.xlabel('X')			#x轴标签
plt.ylabel('Y')			#y轴标签
```

`ax.xaxis` / ` ax.yaxis`

每个坐标轴实际上也是由竖线和数字组成的，每一个竖线其实也是一个axis的subplot，因此`ax.xaxis`也存在``axes`对象。对这个axes进行编辑就会修改xaxis图像上的表现。

##### `legend`图例

```python
x = np.linspace(1, 10, 10)
y = 3 * x
z = 3 / x
plt.xlabel('x轴')
plt.ylabel('y轴')
line1, = plt.plot(x,y,color='r',linewidth=4,linestyle='-',label='图标1')
line2, = plt.plot(x,z,color='b',linewidth=1.5,linestyle='-',label='图标2')
plt.legend(handles=[line1,line2],labels=['图标11','图标22'],loc='best')
plt.show()
```

- **labels**：图例名称（能够覆盖plt.plot( )中label参数值）

- **handles**：所画线条的**实例对象**

  **handles若要获取线条图像的实例**，必须用**x, = plt.plot( )**让plt.plot( )返回一个二元组值。

- **loc**：图例位置

  - ***loc = 'best'***：图例自动‘安家’在一个坐标面内的数据图表最少的位置

  - ***loc = (x_bias, y_bias)***：（x_bias, y_bias）表示图例举例左下角的位置比例。例如，当坐标轴的范围限制为xlim=(0, 16), ylim=(0, 9)，**x_bias = x/(x_max-x_min) , y_bias = y/(y_max-y_min) )**（即进行归一化处理）

  - ***loc = 'XXX'***：选择坐标面中的九个位置之一。loc = 'center'表示坐标平面中心位置，九种参数值及所对应位置如下图所示：

    <img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809195600980.png" alt="image-20230809195600980" style="zoom:67%;" />

##### subplot 子图

```python
x=np.linspace(0,10,200)#从0到10之间等距产生200个值
y=np.sin(x)

ax1 = plt.subplot(2, 2, 1)
plt.plot(x,np.sin(x), 'k')

ax2 = plt.subplot(2, 2, 2, sharey=ax1) # 与 ax1 共享y轴
plt.plot(x, np.cos(x), 'g')

ax3 = plt.subplot(2, 2, 3)
plt.plot(x, x, 'r')

ax4 = plt.subplot(2, 2, 4, sharey=ax3) # 与 ax3 共享y轴
plt.plot(x, 2*x, 'y')

plt.show()
```

- 第一个参数：子图的总行数
- 第二个参数：子图的总列数
- 第三个参数：活跃区域

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809205450990.png" alt="image-20230809205450990" style="zoom:67%;" />



##### plt.annotate 添加注释

```python
import matplotlib.pyplot as plt
plt.rcParams['font.sans-serif']=['SimHei']
plt.rcParams['axes.unicode_minus']=False
plt.style.use('seaborn-whitegrid')

plt.figure(figsize=(5, 4), dpi=120)
plt.plot([1, 2, 5], [7, 8, 9])

plt.annotate(text='basic unility of annotate',  # 注释内容
             xy=(2, 8),  			# 箭头末端位置

             xytext=(1.0, 8.75),  	# 文本起始位置

             weight='bold',  		# 文本格式

             color='b',  			# 文本颜色
             # 箭头属性设置
             arrowprops=dict(facecolor='r',
                             alpha=0.16,  # 透明度
                             arrowstyle='fancy',  # 箭头类型
                             hatch='--',  # 填充形状
                             connectionstyle='arc3,rad=0.5',    #箭头弯曲
                             # 其它参考matplotlib.patches.Polygon中任何参数
                             ),
             )
plt.show()
```

- **s：**注释文本的内容

- **xy：**被注释的坐标位置点，二维元组形如(x,y)

- **xytext：**注释文本的坐标位置点，也是二维元组，默认与xy相同

- arrowstyle：箭头形状

  <img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809204643654.png" alt="image-20230809204643654" style="zoom: 50%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809204945807.png" alt="image-20230809204945807" style="zoom:67%;" />



##### pyplot.text 添加文本

```python
plt.style.use('seaborn-whitegrid')		#修改样式

plt.figure(figsize=(5, 4), dpi=120)
plt.plot([1, 2, 5], [7, 8, 9])
plt.text(x=2.2,  # 文本x轴坐标

         y=8,  # 文本y轴坐标

         s='basic unility of text',  # 文本内容

         rotation=10,  # 文字旋转角度

         ha='left',  # x=2.2是文字的左端位置，可选'center', 'right', 'left'

         va='baseline',  # y=8是文字的低端位置，可选'center', 'top', 'bottom', 'baseline', 'center_baseline'

         fontdict=dict(fontsize=12,
                       color='r',
                       family='monospace',  # 字体,可选'serif', 'sans-serif', 'cursive', 'fantasy', 'monospace'
                       weight='bold',  # 磅值，可选'light', 'normal', 'medium', 'semibold', 'bold', 'heavy', 'black'
                       ),  # 字体属性设置

         # 添加文字背景文本框
         bbox={'facecolor': '#74C476',  # 填充色
               'edgecolor': 'b',  # 外框色
               'alpha': 0.5,  # 框透明度
               'pad': 0.8,  # 本文与框周围距离
               'boxstyle':'sawtooth' #形状：
               }
         )
plt.show()
```

- 文本框的`boxstyle`：

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809203254921.png" alt="image-20230809203254921" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809203441193.png" alt="image-20230809203441193" style="zoom:67%;" />



##### plt.style.use 样式美化，定制画布风格

- 获取所有的自带样式

  ```python
  print(plt.style.available) # 打印样式列表
  ['bmh', 'classic', 'dark_background', 'fast', 
  'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn-bright', 
  'seaborn-colorblind', 'seaborn-dark-palette', 'seaborn-dark', 'seaborn-darkgrid',
   'seaborn-deep', 'seaborn-muted', 'seaborn-notebook', 'seaborn-paper', 
  'seaborn-pastel', 'seaborn-poster', 'seaborn-talk', 'seaborn-ticks',
   'seaborn-white', 'seaborn-whitegrid', 'seaborn', 'Solarize_Light2', 
  'tableau-colorblind10', '_classic_test']
  ```

- 修改样式

  ```python
  plt.style.use('样式名称')
  #如：plt.style.use('seaborn-whitegrid'
  ```

#### bar 柱状图

##### 单系列柱状图

```python
x = np.arange(10)
y = np.random.randint(0,20,10)
plt.bar(x, y)
plt.show()
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809205716455.png" alt="image-20230809205716455" style="zoom:67%;" />

##### 水平向条形图

```python
df.plot.barh( grid = True, colormap = 'BuGn_r')
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809210245521.png" alt="image-20230809210245521" style="zoom:67%;" />

##### 多系列柱状图

```python
# 多系列柱状图
df = pd.DataFrame(np.random.rand(10, 3), columns = ['a', 'b', 'c'])
df.plot(kind = 'bar'， grid = True, colormap = 'summer_r')
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809205951379.png" alt="image-20230809205951379" style="zoom:67%;" />

##### 多系列堆叠图

```python
# 多系列堆叠图(添加stacked = True属性)
df.plot(kind = 'bar',  grid = True, colormap = 'Blues_r', stacked = True)
```

#### scatter 散点图

- c：颜色（b--blue, c--cyan,g--green,k--black,m--magenta,r--red,w--white,y--yellow）
- s：控制点的大小，默认为20
- marker：散点图点的形状，默认为圆形
- alpha：透明度





- 
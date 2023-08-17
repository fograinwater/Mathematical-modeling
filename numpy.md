## numpy

矩阵处理工具



### NumPy Ndarray 对象

ndarray是一个 N 维数组对象 ，它是一系列同类型数据的集合，索引从 0 开始。

ndarray 内部由以下内容组成：

- 一个指向数据（内存或内存映射文件中的一块数据）的指针。
- 数据类型或 dtype，描述在数组中的固定大小值的格子。
- 一个表示数组形状（shape）的元组，表示各维度大小的元组。
- 一个跨度元组（stride），其中的整数指的是为了前进到当前维度下一个元素需要"跨过"的字节数



### NumPy 数据类型

numpy 支持的数据类型比 Python 内置的类型要多很多，基本上可以和 C 语言的数据类型对应上，其中部分类型对应为 Python 内置的类型。下表列举了常用 NumPy 基本类型。

numpy 的数值类型实际上是 dtype 对象的实例，并对应唯一的字符，包括 np.bool_，np.int32，np.float32，等等。

| 名称       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| bool_      | 布尔型数据类型（True 或者 False）                            |
| int_       | 默认的整数类型（类似于 C 语言中的 long，int32 或 int64）     |
| intc       | 与 C 的 int 类型一样，一般是 int32 或 int 64                 |
| intp       | 用于索引的整数类型（类似于 C 的 ssize_t，一般情况下仍然是 int32 或 int64） |
| int8       | 字节（-128 to 127）                                          |
| int16      | 整数（-32768 to 32767）                                      |
| int32      | 整数（-2147483648 to 2147483647）                            |
| int64      | 整数（-9223372036854775808 to 9223372036854775807）          |
| uint8      | 无符号整数（0 to 255）                                       |
| uint16     | 无符号整数（0 to 65535）                                     |
| uint32     | 无符号整数（0 to 4294967295）                                |
| uint64     | 无符号整数（0 to 18446744073709551615）                      |
| float_     | float64 类型的简写                                           |
| float16    | 半精度浮点数，包括：1 个符号位，5 个指数位，10 个尾数位      |
| float32    | 单精度浮点数，包括：1 个符号位，8 个指数位，23 个尾数位      |
| float64    | 双精度浮点数，包括：1 个符号位，11 个指数位，52 个尾数位     |
| complex_   | complex128 类型的简写，即 128 位复数                         |
| complex64  | 复数，表示双 32 位浮点数（实数部分和虚数部分）               |
| complex128 | 复数，表示双 64 位浮点数（实数部分和虚数部分）               |



#### 数据类型对象 (dtype)

数据类型对象（numpy.dtype 类的实例）用来描述与数组对应的内存区域是如何使用，它描述了数据的以下几个方面：：

- 数据的类型（整数，浮点数或者 Python 对象）
- 数据的大小（例如， 整数使用多少个字节存储）
- 数据的字节顺序（小端法或大端法）
- 在结构化类型的情况下，字段的名称、每个字段的数据类型和每个字段所取的内存块的部分
- 如果数据类型是子数组，那么它的形状和数据类型是什么。

dtype 对象是使用以下语法构造的：

```python
numpy.dtype(object, align, copy)
```

- object - 要转换为的数据类型对象
- align - 如果为 true，填充字段使其类似 C 的结构体。
- copy - 复制 dtype 对象 ，如果为 false，则是对内置数据类型对象的引用



### NumPy 数组属性

数组的维数称为秩（rank），秩就是轴的数量。一维数组的秩为 1，二维数组的秩为 2，类推。

【区分“维数”和“维度”】：

numpy数组有多少维（维数），每一维含有多少个元素（每个维度的长度）。

NumPy 的数组中比较重要 ndarray 对象属性有：

| 属性             | 说明                                                         |
| :--------------- | :----------------------------------------------------------- |
| ndarray.ndim     | 秩，即轴的数量或维度的数量                                   |
| ndarray.shape    | 数组的维度，对于矩阵，n 行 m 列                              |
| ndarray.size     | 数组元素的总个数，相当于 .shape 中 n*m 的值。也可以用于调整数组每一维的维度。 |
| ndarray.dtype    | ndarray 对象的元素类型                                       |
| ndarray.itemsize | ndarray 对象中每个元素的大小，以字节为单位                   |
| ndarray.real     | ndarray元素的实部                                            |
| ndarray.imag     | ndarray 元素的虚部                                           |

**使用shape属性或reshape函数调整数组的大小：**

```python
a = np.array([[1, 2, 3], [4, 5, 6]])
a.shape = (3, 2)
print(a)
b = a.reshape(2,3)
print (b)

#输出：
[[1 2]
 [3 4]
 [5 6]]
[[1 2 3]
 [4 5 6]]
```

注：ndarray.reshape 通常返回的是非拷贝副本，即改变返回后数组的元素，原数组对应元素的值也会改变。

```python
In [1]: import numpy as np

In [2]: a=np.array([[1,2,3],[4,5,6]])

In [3]: a
Out[3]:
array([[1, 2, 3],
       [4, 5, 6]])

In [4]: b=a.reshape((6,))

In [5]: b
Out[5]: array([1, 2, 3, 4, 5, 6])

In [6]: b[0]=100

In [7]: b
Out[7]: array([100,   2,   3,   4,   5,   6])

In [8]: a
Out[8]:
array([[100,   2,   3],
       [  4,   5,   6]])
```

##### 对axis的理解：

在 NumPy中，每一个线性的数组称为是一个轴（axis），也就是维度（dimensions）。比如说，二维数组相当于是两个一维数组，其中第一个一维数组中每个元素又是一个一维数组。所以一维数组就是 NumPy 中的轴（axis），第一个轴相当于是底层数组，第二个轴是底层数组里的数组。而轴的数量——秩，就是数组的维数。

很多时候可以声明 axis。axis=0，表示沿着第 0 轴进行操作，即对每一列进行操作；axis=1，表示沿着第1轴进行操作，即对每一行进行操作。

例如，对于二维数组：

![image-20230806104430630](https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230806104430630.png)

- a.mean中的axis=x表示**沿轴x的方向**，**求剩余的轴上的每一个元素的均值**。其结果的维度肯定是剩余轴构成的维度。

```python
a = np.array([[1, 2, 3], [4, 5, 6]])
print(a)
b = a.mean(axis=1)
print(b)

#输出：
[[1 2 3]
 [4 5 6]]
[2. 5.] 
```



### 创建数组

#### np.array

```python
numpy.array(object, dtype = None, copy = True, order = None, subok = False, ndmin = 0)
```

**参数说明：**

| 名称   | 描述                     |
| :----- | :----------------------- |
| object | 数组或嵌套的数列         |
| dtype  | 数组元素的数据类型，可选 |
| ndmin  | 指定生成数组的最小维度   |



#### numpy.empty

numpy.empty 方法用来创建一个指定形状（shape）、数据类型（dtype）且未初始化的数组：

```python
numpy.empty(shape, dtype = float, order = 'C')
```

| 参数  | 描述                                                         |
| :---- | :----------------------------------------------------------- |
| shape | 数组形状                                                     |
| dtype | 数据类型，可选                                               |
| order | 有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序。 |



#### 使用列表、元组创建数组

#### numpy.array

同时使用列表和元组创建数组时，意味着创建的是二维数组，需要在最外面加 `[]`.

```python
>>> x = np.array([2, 3, 1, 0])
>>> x = np.array([[1,2,3],(4.0,5,6)])

#输出：
[1 2 3]
[1 2 3]
[[1. 2. 3.]
 [4. 5. 6.]]
```

#### numpy.asarray

numpy.asarray 类似 numpy.array，但 numpy.asarray 参数只有三个，比 numpy.array 少两个。

```python
numpy.asarray(a, dtype = None, order = None)
```

参数说明：

| 参数  | 描述                                                         |
| :---- | :----------------------------------------------------------- |
| a     | 任意形式的输入参数，可以是，列表, 列表的元组, 元组, 元组的元组, 元组的列表，多维数组 |
| dtype | 数据类型，可选                                               |
| order | 可选，有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序。 |



#### 原生数组的创建

##### zeros(shape)

将创建一个用指定形状用0填充的数组。默认的dtype是float64。

##### ones(shape)

将创建一个用1个值填充的数组

```python
numpy.zeros(shape, dtype = float, order = 'C')
numpy.ones(shape, dtype = None, order = 'C')
```

参数说明：

| 参数  | 描述                                                |
| :---- | :-------------------------------------------------- |
| shape | 数组形状                                            |
| dtype | 数据类型，可选                                      |
| order | 'C' 用于 C 的行数组，或者 'F' 用于 FORTRAN 的列数组 |



##### numpy.zeros_like 

用于创建一个与给定数组具有相同形状的数组，数组元素以 0 来填充

##### numpy.ones_like 

用于创建一个与给定数组具有相同形状的数组，数组元素以 1 来填充

```python
numpy.zeros_like(a, dtype=None, order='K', subok=True, shape=None)
numpy.ones_like(a, dtype=None, order='K', subok=True, shape=None)
```

参数说明：

| 参数  | 描述                                                         |
| :---- | :----------------------------------------------------------- |
| a     | 给定要创建相同形状的数组                                     |
| dtype | 创建的数组的数据类型                                         |
| order | 数组在内存中的存储顺序，可选值为 'C'（按行优先）或 'F'（按列优先），默认为 'K'（保留输入数组的存储顺序） |
| subok | 是否允许返回子类，如果为 True，则返回一个子类对象，否则返回一个与 a 数组具有相同数据类型和存储顺序的数组 |
| shape | 创建的数组的形状，如果不指定，则默认为 a 数组的形状。        |



#### 从数值范围创建数组

##### np.arange()

将创建具有有规律递增值的数组。根据 start 与 stop 指定的范围以及 step 设定的步长，生成一个 ndarray。

```python
numpy.arange([start], stop, [step], [dtype])
```

参数说明：

| 参数    | 描述                                                         |
| :------ | :----------------------------------------------------------- |
| `start` | 起始值，默认为`0`                                            |
| `stop`  | 终止值（不包含）                                             |
| `step`  | 步长，默认为`1`                                              |
| `dtype` | 返回`ndarray`的数据类型，如果没有提供，则会使用输入数据的类型。 |



##### np.linspace() 

将创建具有指定数量元素的数组，并在指定的开始值和结束值之间平均间隔。数组是一个等差数列构成的，格式如下：

```python
np.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)
```

参数说明：

| 参数       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| `start`    | 序列的起始值                                                 |
| `stop`     | 序列的终止值，如果`endpoint`为`true`，该值包含于数列中       |
| `num`      | 要生成的等步长的样本数量，默认为`50`                         |
| `endpoint` | 该值为 `true` 时，数列中包含`stop`值，反之不包含，默认是True。 |
| `retstep`  | 如果为 True 时，生成的数组中会显示间距，反之不显示。         |
| `dtype`    | `ndarray` 的数据类型                                         |



##### np.tile()

np.tile(A,res)：把数组 A 当成一个元素来构造 shape 为 res 的数组

（A 是个数组，reps 是个元组）

如下图：

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230809165838811.png" alt="image-20230809165838811" style="zoom:67%;" />

例如：

```python
a = np.array([0,1,2,3])
a = np.tile(a, 2)   # shape可以是一维的，此时可以不用元组表示
#或：a = np.tile(np.array([0,1,2,3]), 2)

#输出:
[0 1 2 3 0 1 2 3]
```

```python
np.tile(np.arange(1,25),(1,10))

#输出:
[[ 1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
   1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
   1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
   1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
   1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
   1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
   1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
   1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
   1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24
   1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24]]
```



### NumPy 切片和索引

ndarray对象的内容可以通过索引或切片来访问和修改，与 Python 中 list 的切片操作一样。

#### slice 函数

切片对象可以通过内置的 slice 函数，并设置 start, stop 及 step 参数进行，从原数组中切割出一个新数组。

```python
import numpy as np
 
a = np.arange(10)
s = slice(2,7,2)   # 从索引 2 开始到索引 7 停止，间隔为2
print (a[s])
```

#### 使用冒号分隔切片参数 **start:stop:step** 

冒号 **:** 的解释：

- 如果只放置一个参数，如 **[2]**，将返回与该索引相对应的单个元素。
- 如果为 **[2:]**，表示从该索引开始以后的所有项都将被提取。
- 如果使用了两个参数，如 **[2:7]**，那么则提取两个索引(不包括停止索引)之间的项。
- 三个参数就对应**start:stop:step** 

```python
import numpy as np
 
a = np.arange(10)  
b = a[2:7:2]   # 从索引 2 开始到索引 7 停止，间隔为 2
print(b)

#输出：
[2  4  6]
```

numpy.argmax(array, axis) 用于返回一个numpy数组中最大值的索引值。当一组中同时出现几个最大值时，返回第一个最大值的索引值。



### NumPy 迭代数组

NumPy 迭代器对象 numpy.nditer 提供了一种灵活访问一个或者多个数组元素的方式。

```python
a = np.arange(6).reshape(2,3)
print ('原始数组是：')
print (a)
print ('迭代输出元素：')
for x in np.nditer(a):
    print (x, end=", " )

#输出：
原始数组是：
[[0 1 2]
 [3 4 5]]
迭代输出元素：
0, 1, 2, 3, 4, 5, 
```



### Numpy 数组操作

Numpy 中包含了一些函数用于处理数组，大概可分为以下几类：

- [修改数组形状](https://www.runoob.com/numpy/numpy-array-manipulation.html#numpy_oparr1)
- [翻转数组](https://www.runoob.com/numpy/numpy-array-manipulation.html#numpy_oparr2)
- [修改数组维度](https://www.runoob.com/numpy/numpy-array-manipulation.html#numpy_oparr3)
- [连接数组](https://www.runoob.com/numpy/numpy-array-manipulation.html#numpy_oparr4)
- [分割数组](https://www.runoob.com/numpy/numpy-array-manipulation.html#numpy_oparr5)
- [数组元素的添加与删除](https://www.runoob.com/numpy/numpy-array-manipulation.html#numpy_oparr6)

------

#### 修改数组形状

| 函数      | 描述                                               |
| :-------- | :------------------------------------------------- |
| `reshape` | 不改变数据的条件下修改形状                         |
| `flat`    | 数组元素迭代器                                     |
| `flatten` | 返回一份数组拷贝，对拷贝所做的修改不会影响原始数组 |
| `ravel`   | 返回展开数组                                       |

##### numpy.reshape

numpy.reshape 函数可以在**不改变数据**的条件下修改形状，格式如下：

```python
numpy.reshape(arr, newshape, order='C')
```

- `arr`：要修改形状的数组
- `newshape`：整数或者整数数组，新的形状应当兼容原有形状
- `order`：'C' -- 按行，'F' -- 按列，'A' -- 原顺序，'k' -- 元素在内存中的出现顺序。



##### numpy.ndarray.flat

numpy.ndarray.flat 是一个数组元素迭代器，实例如下:

```python
a = np.arange(9).reshape(3,3) 
print ('原始数组：')
for row in a:
    print (row)
 
#对数组中每个元素都进行处理，可以使用flat属性，该属性是一个数组元素迭代器：
print ('迭代后的数组：')
for element in a.flat:
    print (element)
    
#输出：
原始数组：
[0 1 2]
[3 4 5]
[6 7 8]
迭代后的数组：
0
1
2
3
4
5
6
7
8
```

##### numpy.ndarray.flatten

numpy.ndarray.flatten 返回一份**数组拷贝**，对拷贝所做的修改**不会影响原始数组**，格式如下：

```python
ndarray.flatten(order='C')
```

```python
a = np.arange(8).reshape(2,4)
 
print ('原数组：')
print (a)
# 默认按行
 
print ('展开的数组：')
print (a.flatten())
 
print ('以 F 风格顺序展开的数组：')
print (a.flatten(order = 'F'))

#输出：
原数组：
[[0 1 2 3]
 [4 5 6 7]]
展开的数组：
[0 1 2 3 4 5 6 7]
以 F 风格顺序展开的数组：
[0 4 1 5 2 6 3 7]
```

##### numpy.ravel

numpy.ravel() **展平**的数组元素，顺序通常是"C风格"，返回的是数组视图（view，有点类似 C/C++引用reference的意味），**修改会影响原始数组**。

该函数接收两个参数：

```python
numpy.ravel(a, order='C')
```

```python
a = np.arange(8).reshape(2,4)
 
print ('原数组：')
print (a)
 
print ('调用 ravel 函数之后：')
print (a.ravel())
 
print ('以 F 风格顺序调用 ravel 函数之后：')
print (a.ravel(order = 'F'))

#输出：
原数组：
[[0 1 2 3]
 [4 5 6 7]]
调用 ravel 函数之后：
[0 1 2 3 4 5 6 7]
以 F 风格顺序调用 ravel 函数之后：
[0 4 1 5 2 6 3 7]
```



#### 翻转数组

| 函数        | 描述                       |
| :---------- | :------------------------- |
| `transpose` | 对换数组的维度             |
| `ndarray.T` | 和 `self.transpose()` 相同 |

##### numpy.transpose

numpy.transpose 函数用于对换数组的维度，格式如下：

```python
numpy.transpose(arr, axes)
```

参数说明:

- `arr`：要操作的数组
- `axes`：整数列表，对应维度，通常所有维度都会对换。

```python
a = np.arange(12).reshape(3, 4)

print('原数组：')
print(a)

print('对换数组：')
print(np.transpose(a))

#输出：
原数组：
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
对换数组：
[[ 0  4  8]
 [ 1  5  9]
 [ 2  6 10]
 [ 3  7 11]]
```

##### numpy.ndarray.T

```python
a = np.arange(12).reshape(3, 4)

print('原数组：')
print(a)

print('转置数组：')
print(a.T)

#输出：
原数组：
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
转置数组：
[[ 0  4  8]
 [ 1  5  9]
 [ 2  6 10]
 [ 3  7 11]]
```



#### 连接数组

| 函数          | 描述                           |
| :------------ | :----------------------------- |
| `concatenate` | 连接沿现有轴的数组序列         |
| `stack`       | 沿着新的轴加入一系列数组       |
| `hstack`      | 水平堆叠序列中的数组（列方向） |
| `vstack`      | 竖直堆叠序列中的数组（行方向） |

##### numpy.concatenate

numpy.concatenate 函数用于**沿指定轴**连接**相同形状**的两个或多个数组，格式如下：

```python
numpy.concatenate((a1, a2, ...), axis)
```

参数说明：

- `a1, a2, ...`：相同类型的数组
- `axis`：沿着它连接数组的轴，默认为 0

```python
a = np.array([[1, 2], [3, 4]])

print('第一个数组：')
print(a)
b = np.array([[5, 6], [7, 8]])

print('第二个数组：')
print(b)
# 两个数组的维度相同

print('沿轴 0 连接两个数组：')
print(np.concatenate((a, b)))

print('沿轴 1 连接两个数组：')
print(np.concatenate((a, b), axis=1))

#输出：
第一个数组：
[[1 2]
 [3 4]]
第二个数组：
[[5 6]
 [7 8]]
沿轴 0 连接两个数组：
[[1 2]
 [3 4]
 [5 6]
 [7 8]]
沿轴 1 连接两个数组：
[[1 2 5 6]
 [3 4 7 8]]
```



#### 分割数组

| 函数     | 数组及操作                             |
| :------- | :------------------------------------- |
| `split`  | 将一个数组分割为多个子数组             |
| `hsplit` | 将一个数组水平分割为多个子数组（按列） |
| `vsplit` | 将一个数组垂直分割为多个子数组（按行） |

##### numpy.split

numpy.split 函数沿特定的轴将数组分割为子数组，格式如下：

```python
numpy.split(ary, indices_or_sections, axis)
```

参数说明：

- `ary`：被分割的数组
- `indices_or_sections`：如果是一个整数，就用该数平均切分，如果是一个数组，为沿轴切分的位置（左开右闭）
- `axis`：设置沿着哪个方向进行切分，默认为 0，横向切分，即水平方向。为 1 时，纵向切分，即竖直方向。

```python
a = np.arange(9)

print('第一个数组：')
print(a)

print('将数组分为三个大小相等的子数组：')
b = np.split(a, 3)
print(b)

print('将数组在一维数组中表明的位置分割：')
b = np.split(a, [4, 7])
print(b)

#输出：
第一个数组：
[0 1 2 3 4 5 6 7 8]
将数组分为三个大小相等的子数组：
[array([0, 1, 2]), array([3, 4, 5]), array([6, 7, 8])]
将数组在一维数组中表明的位置分割：
[array([0, 1, 2, 3]), array([4, 5, 6]), array([7, 8])]
```

axis 为 0 时在水平方向分割，axis 为 1 时在垂直方向分割：

```python
a = np.arange(16).reshape(4, 4)
print('第一个数组：')
print(a)
print('默认分割（0轴）：')
b = np.split(a,2)
print(b)

print('沿水平方向分割：')
c = np.split(a,2,1)
print(c)

#输出：
第一个数组：
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]
 [12 13 14 15]]
默认分割（0轴）：
[array([[0, 1, 2, 3],
       [4, 5, 6, 7]]), array([[ 8,  9, 10, 11],
       [12, 13, 14, 15]])]
沿水平方向分割：
[array([[ 0,  1],
       [ 4,  5],
       [ 8,  9],
       [12, 13]]), array([[ 2,  3],
       [ 6,  7],
       [10, 11],
       [14, 15]])]
```



#### 数组元素的添加与删除

| 函数     | 元素及描述                               |
| :------- | :--------------------------------------- |
| `resize` | 返回指定形状的新数组                     |
| `append` | 将值添加到数组末尾                       |
| `insert` | 沿指定轴将值插入到指定下标之前           |
| `delete` | 删掉某个轴的子数组，并返回删除后的新数组 |
| `unique` | 查找数组内的唯一元素                     |

##### numpy.resize

numpy.resize 函数返回指定大小的新数组。

如果新数组大小大于原始大小，则包含原始数组中的元素的副本。

```python
numpy.resize(arr, shape)
```

参数说明：

- `arr`：要修改大小的数组
- `shape`：返回数组的新形状



##### numpy.append

numpy.append 函数在数组的末尾添加值。 追加操作会分配整个数组，并把原来的数组复制到新数组中。 此外，输入数组的维度必须匹配否则将生成ValueError。

append 函数**返回的始终是一个一维数组**。

```
numpy.append(arr, values, axis=None)
```

参数说明：

- `arr`：输入数组
- `values`：要向`arr`添加的值，需要和`arr`形状相同（除了要添加的轴）
- `axis`：默认为 None。当axis无定义时，是横向加成，返回总是为一维数组！当axis有定义的时候，分别为0和1的时候。当axis有定义的时候，分别为0和1的时候（列数要相同）。当axis为1时，数组是加在右边（行数要相同）

```python
a = np.array([[1, 2, 3], [4, 5, 6]])

print('第一个数组：')
print(a)

print('向数组添加元素：')
print(np.append(a, [7, 8, 9]))

print('沿轴 0 添加元素：')
print(np.append(a, [[7, 8, 9]], axis=0))

print('沿轴 1 添加元素：')
print(np.append(a, [[5, 5, 5], [7, 8, 9]], axis=1))

#输出：
第一个数组：
[[1 2 3]
 [4 5 6]]
向数组添加元素：
[1 2 3 4 5 6 7 8 9]
沿轴 0 添加元素：
[[1 2 3]
 [4 5 6]
 [7 8 9]]
沿轴 1 添加元素：
[[1 2 3 5 5 5]
 [4 5 6 7 8 9]]
```



##### numpy.insert

numpy.insert 函数在给定索引之前，沿给定轴在输入数组中插入值。

如果值的类型转换为要插入，则它与输入数组不同。 插入没有原地的，函数会返回一个新数组。 此外，如果未提供轴，则输入数组会被展开。

```
numpy.insert(arr, obj, values, axis)
```

参数说明：

- `arr`：输入数组
- `obj`：在其之前插入值的索引
- `values`：要插入的值
- `axis`：沿着它插入的轴，如果未提供，则输入数组会被展开

```python
a = np.array([[1, 2], [3, 4], [5, 6]])

print('第一个数组：')
print(a)

print('未传递 Axis 参数。 在删除之前输入数组会被展开。')
print(np.insert(a, 3, [11, 12]))
print('传递了 Axis 参数。 会广播值数组来配输入数组。')

print('沿轴 0 广播：')
print(np.insert(a, 1, [11], axis=0))

print('沿轴 1 广播：')
print(np.insert(a, 1, 11, axis=1))

#输出：
第一个数组：
[[1 2]
 [3 4]
 [5 6]]
未传递 Axis 参数。 在删除之前输入数组会被展开。
[ 1  2  3 11 12  4  5  6]
传递了 Axis 参数。 会广播值数组来配输入数组。
沿轴 0 广播：
[[ 1  2]
 [11 11]
 [ 3  4]
 [ 5  6]]
沿轴 1 广播：
[[ 1 11  2]
 [ 3 11  4]
 [ 5 11  6]]
```

##### numpy.delete

numpy.delete 函数返回从输入数组中删除指定子数组的新数组。 与 insert() 函数的情况一样，如果未提供轴参数，则输入数组将展开。

```
Numpy.delete(arr, obj, axis)
```

参数说明：

- `arr`：输入数组
- `obj`：可以被切片，整数或者整数数组，表明要从输入数组删除的子数组
- `axis`：沿着它删除给定子数组的轴，如果未提供，则输入数组会被展开

```python
a = np.arange(12).reshape(3, 4)

print('第一个数组：')
print(a)

print('未传递 Axis 参数。 在插入之前输入数组会被展开。')
print(np.delete(a, 5))

print('删除第二列：')
print(np.delete(a, 1, axis=1))

print('包含从数组中删除的替代值的切片：')
a = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
print(np.delete(a, np.s_[::2]))

#输出：
第一个数组：
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
未传递 Axis 参数。 在插入之前输入数组会被展开。
[ 0  1  2  3  4  6  7  8  9 10 11]
删除第二列：
[[ 0  2  3]
 [ 4  6  7]
 [ 8 10 11]]
包含从数组中删除的替代值的切片：
[ 2  4  6  8 10]
```

##### numpy.unique

numpy.unique 函数用于去除数组中的重复元素。

```
numpy.unique(arr, return_index, return_inverse, return_counts)
```

- `arr`：输入数组，如果不是一维数组则会展开



### NumPy 算术函数

NumPy 算术函数包含简单的加减乘除: **add()**，**subtract()**，**multiply()** 和 **divide()**。

需要注意的是数组必须具有相同的形状或符合数组广播规则。

```python
import numpy as np 
 
a = np.arange(9, dtype = np.float_).reshape(3,3)  
print ('第一个数组：')
print (a)

print ('第二个数组：')
b = np.array([10,10,10])  
print (b)

print ('两个数组相加：')
print (np.add(a,b))

print ('两个数组相减：')
print (np.subtract(a,b))

print ('两个数组相乘：')
print (np.multiply(a,b))

print ('两个数组相除：')
print (np.divide(a,b))

#输出：
第一个数组：
[[0. 1. 2.]
 [3. 4. 5.]
 [6. 7. 8.]]
第二个数组：
[10 10 10]
两个数组相加：
[[10. 11. 12.]
 [13. 14. 15.]
 [16. 17. 18.]]
两个数组相减：
[[-10.  -9.  -8.]
 [ -7.  -6.  -5.]
 [ -4.  -3.  -2.]]
两个数组相乘：
[[ 0. 10. 20.]
 [30. 40. 50.]
 [60. 70. 80.]]
两个数组相除：
[[0.  0.1 0.2]
 [0.3 0.4 0.5]
 [0.6 0.7 0.8]]
```

##### numpy.reciprocal()

numpy.reciprocal() 函数返回参数逐元素的倒数。如 **1/4** 倒数为 **4/1**。

```python
a = np.array([0.25, 1.33, 1, 100])
print('我们的数组是：')
print(a)

print('调用 reciprocal 函数：')
print(np.reciprocal(a))

#输出：
我们的数组是：
[  0.25   1.33   1.   100.  ]
调用 reciprocal 函数：
[4.        0.7518797 1.        0.01     ]
```

##### numpy.power()

numpy.power() 函数将第一个输入数组中的元素作为底数，计算它与第二个输入数组中相应元素的幂。

```python
a = np.array([10, 100, 1000])
print('我们的数组是；')
print(a)

print('调用 power 函数：')
print(np.power(a, 2))

print('第二个数组：')
b = np.array([1, 2, 3])
print(b)

print('再次调用 power 函数：')
print(np.power(a, b))

#输出：
我们的数组是；
[  10  100 1000]
调用 power 函数：
[    100   10000 1000000]
第二个数组：
[1 2 3]
再次调用 power 函数：
[        10      10000 1000000000]
```

##### numpy.cumsum()

cumsum的作用主要就是计算轴向的累加和。

最重要的参数就是axis

- axis没有值时，默认是一个一维数组进行加和
- np.cumsum(axis=0)，按行累加
- np.cumsum(axis=1)，按列累加

![image-20230816102927737](https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230816102927737.png)



### NumPy 统计函数

NumPy 提供了很多统计函数，用于从数组中查找最小元素，最大元素，百分位标准差和方差等。 函数说明如下：

#### numpy.amin() 和 numpy.amax()

numpy.amin() 用于计算数组中的元素沿指定轴的最小值。

numpy.amax() 用于计算数组中的元素沿指定轴的最大值。

```python
a = np.array([[3, 7, 5], [8, 4, 3], [2, 4, 9]])
print('我们的数组是：')
print(a)

print('调用 amin() 函数：')
print(np.amin(a, 1)) #0和1代表axis

print('再次调用 amin() 函数：')
print(np.amin(a, 0))

print('调用 amax() 函数：')
print(np.amax(a))

print('再次调用 amax() 函数：')
print(np.amax(a, axis=0))

#输出：
我们的数组是：
[[3 7 5]
 [8 4 3]
 [2 4 9]]
调用 amin() 函数：
[3 3 2]
再次调用 amin() 函数：
[2 4 3]
调用 amax() 函数：
9
再次调用 amax() 函数：
[8 7 9]
```

#### numpy.ptp()

numpy.ptp()函数计算数组中元素最大值与最小值的差（最大值 - 最小值）。

```python
a = np.array([[3, 7, 5], [8, 4, 3], [2, 4, 9]])
print('我们的数组是：')
print(a)

print('调用 ptp() 函数：')
print(np.ptp(a))

print('沿轴 1 调用 ptp() 函数：')
print(np.ptp(a, axis=1))

print('沿轴 0 调用 ptp() 函数：')
print(np.ptp(a, axis=0))

#输出：
我们的数组是：
[[3 7 5]
 [8 4 3]
 [2 4 9]]
调用 ptp() 函数：
7
沿轴 1 调用 ptp() 函数：
[4 5 7]
沿轴 0 调用 ptp() 函数：
[6 3 6]
```

#### numpy.median()

numpy.median() 函数用于计算数组 a 中元素的中位数（中值）

```python
a = np.array([[30, 65, 70], [80, 95, 10], [50, 90, 60]])
print('我们的数组是：')
print(a)

print('调用 median() 函数：')
print(np.median(a)) #整体的中位数

print('沿轴 0 调用 median() 函数：')
print(np.median(a, axis=0))

print('沿轴 1 调用 median() 函数：')
print(np.median(a, axis=1))

#输出：
我们的数组是：
[[30 65 70]
 [80 95 10]
 [50 90 60]]
调用 median() 函数：
65.0
沿轴 0 调用 median() 函数：
[50. 90. 60.]
沿轴 1 调用 median() 函数：
[65. 80. 60.]
```

#### numpy.mean()

numpy.mean() 函数返回数组中元素的算术平均值。 如果提供了轴，则沿其计算。

算术平均值是沿轴的元素的总和除以元素的数量。

```python
a = np.array([[1, 2, 3], [3, 4, 5], [4, 5, 6]])
print('我们的数组是：')
print(a)

print('调用 mean() 函数：')
print(np.mean(a))

print('沿轴 0 调用 mean() 函数：')
print(np.mean(a, axis=0))

print('沿轴 1 调用 mean() 函数：')
print(np.mean(a, axis=1))

#输出：
我们的数组是：
[[1 2 3]
 [3 4 5]
 [4 5 6]]
调用 mean() 函数：
3.6666666666666665
沿轴 0 调用 mean() 函数：
[2.66666667 3.66666667 4.66666667]
沿轴 1 调用 mean() 函数：
[2. 4. 5.]
```

#### numpy.average()

numpy.average() 函数根据在另一个数组中给出的各自的权重计算数组中元素的加权平均值。

该函数可以接受一个轴参数。 如果没有指定轴，则数组会被展开。

加权平均值即将各数值乘以相应的权数，然后加总求和得到总体值，再除以总的单位数。

考虑数组[1,2,3,4]和相应的权重[4,3,2,1]，通过将相应元素的乘积相加，并将和除以权重的和，来计算加权平均值

```python
a = np.array([1, 2, 3, 4])
print('我们的数组是：')
print(a)

print('调用 average() 函数：')
print(np.average(a)) #被展开后整体的平均值

# 不指定权重时相当于 mean 函数
wts = np.array([4, 3, 2, 1])
print('再次调用 average() 函数：')
print(np.average(a, weights=wts))

# 如果 returned 参数设为 true，则返回权重的和
print('权重的和：')
print(np.average([1, 2, 3, 4], weights=[4, 3, 2, 1], returned=True))

#输出：
我们的数组是：
[1 2 3 4]
调用 average() 函数：
2.5
再次调用 average() 函数：
2.0
权重的和：
(2.0, 10.0)
```

在多维数组中，可以指定用于计算的轴。

```python
a = np.arange(6).reshape(3, 2)
print('我们的数组是：')
print(a)

print('修改后的数组：')
wt = np.array([3, 5])
print(np.average(a, axis=1, weights=wt))

print('修改后的数组：')
print(np.average(a, axis=1, weights=wt, returned=True))

#输出：
我们的数组是：
[[0 1]
 [2 3]
 [4 5]]
修改后的数组：
[0.625 2.625 4.625]
修改后的数组：
(array([0.625, 2.625, 4.625]), array([8., 8., 8.]))
```

#### numpy.var方差

统计中的方差（样本方差）是每个样本值与全体样本值的平均数之差的平方值的平均数，即 mean((x - x.mean())** 2)。

```python
print (np.var([1,2,3,4]))

#输出：
1.25
```

#### numpy.std标准差

标准差是一组数据平均值分散程度的一种度量。

标准差是方差的算术平方根。

标准差公式如下：

```python
std = sqrt(mean((x - x.mean())**2))
```

```python
print (np.std([1,2,3,4]))

#输出：
1.1180339887498949
```



### NumPy 排序、条件筛选函数

#### numpy.sort()

numpy.sort() 函数返回输入数组的排序副本。函数格式如下：

```
numpy.sort(a, axis, kind, order)
```

参数说明：

- a: 要排序的数组
- axis: 沿着它排序数组的轴，如果没有数组会被展开，沿着最后的轴排序， axis=0 按列排序，axis=1 按行排序
- kind: 默认为'quicksort'（快速排序）
- order: 如果数组包含字段，则是要排序的字段

```python
a = np.array([[3, 7], [9, 1]])
print('我们的数组是：')
print(a)

print('调用 sort() 函数：')
print(np.sort(a))

print('按列排序：')
print(np.sort(a, axis=0))

# 在 sort 函数中排序字段
dt = np.dtype([('name', 'S10'), ('age', int)])
a = np.array([("raju", 21), ("anil", 25), ("ravi", 17), ("amar", 27)], dtype=dt)
print('我们的数组是：')
print(a)

print('按 name 排序：')
print(np.sort(a, order='name'))

#输出：
我们的数组是：
[[3 7]
 [9 1]]
调用 sort() 函数：
[[3 7]
 [1 9]]
按列排序：
[[3 1]
 [9 7]]
我们的数组是：
[(b'raju', 21) (b'anil', 25) (b'ravi', 17) (b'amar', 27)]
按 name 排序：
[(b'amar', 27) (b'anil', 25) (b'raju', 21) (b'ravi', 17)]
```



#### numpy.where()

numpy.where() 函数返回输入数组中满足给定条件的元素的索引

```python
x = np.arange(9.).reshape(3, 3)
print('我们的数组是：')
print(x)
print('大于 3 的元素的索引：')
y = np.where(x > 3)
print(y)
print('使用这些索引来获取满足条件的元素：')
print(x[y])

#输出：
我们的数组是：
[[0. 1. 2.]
 [3. 4. 5.]
 [6. 7. 8.]]
大于 3 的元素的索引：
(array([1, 1, 2, 2, 2], dtype=int64), array([1, 2, 0, 1, 2], dtype=int64))
使用这些索引来获取满足条件的元素：
[4. 5. 6. 7. 8.]
```



#### numpy.extract()

numpy.extract() 函数根据某个条件从数组中抽取元素，返回满条件的元素。

```python
x = np.arange(9.).reshape(3, 3)
print('我们的数组是：')
print(x)
# 定义条件, 选择偶数元素
condition = np.mod(x, 2) == 0
print('按元素的条件值：')
print(condition)
print('使用条件提取元素：')
print(np.extract(condition, x))

#输出：
我们的数组是：
[[0. 1. 2.]
 [3. 4. 5.]
 [6. 7. 8.]]
按元素的条件值：
[[ True False  True]
 [False  True False]
 [ True False  True]]
使用条件提取元素：
[0. 2. 4. 6. 8.]
```



### NumPy 线性代数 linalg

NumPy 提供了线性代数函数库 **linalg**，该库包含了线性代数所需的所有功能：

| 函数          | 描述                             |
| :------------ | :------------------------------- |
| `dot`         | 两个数组的点积，即元素对应相乘。 |
| `vdot`        | 两个向量的点积                   |
| `inner`       | 两个数组的内积                   |
| `matmul`      | 两个数组的矩阵积                 |
| `determinant` | 数组的行列式                     |
| `solve`       | 求解线性矩阵方程                 |
| `inv`         | 计算矩阵的乘法逆矩阵             |

#### numpy.dot()

numpy.dot() 

对于两个一维的数组，计算的是这两个数组**对应下标元素的乘积和(**数学上称之为向量点积)；

对于二维数组，计算的是两个数组的矩阵乘积；

对于多维数组，它的通用计算公式如下，即结果数组中的每个元素都是：数组a的最后一维上的所有元素与数组b的倒数第二位上的所有元素的乘积和： **dot(a, b)[i,j,k,m] = sum(a[i,j,:] \* b[k,:,m])**。

```
numpy.dot(a, b, out=None) 
```

**参数说明：**

- **a** : ndarray 数组
- **b** : ndarray 数组
- **out** : ndarray, 可选，用来保存dot()的计算结果

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([[11, 12], [13, 14]])
print(np.dot(a, b))

#输出：
[[37 40]
 [85 92]]
```

计算式：

```
[[1*11+2*13, 1*12+2*14],[3*11+4*13, 3*12+4*14]]
```



#### numpy.vdot()

numpy.vdot() 函数是两个向量的点积。 如果第一个参数是复数，那么它的共轭复数会用于计算。 如果参数是多维数组，它会被展开。

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([[11, 12], [13, 14]])
# vdot 将数组展开计算内积
print(np.vdot(a, b))

#输出：
130
```

计算式：

```
1*11 + 2*12 + 3*13 + 4*14 = 130
```



#### numpy.inner()

numpy.inner() 函数返回一维数组的向量内积。

```python
print(np.inner(np.array([1, 2, 3]), np.array([0, 1, 0])))
# 等价于 1*0+2*1+3*0

#输出：
2
```

对于更高的维度，它返回最后一个轴上的和的乘积。

```python
a = np.array([[1, 2], [3, 4]])

print('数组 a：')
print(a)
b = np.array([[11, 12], [13, 14]])

print('数组 b：')
print(b)

print('内积：')
print(np.inner(a, b))

#输出：
数组 a：
[[1 2]
 [3 4]]
数组 b：
[[11 12]
 [13 14]]
内积：
[[35 41]
 [81 95]]
```



#### numpy.linalg.det()

numpy.linalg.det() 函数计算输入矩阵的行列式。

行列式在线性代数中是非常有用的值。 它从方阵的对角元素计算。 对于 2×2 矩阵，它是左上和右下元素的乘积与其他两个的乘积的差。

换句话说，对于矩阵[[a，b]，[c，d]]，行列式计算为 ad-bc。 较大的方阵被认为是 2×2 矩阵的组合

```python
a = np.array([[1, 2], [3, 4]])
print(a)
print(np.linalg.det(a))

b = np.array([[6,1,1], [4, -2, 5], [2,8,7]])
print (b)
print (np.linalg.det(b))
print (6*(-2*7 - 5*8) - 1*(4*7 - 5*2) + 1*(4*8 - -2*2))

#输出：
[[1 2]
 [3 4]]
-2.0000000000000004
[[ 6  1  1]
 [ 4 -2  5]
 [ 2  8  7]]
-306.0
-306
```



### numpy.linalg.solve()

numpy.linalg.solve() 函数给出了矩阵形式的线性方程的解。

考虑以下线性方程：

```
x + y + z = 6

2y + 5z = -4

2x + 5y - z = 27
```

可以使用矩阵表示为：

![image-20230806132642142](https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230806132642142.png)



#### numpy.linalg.inv()

numpy.linalg.inv() 函数计算矩阵的乘法逆矩阵。

**逆矩阵（inverse matrix）**：设A是数域上的一个n阶矩阵，若在相同数域上存在另一个n阶矩阵B，使得： AB=BA=E ，则我们称B是A的逆矩阵，而A则被称为可逆矩阵。注：E为单位矩阵。

```python
x = np.array([[1, 2], [3, 4]])
y = np.linalg.inv(x)
print(x)
print(y)
print(np.dot(x, y))

#输出：
[[1 2]
 [3 4]]
[[-2.   1. ]
 [ 1.5 -0.5]]
[[1.0000000e+00 0.0000000e+00]
 [8.8817842e-16 1.0000000e+00]]
```



### NumPy Matplotlib

Matplotlib 是 Python 的绘图库。

```python
import numpy as np
from matplotlib import pyplot as plt

x = np.arange(1, 11)
y = 2 * x + 5
plt.title("Matplotlib demo")
plt.xlabel("x axis caption")
plt.ylabel("y axis caption")
plt.plot(x, y)
plt.show()
```



作为线性图的替代，可以通过向 plot() 函数添加格式字符串来显示离散值。 可以使用以下格式化字符。

| 字符   | 描述         |
| :----- | :----------- |
| `'-'`  | 实线样式     |
| `'--'` | 短横线样式   |
| `'-.'` | 点划线样式   |
| `':'`  | 虚线样式     |
| `'.'`  | 点标记       |
| `','`  | 像素标记     |
| `'o'`  | 圆标记       |
| `'v'`  | 倒三角标记   |
| `'^'`  | 正三角标记   |
| `'<'`  | 左三角标记   |
| `'>'`  | 右三角标记   |
| `'1'`  | 下箭头标记   |
| `'2'`  | 上箭头标记   |
| `'3'`  | 左箭头标记   |
| `'4'`  | 右箭头标记   |
| `'s'`  | 正方形标记   |
| `'p'`  | 五边形标记   |
| `'*'`  | 星形标记     |
| `'h'`  | 六边形标记 1 |
| `'H'`  | 六边形标记 2 |
| `'+'`  | 加号标记     |
| `'x'`  | X 标记       |
| `'D'`  | 菱形标记     |
| `'d'`  | 窄菱形标记   |
| `'|'`  | 竖直线标记   |
| `'_'`  | 水平线标记   |

以下是颜色的缩写：

| 字符  | 颜色   |
| :---- | :----- |
| `'b'` | 蓝色   |
| `'g'` | 绿色   |
| `'r'` | 红色   |
| `'c'` | 青色   |
| `'m'` | 品红色 |
| `'y'` | 黄色   |
| `'k'` | 黑色   |
| `'w'` | 白色   |

要显示圆来代表点，而不是上面示例中的线，请使用 ob 作为 plot() 函数中的格式字符串。

```python
import numpy as np 
from matplotlib import pyplot as plt 
 
x = np.arange(1,11) 
y =  2  * x +  5 
plt.title("Matplotlib demo") 
plt.xlabel("x axis caption") 
plt.ylabel("y axis caption") 
plt.plot(x,y,"ob") 
plt.show()
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230806133323832.png" alt="image-20230806133323832" style="zoom:50%;" />



#### subplot()

subplot() 函数允许你在同一图中绘制不同的东西。

以下实例绘制正弦和余弦值：

```python
import numpy as np 
import matplotlib.pyplot as plt 
# 计算正弦和余弦曲线上的点的 x 和 y 坐标 
x = np.arange(0,  3  * np.pi,  0.1) 
y_sin = np.sin(x) 
y_cos = np.cos(x)  
# 建立 subplot 网格，高为 2，宽为 1  
# 激活第一个 subplot
plt.subplot(2,  1,  1)  
# 绘制第一个图像 
plt.plot(x, y_sin) 
plt.title('Sine')  
# 将第二个 subplot 激活，并绘制第二个图像
plt.subplot(2,  1,  2) 
plt.plot(x, y_cos) 
plt.title('Cosine')  
# 展示图像
plt.show()
```



#### bar()

pyplot 子模块提供 bar() 函数来生成条形图。

以下实例生成两组 x 和 y 数组的条形图。

```python
from matplotlib import pyplot as plt 
x =  [5,8,10] 
y =  [12,16,6] 
x2 =  [6,9,11] 
y2 =  [6,15,7] 
plt.bar(x, y, align =  'center') 
plt.bar(x2, y2, color =  'g', align =  'center') 
plt.title('Bar graph') 
plt.ylabel('Y axis') 
plt.xlabel('X axis') 
plt.show()
```



<img src="C:\Users\34093\AppData\Roaming\Typora\typora-user-images\image-20230806133701401.png" alt="image-20230806133701401" style="zoom:50%;" />

#### numpy.histogram()

numpy.histogram() 函数是数据的频率分布的图形表示。 水平尺寸相等的矩形对应于类间隔，称为 bin，变量 height 对应于频率。

numpy.histogram()函数将输入数组和 bin 作为两个参数。 bin 数组中的连续元素用作每个 bin 的边界。



#### 保存图片plt.savefig

先新建一个目标文件夹，假设这里直接在程序运行的目录下新建了`img`文件夹

```python
i = 1
plt.savefig(f'./img/第{i}张图片')
```



#### 如果plot无法显示中文

我们可以使用系统的字体：

```python
from matplotlib import pyplot as plt
import matplotlib
a=sorted([f.name for f in matplotlib.font_manager.fontManager.ttflist])

for i in a:
    print(i)
```

*打印出你的 font_manager 的 ttflist 中所有注册的名字，找一个看中文字体例如：STFangsong(仿宋）,然后添加以下代码即可：*

```python
plt.rcParams['font.family']=['STFangsong']
```

测试一下：

```python
from matplotlib import pyplot as plt
import numpy as np

plt.rcParams['font.family']=['STFangsong']

x = np.arange(1, 11)
y = 2 * x + 5
plt.title("菜鸟教程 - 测试")
plt.xlabel("x 轴")
plt.ylabel("y 轴")
plt.plot(x, y)
plt.show()
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230806134448987.png" alt="image-20230806134448987" style="zoom:50%;" />

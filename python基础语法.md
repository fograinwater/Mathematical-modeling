### python基础语法

#### 注释

```python
# 单行注释
```

```python
'''
单引号的多行注释
'''
```

```python
"""
双引号的多行注释
"""
```

#### 多行语句

python通常需要在一行中写完一条语句，如果语句太长，可用反斜杠 `\` 来实现单行语句的多行书写，例如：

```python
x = "这条语句很长11111111111111111" + \
	"2222222222222" + \
	"3333333333333"

y = 1 + 2 + 3 + 4 + 5 \
    +6 + 7 + 8
```

但是在 [], {}, 或 () 中的多行语句，不需要使用反斜杠 `\`，例如：

```python
str = {"111",
      "222",
      "333"}
```



### print 输出

**print** 默认输出是换行的，如果要实现不换行需要在变量末尾加上 **end=""**，例如：

```python
s1 = "abc"
s2 = "123"
print(s1, end="")
print(s2)

#输出：abc123
```

使用 repr() 或 str() 将输出的值转成字符串

- **str()：** 函数返回一个用户易读的表达形式。
- **repr()：** 产生一个解释器易读的表达形式。

##### str.format() 进行格式输出

{}括号及其里面的字符 (称作格式化字段) 将会被 format() 中的参数替换。

```python
>>> print('今天{}： "{}!"'.format('心情', '\(^o^)/~'))

# 输出：
今天心情： "\(^o^)/~!"
```

在括号中的数字用于指向传入对象在 format() 中的位置

```python
>>> print('{0} 和 {1}'.format('Google', 'Runoob'))
Google 和 Runoob
>>> print('{1} 和 {0}'.format('Google', 'Runoob'))
Runoob 和 Google
```

如果在 format() 中使用了关键字参数, 那么它们的值会指向使用该名字的参数。

```python
>>> print('今天{what}： {how}'.format(what='心情', how='\(^o^)/~!'))

# 输出：
今天心情： "\(^o^)/~!"
```

位置及关键字参数可以任意的结合:

```python
>>> print('站点列表 {0}, {1}, 和 {other}。'.format('Google', 'Runoob', other='Taobao'))
站点列表 Google, Runoob, 和 Taobao。
```

可选项 **:** 和格式标识符可以跟着字段名。 这就允许对值进行更好的格式化。 下面的例子将 Pi 保留到小数点后三位：

```python
>>> import math
>>> print('常量 PI 的值近似为 {0:.3f}。'.format(math.pi))
常量 PI 的值近似为 3.142。
```

在 **:** 后传入一个整数, 可以保证该域至少有这么多的宽度。 用于美化表格时很有用。

```python
>>> table = {'Google': 1, 'Runoob': 2, 'Taobao': 3}
>>> for name, number in table.items():
...     print('{0:10} ==> {1:10d}'.format(name, number))
... 
Google     ==>          1
Runoob     ==>          2
Taobao     ==>          3
```



### 基本数据类型

Python 中的变量不需要声明，但每个**变量在使用前都必须赋值**，变量赋值以后该变量才会被创建。

在 Python 中，变量就是变量，它没有类型，我们所说的**"类型"是变量所指的内存中对象的类型**。因此一个变量可以通过赋值指向不同类型的对象。

- 使用` type() `**查询变量所指的对象类型**

```python
>>> a, b, c, d = 20, 5.5, True, 4+3j
>>> print(type(a), type(b), type(c), type(d))
#输出：
<class 'int'> <class 'float'> <class 'bool'> <class 'complex'>
```



#### 标准数据类型

- **不可变数据（3 个）：**Number（数字）、String（字符串）、Tuple（元组）；
- **可变数据（3 个）：**List（列表）、Dictionary（字典）、Set（集合）。

#### 多个变量赋值

可同时为多个变量赋相同的值。例如：

```python
a = b = c = 1
```

也可以为多个对象指定多个变量。例如：

```python
a, b, c = 1, 2, "runoob"
```



#### 数据类型转换

只需要将数据类型作为函数名即可。

| 函数                                                         | 描述                                                |
| :----------------------------------------------------------- | :-------------------------------------------------- |
| int(x [,base\])](https://www.runoob.com/python3/python-func-int.html) | 将x转换为一个整数                                   |
| [float(x)](https://www.runoob.com/python3/python-func-float.html) | 将x转换到一个浮点数                                 |
| complex(real [,imag\])](https://www.runoob.com/python3/python-func-complex.html) | 创建一个复数                                        |
| [str(x)](https://www.runoob.com/python3/python-func-str.html) | 将对象 x 转换为字符串                               |
| [repr(x)](https://www.runoob.com/python3/python-func-repr.html) | 将对象 x 转换为表达式字符串                         |
| [eval(str)](https://www.runoob.com/python3/python-func-eval.html) | 用来计算在字符串中的有效Python表达式,并返回一个对象 |
| [tuple(s)](https://www.runoob.com/python3/python3-func-tuple.html) | 将序列 s 转换为一个元组                             |
| [list(s)](https://www.runoob.com/python3/python3-att-list-list.html) | 将序列 s 转换为一个列表                             |
| [set(s)](https://www.runoob.com/python3/python-func-set.html) | 转换为可变集合                                      |
| [dict(d)](https://www.runoob.com/python3/python-func-dict.html) | 创建一个字典。d 必须是一个 (key, value)元组序列。   |
| [frozenset(s)](https://www.runoob.com/python3/python-func-frozenset.html) | 转换为不可变集合                                    |
| [chr(x)](https://www.runoob.com/python3/python-func-chr.html) | 将一个整数转换为一个字符                            |
| [ord(x)](https://www.runoob.com/python3/python-func-ord.html) | 将一个字符转换为它的整数值                          |
| [hex(x)](https://www.runoob.com/python3/python-func-hex.html) | 将一个整数转换为一个十六进制字符串                  |
| [oct(x)](https://www.runoob.com/python3/python-func-oct.html) | 将一个整数转换为一个八进制字符串                    |



#### Number（数字）

python中数字有四种类型：整数、布尔型、浮点数和复数。

- **int** (整数), 如 1, 只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。
- **bool** (布尔)：True、False。
  - Python3 中，bool 是 int 的子类，在比较 和 运算时，Python 会将 **True 视为 1，False 视为 0**。因此True 和 False 可以和数字相加， True == 1、False==0 会返回 True。
  - 所有**非零**的数字和**非空**的字符串、列表、元组等数据类型都被视为 **True**，只有 **0、空字符串、空列表、空元组**等被视为 **False**。
- **float** (浮点数), 如 1.23、3E-2。布尔类型可以和逻辑运算符一起使用，包括 and、or 和 not。
- **complex** (复数), 如 1 + 2j、 1.1 + 2.2j。由实数和虚数部分构成，可以用 **a + bj**，或者 **complex(a,b)** 表示，**a** 和 **b** 都是浮点型。



##### 数学函数

| 函数                                                         | 返回值 ( 描述 )                                              |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [abs(x)](https://www.runoob.com/python3/python3-func-number-abs.html) | 返回数字的绝对值，如abs(-10) 返回 10                         |
| [ceil(x)](https://www.runoob.com/python3/python3-func-number-ceil.html) | 返回数字的上入整数，如math.ceil(4.1) 返回 5                  |
| cmp(x, y)                                                    | 如果 x < y 返回 -1, 如果 x == y 返回 0, 如果 x > y 返回 1。 **Python 3 已废弃，使用 (x>y)-(x<y) 替换**。 |
| [exp(x)](https://www.runoob.com/python3/python3-func-number-exp.html) | 返回e的x次幂(ex),如math.exp(1) 返回2.718281828459045         |
| [fabs(x)](https://www.runoob.com/python3/python3-func-number-fabs.html) | 以浮点数形式返回数字的绝对值，如math.fabs(-10) 返回10.0      |
| [floor(x)](https://www.runoob.com/python3/python3-func-number-floor.html) | 返回数字的下舍整数，如math.floor(4.9)返回 4                  |
| [log(x)](https://www.runoob.com/python3/python3-func-number-log.html) | 如math.log(math.e)返回1.0,math.log(100,10)返回2.0            |
| [log10(x)](https://www.runoob.com/python3/python3-func-number-log10.html) | 返回以10为基数的x的对数，如math.log10(100)返回 2.0           |
| [max(x1, x2,...)](https://www.runoob.com/python3/python3-func-number-max.html) | 返回给定参数的最大值，参数可以为序列。                       |
| [min(x1, x2,...)](https://www.runoob.com/python3/python3-func-number-min.html) | 返回给定参数的最小值，参数可以为序列。                       |
| [modf(x)](https://www.runoob.com/python3/python3-func-number-modf.html) | 返回x的整数部分与小数部分，两部分的数值符号与x相同，整数部分以浮点型表示。 |
| [pow(x, y)](https://www.runoob.com/python3/python3-func-number-pow.html) | x**y 运算后的值。                                            |
| [round(x [,n\])](https://www.runoob.com/python3/python3-func-number-round.html) | 返回浮点数 x 的四舍五入值，如给出 n 值，则代表舍入到小数点后的位数。**其实准确的说是保留值将保留到离上一位更近的一端。** |
| [sqrt(x)](https://www.runoob.com/python3/python3-func-number-sqrt.html) | 返回数字x的平方根。                                          |



##### 随机数函数

| 函数                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [choice(seq)](https://www.runoob.com/python3/python3-func-number-choice.html) | 从序列的元素中随机挑选一个元素，比如random.choice(range(10))，从0到9中随机挑选一个整数。 |
| [randrange ([start,\] stop [,step])](https://www.runoob.com/python3/python3-func-number-randrange.html) | 从指定范围内，按指定基数递增的集合中获取一个随机数，基数默认值为 1 |
| [random()](https://www.runoob.com/python3/python3-func-number-random.html) | 随机生成下一个实数，它在[0,1)范围内。                        |
| seed([x\])](https://www.runoob.com/python3/python3-func-number-seed.html) | 改变随机数生成器的种子seed。如果你不了解其原理，你不必特别去设定seed，Python会帮你选择seed。 |
| [shuffle(lst)](https://www.runoob.com/python3/python3-func-number-shuffle.html) | 将序列的所有元素随机排序                                     |
| [uniform(x, y)](https://www.runoob.com/python3/python3-func-number-uniform.html) | 随机生成下一个实数，它在[x,y]范围内。                        |



##### 三角函数

| 函数                                                         | 描述                                              |
| :----------------------------------------------------------- | :------------------------------------------------ |
| [acos(x)](https://www.runoob.com/python3/python3-func-number-acos.html) | 返回x的反余弦弧度值。                             |
| [asin(x)](https://www.runoob.com/python3/python3-func-number-asin.html) | 返回x的反正弦弧度值。                             |
| [atan(x)](https://www.runoob.com/python3/python3-func-number-atan.html) | 返回x的反正切弧度值。                             |
| [atan2(y, x)](https://www.runoob.com/python3/python3-func-number-atan2.html) | 返回给定的 X 及 Y 坐标值的反正切值。              |
| [cos(x)](https://www.runoob.com/python3/python3-func-number-cos.html) | 返回x的弧度的余弦值。                             |
| [hypot(x, y)](https://www.runoob.com/python3/python3-func-number-hypot.html) | 返回欧几里德范数 sqrt(x*x + y*y)。                |
| [sin(x)](https://www.runoob.com/python3/python3-func-number-sin.html) | 返回的x弧度的正弦值。                             |
| [tan(x)](https://www.runoob.com/python3/python3-func-number-tan.html) | 返回x弧度的正切值。                               |
| [degrees(x)](https://www.runoob.com/python3/python3-func-number-degrees.html) | 将弧度转换为角度,如degrees(math.pi/2) ， 返回90.0 |
| [radians(x)](https://www.runoob.com/python3/python3-func-number-radians.html) | 将角度转换为弧度                                  |



##### 数学常量

| 常量 | 描述                                 |
| :--- | :----------------------------------- |
| pi   | 数学常量 pi（圆周率，一般以π来表示） |
| e    | 数学常量 e，e即自然常数（自然常数）  |

```python
import math
print(math.pi)
print(math.e)

#输出：
3.141592653589793
2.718281828459045
```



#### String（字符串）

- 单引号 **'** 和双引号 **"** 使用完全相同。

- 使用三引号(**'''** 或 **"""**)可以指定一个多行字符串。

  ```python
  s = """ xy
      123
      abc
  456  def
  """
  
  # 输出：print(s)
   xy
      123
      abc
  456  def
  ```

- Python 中的字符串不能改变。因此向一个索引位置赋值，比如 **word[0] = 'm'** 会导致错误

- 转义符 `\`。反斜杠可以用来转义，使用 **r** 可以让反斜杠不发生转义(r 指 raw string)。 如 **r"this is a line with \n"** 则 **\n** 会显示，并不是换行。

  ```python
  print('\n')       # 输出空行
  print(r'\n')      # 输出 \n
  ```

- 字符串可以用 **+** 运算符连接在一起，用 ***** 运算符重复。

  ```python
  s = "abc" * 3              #输出s = "abcabcabc" 
  ```

- Python 中的字符串有两种索引方式，从左往右以 **0** 开始，从右往左以 **-1** 开始。

- 字符串的截取的语法格式如下：**变量[头下标:尾下标:步长]**   **（注：区间是左闭右开）**

  ```python
  str='123456789'
   
  print(str)                 # 输出字符串:123456789
  print(str[0])              # 输出字符串第一个字符:1
  print(str[0:-1])           # 输出第一个到倒数第二个的所有字符:12345678
  print(str[2:5])            # 输出从第三个开始到第六个的字符（不包含）：345
  print(str[2:])             # 输出从第三个开始后的所有字符：3456789
  print(str[1:5:2])          # 输出从第二个开始到第五个且每隔一个的字符（步长为2）:24
  print(str * 2)             # 输出字符串两次:123456789123456789
  ```

- 单个字符也是一个字符串。使用**`ord()`函数**可以获取字符对应的整数值。

  ```python
  x = ord("A")
  print(x)
  
  #输出：
  65
  ```

##### 转义字符

| 转义字符       | 描述                                                         | 实例                                                         |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| \ (放在行尾时) | 续行符                                                       | `>>> print("line1 \ ... line2 \ ... line3") line1 line2 line3 >>> ` |
| \ \            | 反斜杠符号                                                   | `>>> print("\\") \`                                          |
| \'             | 单引号                                                       | `>>> print('\'') '`                                          |
| \"             | 双引号                                                       | `>>> print("\"") "`                                          |
| \a             | 响铃                                                         | `>>> print("\a")`执行后电脑有响声。                          |
| \b             | 退格(Backspace)                                              | `>>> print("Hello \b World!") Hello World!`                  |
| \000           | 空                                                           | `>>> print("\000") >>> `                                     |
| \n             | 换行                                                         | `>>> print("\n")  >>>`                                       |
| \v             | 纵向制表符                                                   | `>>> print("Hello \v World!") Hello        World! >>>`       |
| \t             | 横向制表符                                                   | `>>> print("Hello \t World!") Hello    World! >>>`           |
| \r             | 回车，将 **\r** 后面的内容移到字符串开头，并逐一替换开头部分的字符，直至将 **\r** 后面的内容完全替换完成。 | `>>> print("Hello\rWorld!") World! >>> print('google runoob taobao\r123456') 123456 runoob taobao` |
| \f             | 换页                                                         | `>>> print("Hello \f World!") Hello        World! >>> `      |
| \yyy           | 八进制数，y 代表 0~7 的字符，例如：\012 代表换行。           | `>>> print("\110\145\154\154\157\40\127\157\162\154\144\41") Hello World!` |
| \xyy           | 十六进制数，以 \x 开头，y 代表的字符，例如：\x0a 代表换行    | `>>> print("\x48\x65\x6c\x6c\x6f\x20\x57\x6f\x72\x6c\x64\x21") Hello World!` |



使用 **\r** 实现百分比精度：

```python
print("第一行")
print("\000")
print("第二行")

#输出：
第一行
 
第二行
```



#### Tuple（元组）

- 元组与列表类似，但是元组的元素不能修改。元组写在小括号 **()** 里，元素之间用逗号隔开。元组中的元素类型可以不相同。
- 元组可以被索引和截取（下标索引从0开始，-1 为从末尾开始的位置）。

```python
tuple = ( 'abcd', 786 , 2.23, 'runoob', 70.2 )
tinytuple = (123, 'runoob')

print(tuple)       			# 输出完整元组
print(tuple[0])      		# 输出元组的第一个元素
print(tuple[1:3])     		# 输出从第二个元素开始到第三个元素
print(tuple[2:])     		# 输出从第三个元素开始的所有元素
print(tinytuple * 2)   		# 输出两次元组
print(tuple + tinytuple) 	# 连接元组

#输出：
('abcd', 786, 2.23, 'runoob', 70.2)
abcd
(786, 2.23)
(2.23, 'runoob', 70.2)
(123, 'runoob', 123, 'runoob')
('abcd', 786, 2.23, 'runoob', 70.2, 123, 'runoob')
```

```python
>>> tup[0] = 11 # 修改元组元素的操作是非法的
Traceback (most recent call last):
 File "<stdin>", line 1, **in** <module>
TypeError: 'tuple' object does **not** support item assignment
```

- 构造包含 0 个或 1 个元素的元组比较特殊，所以有一些额外的语法规则：

  ```python
  tup1 = ()    # 空元组
  tup2 = (20,) # 一个元素，需要在元素后添加逗号
  ```

##### 元组内置函数

| 序号 | 方法及描述                               | 实例                                                         |
| :--- | :--------------------------------------- | :----------------------------------------------------------- |
| 1    | len(tuple) 计算元组元素个数。            | `>>> tuple1 = ('Google', 'Runoob', 'Taobao') >>> len(tuple1) 3 >>> ` |
| 2    | max(tuple) 返回元组中元素最大值。        | `>>> tuple2 = ('5', '4', '8') >>> max(tuple2) '8' >>> `      |
| 3    | min(tuple) 返回元组中元素最小值。        | `>>> tuple2 = ('5', '4', '8') >>> min(tuple2) '4' >>> `      |
| 4    | tuple(iterable) 将可迭代系列转换为元组。 | `>>> list1= ['Google', 'Taobao', 'Runoob', 'Baidu'] >>> tuple1=tuple(list1) >>> tuple1 ('Google', 'Taobao', 'Runoob', 'Baidu')` |



#### List（列表）

- List（列表）通常用于实现集合类的数据结构。
- List是写在方括号 **[]** 之间、用逗号分隔开的元素列表。
- 列表中元素的类型可以不相同。

- 列表的**索引和截取（**索引值以 **0** 为开始值，**-1** 为从末尾的开始位置，如果步长为负数表示逆向读取，不指定步长则默认为1）

  ```python
  变量[头下标:尾下标:步长]
  ```

  ```python
  list = [ 'abcd', 786 , 2.23, 'runoob', 70.2 ]
  tinylist = [123, 'runoob']
  
  print (list)            # 输出完整列表
  print (list[0])         # 输出列表第一个元素
  print (list[1:3])       # 从第二个开始输出到第三个元素
  print (list[2:])        # 输出从第三个元素开始的所有元素
  print (tinylist * 2)    # 输出两次列表
  print (list + tinylist) # 连接列表
  
  #输出：
  ['abcd', 786, 2.23, 'runoob', 70.2]
  abcd
  [786, 2.23]
  [2.23, 'runoob', 70.2]
  [123, 'runoob', 123, 'runoob']
  ['abcd', 786, 2.23, 'runoob', 70.2, 123, 'runoob']
  ```

- **改变列表中的元素**

  ```python
  #改变单个元素
  >>> a = [1, 2, 3, 4, 5, 6]
  >>> a[0] = 9
  >>> a
  [9, 2, 3, 4, 5, 6]
  
  #改变连续几个元素
  >>> a[2:5] = [13, 14, 15]
  >>> a
  [9, 2, 13, 14, 15, 6]
  
  #删除部分元素
  >>> a[2:5] = []   # 将对应的元素值设置为 [] 
  >>> a
  [9, 2, 6]
  ```

- string、list 和 tuple 都属于 sequence（序列）。



##### 列表函数&方法

Python包含以下函数:

| 序号 | 函数                                                         |
| :--- | :----------------------------------------------------------- |
| 1    | [len(list)](https://www.runoob.com/python3/python3-att-list-len.html) 列表元素个数 |
| 2    | [max(list)](https://www.runoob.com/python3/python3-att-list-max.html) 返回列表元素最大值 |
| 3    | [min(list)](https://www.runoob.com/python3/python3-att-list-min.html) 返回列表元素最小值 |
| 4    | [list(seq)](https://www.runoob.com/python3/python3-att-list-list.html) 将元组转换为列表 |

Python包含以下方法:

| 序号 | 方法                                                         |
| :--- | :----------------------------------------------------------- |
| 1    | [list.append(obj)](https://www.runoob.com/python3/python3-att-list-append.html) 在列表末尾添加新的对象 |
| 2    | [list.count(obj)](https://www.runoob.com/python3/python3-att-list-count.html) 统计某个元素在列表中出现的次数 |
| 3    | [list.extend(seq)](https://www.runoob.com/python3/python3-att-list-extend.html) 在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表） |
| 4    | [list.index(obj)](https://www.runoob.com/python3/python3-att-list-index.html) 从列表中找出某个值第一个匹配项的索引位置 |
| 5    | [list.insert(index, obj)](https://www.runoob.com/python3/python3-att-list-insert.html) 将对象插入列表 |
| 6    | list.pop([index=-1\])](https://www.runoob.com/python3/python3-att-list-pop.html) 移除列表中的一个元素（默认最后一个元素），并且返回该元素的值 |
| 7    | [list.remove(obj)](https://www.runoob.com/python3/python3-att-list-remove.html) 移除列表中某个值的第一个匹配项 |
| 8    | [list.reverse()](https://www.runoob.com/python3/python3-att-list-reverse.html) 反向列表中元素 |
| 9    | [list.sort( key=None, reverse=False)](https://www.runoob.com/python3/python3-att-list-sort.html) 对原列表进行排序 |
| 10   | [list.clear()](https://www.runoob.com/python3/python3-att-list-clear.html) 清空列表 |
| 11   | [list.copy()](https://www.runoob.com/python3/python3-att-list-copy.html) 复制列表 |



#### Set（集合）

- 集合（Set）是一种**无序、可变**的数据类型，集合中的元素**不会重复**。
- 可以进行交集、并集、差集等常见的集合操作。
- 集合用大括号 **{}** 表示，也可以使用 **set()** 函数创建集合。元素之间用逗号 **,** 分隔。

**注意：**创建一个空集合必须用 **set()** 而不是 **{ }**，因为 **{ }** 是用来创建一个空字典。

```python
sites = {'Google', 'Taobao', 'Runoob', 'Facebook', 'Zhihu', 'Baidu'}

print(sites)  # 输出集合，重复的元素被自动去掉

# 成员测试
if 'Runoob' in sites :
  print('Runoob 在集合中')
else :
  print('Runoob 不在集合中')

# set可以进行集合运算
a = set('abracadabra')
b = set('alacazam')

print(a)
print(a - b)   # a 和 b 的差集
print(a | b)   # a 和 b 的并集
print(a & b)   # a 和 b 的交集
print(a ^ b)   # a 和 b 中不同时存在的元素

#输出：
{'Zhihu', 'Baidu', 'Taobao', 'Runoob', 'Google', 'Facebook'}
Runoob 在集合中
{'b', 'c', 'a', 'r', 'd'}
{'r', 'b', 'd'}
{'b', 'c', 'a', 'z', 'm', 'r', 'l', 'd'}
{'c', 'a'}
{'z', 'b', 'm', 'r', 'l', 'd'}
```

##### 集合内置方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [add()](https://www.runoob.com/python3/ref-set-add.html)     | 为集合添加元素                                               |
| [clear()](https://www.runoob.com/python3/ref-set-clear.html) | 移除集合中的所有元素                                         |
| [copy()](https://www.runoob.com/python3/ref-set-copy.html)   | 拷贝一个集合                                                 |
| [difference()](https://www.runoob.com/python3/ref-set-difference.html) | 返回多个集合的差集                                           |
| [difference_update()](https://www.runoob.com/python3/ref-set-difference_update.html) | 移除集合中的元素，该元素在指定的集合也存在。                 |
| [discard()](https://www.runoob.com/python3/ref-set-discard.html) | 删除集合中指定的元素                                         |
| [intersection()](https://www.runoob.com/python3/ref-set-intersection.html) | 返回集合的交集                                               |
| [intersection_update()](https://www.runoob.com/python3/ref-set-intersection_update.html) | 返回集合的交集。                                             |
| [isdisjoint()](https://www.runoob.com/python3/ref-set-isdisjoint.html) | 判断两个集合是否包含相同的元素，如果没有返回 True，否则返回 False。 |
| [issubset()](https://www.runoob.com/python3/ref-set-issubset.html) | 判断指定集合是否为该方法参数集合的子集。                     |
| [issuperset()](https://www.runoob.com/python3/ref-set-issuperset.html) | 判断该方法的参数集合是否为指定集合的子集                     |
| [pop()](https://www.runoob.com/python3/ref-set-pop.html)     | 随机移除元素                                                 |
| [remove()](https://www.runoob.com/python3/ref-set-remove.html) | 移除指定元素                                                 |
| [symmetric_difference()](https://www.runoob.com/python3/ref-set-symmetric_difference.html) | 返回两个集合中不重复的元素集合。                             |
| [symmetric_difference_update()](https://www.runoob.com/python3/ref-set-symmetric_difference_update.html) | 移除当前集合中在另外一个指定集合相同的元素，并将另外一个指定集合中不同的元素插入到当前集合中。 |
| [union()](https://www.runoob.com/python3/ref-set-union.html) | 返回两个集合的并集                                           |
| [update()](https://www.runoob.com/python3/ref-set-update.html) | 给集合添加元素                                               |



#### Dictionary（字典）

- 字典是无序的对象集合，列表是有序的对象集合。【因为字典当中的元素是通过键来存取的，而不是通过偏移存取】。

- 字典是一种映射类型，字典用 **{ }** 标识，它是一个无序的 **键(key) : 值(value)** 的集合。键(key)必须使用不可变类型，且在同一个字典中，键(key)必须是唯一的。

  ```python
  dict = {}
  dict['one'] = "香蕉"
  dict[2] = "苹果"
  
  tinydict = {'name': 'runoob','code':1, 'site': 'www.runoob.com'}
  
  print (dict['one'])       # 输出键为 'one' 的值
  print (dict[2])           # 输出键为 2 的值
  print (tinydict)          # 输出完整的字典
  print (tinydict.keys())   # 输出所有键
  print (tinydict.values()) # 输出所有值
  
  #输出：
  香蕉
  苹果
  {'name': 'runoob', 'code': 1, 'site': 'www.runoob.com'}
  dict_keys(['name', 'code', 'site'])
  dict_values(['runoob', 1, 'www.runoob.com'])
  ```

- 也可以使用`dict()`构造函数创建字典：

  ```python
  >>> dict([('Runoob', 1), ('Google', 2), ('Taobao', 3)])
  {'Runoob': 1, 'Google': 2, 'Taobao': 3}
  
  >>> dict(Runoob=1, Google=2, Taobao=3)
  {'Runoob': 1, 'Google': 2, 'Taobao': 3}
  
  >>> {x: x**2 for x in (2, 4, 6)}
  {2: 4, 4: 16, 6: 36}
  ```

##### 字典函数&方法

Python字典包含了以下内置函数：

| 序号 | 函数及描述                                                   | 实例                                                         |
| :--- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 1    | len(dict) 计算字典元素个数，即键的总数。                     | `>>> tinydict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'} >>> len(tinydict) 3` |
| 2    | str(dict) 输出字典，可以打印的字符串表示。                   | `>>> tinydict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'} >>> str(tinydict) "{'Name': 'Runoob', 'Class': 'First', 'Age': 7}"` |
| 3    | type(variable) 返回输入的变量类型，如果变量是字典就返回字典类型。 | `>>> tinydict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'} >>> type(tinydict) <class 'dict'>` |

Python字典包含了以下内置方法：

| 序号 | 函数及描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | [dict.clear()](https://www.runoob.com/python3/python3-att-dictionary-clear.html) 删除字典内所有元素 |
| 2    | [dict.copy()](https://www.runoob.com/python3/python3-att-dictionary-copy.html) 返回一个字典的浅复制 |
| 3    | [dict.fromkeys()](https://www.runoob.com/python3/python3-att-dictionary-fromkeys.html) 创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值 |
| 4    | [dict.get(key, default=None)](https://www.runoob.com/python3/python3-att-dictionary-get.html) 返回指定键的值，如果键不在字典中返回 default 设置的默认值 |
| 5    | [key in dict](https://www.runoob.com/python3/python3-att-dictionary-in.html) 如果键在字典dict里返回true，否则返回false |
| 6    | [dict.items()](https://www.runoob.com/python3/python3-att-dictionary-items.html) 以列表返回一个视图对象 |
| 7    | [dict.keys()](https://www.runoob.com/python3/python3-att-dictionary-keys.html) 返回一个视图对象 |
| 8    | [dict.setdefault(key, default=None)](https://www.runoob.com/python3/python3-att-dictionary-setdefault.html) 和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default |
| 9    | [dict.update(dict2)](https://www.runoob.com/python3/python3-att-dictionary-update.html) 把字典dict2的键/值对更新到dict里 |
| 10   | [dict.values()](https://www.runoob.com/python3/python3-att-dictionary-values.html) 返回一个视图对象 |
| 11   | pop(key[,default\])](https://www.runoob.com/python3/python3-att-dictionary-pop.html) 删除字典 key（键）所对应的值，返回被删除的值。 |
| 12   | [popitem()](https://www.runoob.com/python3/python3-att-dictionary-popitem.html) 返回并删除字典中的最后一对键和值。 |



### 运算

- 数值的除法包含两个运算符：**/** 返回一个浮点数，**//** 返回一个整数。
- 在混合计算时，Python会把整型转换成为浮点数。

#### 算术运算

以下假设变量 **a=10**，变量 **b=21**：

| 运算符 | 描述                                            | 实例                        |
| :----- | :---------------------------------------------- | :-------------------------- |
| +      | 加 - 两个对象相加                               | a + b 输出结果 31           |
| -      | 减 - 得到负数或是一个数减去另一个数             | a - b 输出结果 -11          |
| *      | 乘 - 两个数相乘或是返回一个被重复若干次的字符串 | a * b 输出结果 210          |
| /      | 除 - x 除以 y                                   | b / a 输出结果 2.1          |
| %      | 取模 - 返回除法的余数                           | b % a 输出结果 1            |
| **     | 幂 - 返回x的y次幂                               | a**b 为10的21次方           |
| //     | 取整除 - 往小的方向取整数                       | 9//2 = 4  <br />-9//2  = -5 |

#### 赋值运算

以下假设变量**a=10**，变量**b=20**：

| 运算符 |                             描述                             | 实例                                                         |
| :----: | :----------------------------------------------------------: | :----------------------------------------------------------- |
|   =    |                       简单的赋值运算符                       | c = a + b 将 a + b 的运算结果赋值为 c                        |
|   +=   |                        加法赋值运算符                        | c += a 等效于 c = c + a                                      |
|   -=   |                        减法赋值运算符                        | c -= a 等效于 c = c - a                                      |
|   *=   |                        乘法赋值运算符                        | c *= a 等效于 c = c * a                                      |
|   /=   |                        除法赋值运算符                        | c /= a 等效于 c = c / a                                      |
|   %=   |                        取模赋值运算符                        | c %= a 等效于 c = c % a                                      |
|  **=   |                         幂赋值运算符                         | c ** = a 等效于 c = c ** a                                   |
|  //=   |                       取整除赋值运算符                       | c //= a 等效于 c = c // a                                    |
|   :=   | 海象运算符，可在表达式内部为变量赋值。**Python3.8 版本新增运算符**。 | 在这个示例中，赋值表达式可以避免调用 len() 两次:<br />`if (n := len(a)) > 10:    print(f"List is too long ({n} elements, expected <= 10)")` |

#### 逻辑运算

以下假设变量 a 为 10, b为 20:

| 运算符 | 逻辑表达式 | 描述                                                         | 实例                    |
| :----- | :--------- | :----------------------------------------------------------- | :---------------------- |
| and    | x and y    | 布尔"与" - 如果 x 为 False，x and y 返回 x 的值，否则返回 y 的计算值。 | (a and b) 返回 20。     |
| or     | x or y     | 布尔"或" - 如果 x 是 True，它返回 x 的值，否则它返回 y 的计算值。 | (a or b) 返回 10。      |
| not    | not x      | 布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。 | not(a and b) 返回 False |

#### 成员运算

包括字符串，列表或元组。

| 运算符 | 描述                                                    | 实例                                              |
| :----- | :------------------------------------------------------ | :------------------------------------------------ |
| in     | 如果在指定的序列中找到值返回 True，否则返回 False。     | x 在 y 序列中 , 如果 x 在 y 序列中返回 True。     |
| not in | 如果在指定的序列中没有找到值返回 True，否则返回 False。 | x 不在 y 序列中 , 如果 x 不在 y 序列中返回 True。 |

以下实例演示了Python所有成员运算符的操作：

```python
a = 10
b = 20
list = [1, 2, 3, 4, 5 ]
 
if ( a in list ):
   print ("1 - 变量 a 在给定的列表中 list 中")
else:
   print ("1 - 变量 a 不在给定的列表中 list 中")
 
if ( b not in list ):
   print ("2 - 变量 b 不在给定的列表中 list 中")
else:
   print ("2 - 变量 b 在给定的列表中 list 中")
 
# 修改变量 a 的值
a = 2
if ( a in list ):
   print ("3 - 变量 a 在给定的列表中 list 中")
else:
   print ("3 - 变量 a 不在给定的列表中 list 中")

#输出：
1 - 变量 a 不在给定的列表中 list 中
2 - 变量 b 不在给定的列表中 list 中
3 - 变量 a 在给定的列表中 list 中
```

#### 身份运算

身份运算符用于比较两个对象的存储单元是否相同。

| 运算符 | 描述                                        | 实例                                                         |
| :----- | :------------------------------------------ | :----------------------------------------------------------- |
| is     | is 是判断两个标识符是不是引用自一个对象     | **x is y**, 类似 **id(x) == id(y)** , 如果引用的是同一个对象则返回 True，否则返回 False |
| is not | is not 是判断两个标识符是不是引用自不同对象 | **x is not y** ， 类似 **id(x) != id(y)**。如果引用的不是同一个对象则返回结果 True，否则返回 False。 |

**注：** [id()](https://www.runoob.com/python/python-func-id.html) 函数用于获取对象内存地址。

**is 与 == 区别：**is 用于判断两个变量引用对象是否为同一个， == 用于判断引用变量的值是否相等。

```python
a = 20
b = 20
 
if ( a is b ):
   print ("1 - a 和 b 有相同的标识")
else:
   print ("1 - a 和 b 没有相同的标识")
 
if ( id(a) == id(b) ):
   print ("2 - a 和 b 有相同的标识")
else:
   print ("2 - a 和 b 没有相同的标识")
 
# 修改变量 b 的值
b = 30
if ( a is b ):
   print ("3 - a 和 b 有相同的标识")
else:
   print ("3 - a 和 b 没有相同的标识")
 
if ( a is not b ):
   print ("4 - a 和 b 没有相同的标识")
else:
   print ("4 - a 和 b 有相同的标识")

#输出：
1 - a 和 b 有相同的标识
2 - a 和 b 有相同的标识
3 - a 和 b 没有相同的标识
4 - a 和 b 没有相同的标识
```



### 条件控制

```python
if 表达式1:
    语句
    if 表达式2:
        语句
    elif 表达式3:
        语句
    else:
        语句
elif 表达式4:
    语句
else:
    语句
```



### 循环控制

#### while循环

```python
while <expr>:
    <statement(s)>
else:
    <additional_statement(s)>
```

```python
count = 0
while count < 5:
   print (count, " 小于 5")
   count = count + 1
else:
   print (count, " 大于或等于 5")

#输出：
0  小于 5
1  小于 5
2  小于 5
3  小于 5
4  小于 5
5  大于或等于 5
```



#### for循环

 for 循环可以遍历任何可迭代对象，如一个列表或者一个字符串。

```python
for <variable> in <sequence>:
    <statements>
else:
    <statements>
```

```python
#遍历列表：
sites = ["Baidu", "Google","Runoob","Taobao"]
for site in sites:
    print(site)

#遍历字符串：
word = 'runoob'
for letter in word:
    print(letter)

#配合range()函数使用，遍历一定范围内的数字：
for number in range(1, 6):
    print(number)
    
```

##### 遍历技巧

在**字典**中遍历时，关键字和对应的值可以使用 items() 方法同时解读出来：

```python
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)
...
gallahad the pure
robin the brave
```

在**序列**中遍历时，索引位置和对应值可以使用 enumerate() 函数同时得到：

```python
>>> for i, v in enumerate(['tic', 'tac', 'toe']):
...     print(i, v)
...
0 tic
1 tac
2 toe
```

同时遍历两个或更多的序列，可以使用 zip() 组合：

```python
>>> questions = ['name', 'quest', 'favorite color']
>>> answers = ['lancelot', 'the holy grail', 'blue']
>>> for q, a in zip(questions, answers):
...     print('What is your {0}?  It is {1}.'.format(q, a))
...
What is your name?  It is lancelot.
What is your quest?  It is the holy grail.
What is your favorite color?  It is blue.
```

要**反向遍历**一个序列，首先指定这个序列，然后调用 reversed() 函数：

```python
>>> for i in reversed(range(1, 10, 2)):
...     print(i)
...
9
7
5
3
1
```

要按**顺序遍历**一个序列，使用 **sorted()** 函数返回一个已排序的序列，并不修改原值：

```python
>>> basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
>>> for f in sorted(set(basket)):
...     print(f)
...
apple
banana
orange
pear
```



#### range() 函数

```python
range(start, end, step)
```

```python
for i in range(0, 10, 3) :
    print(i, end="")

for i in range(-10, -100, -30) :
    print(i, end="")
    
a = ['Google', 'Baidu', 'Runoob', 'Taobao', 'QQ']
for i in range(len(a)):
	print(i, a[i], end=" ")

#输出：
0369
-10-40-70
0 Google 1 Baidu 2 Runoob 3 Taobao 4 QQ 
```

使用range()函数创建一个列表

```python
>>>list(range(5))
[0, 1, 2, 3, 4]
```



#### pass 语句

Python pass是空语句，不做任何事情，一般用做占位语句，是为了保持程序结构的完整性。

```python
while True:
    pass  # 等待键盘中断 (Ctrl+C)
```



### 推导式

Python 推导式是一种独特的数据处理方式，可以**从一个数据序列构建另一个新的数据序列的结构体**。支持各种数据结构的推导式：

- 列表(list)推导式
- 字典(dict)推导式
- 集合(set)推导式
- 元组(tuple)推导式

#### 列表推导式

列表推导式格式为：

```python
[表达式 for 变量 in 列表] 
[out_exp_res for out_exp in input_list]

或者 

[表达式 for 变量 in 列表 if 条件]
[out_exp_res for out_exp in input_list if condition]
```

- out_exp_res：列表生成元素表达式，可以是有返回值的函数。
- for out_exp in input_list：迭代 input_list 将 out_exp 传入到 out_exp_res 表达式中。
- if condition：条件语句，可以过滤列表中不符合条件的值。

例如，过滤掉长度小于或等于3的字符串列表，并将剩下的转换成大写字母：

```python
>>> names = ['Bob','Tom','alice','Jerry','Wendy','Smith']
>>> new_names = [name.upper()for name in names if len(name)>3]
>>> print(new_names)
['ALICE', 'JERRY', 'WENDY', 'SMITH']
```



#### 字典推导式

字典推导基本格式：

```python
{ key_expr: value_expr for value in collection }

或

{ key_expr: value_expr for value in collection if condition }
```

例如，使用字符串及其长度创建字典：

```python
listdemo = ['Google','Runoob', 'Taobao']
# 将列表中各字符串值为键，各字符串的长度为值，组成键值对
>>> newdict = {key:len(key) for key in listdemo}
>>> newdict
{'Google': 6, 'Runoob': 6, 'Taobao': 6}
```

例如，提供三个数字，以三个数字为键，三个数字的平方为值来创建字典：

```python
>>> dic = {x: x**2 for x in (2, 4, 6)}
>>> dic
{2: 4, 4: 16, 6: 36}
>>> type(dic)
<class 'dict'>
```



#### 集合推导式

集合推导式基本格式：

```python
{ expression for item in Sequence }
或
{ expression for item in Sequence if conditional }
```

计算数字 1,2,3 的平方数：

```python
>>> setnew = {i**2 for i in (1,2,3)}
>>> setnew
{1, 4, 9}
```



#### 元组推导式（生成器表达式）

元组推导式可以利用 range 区间、元组、列表、字典和集合等数据类型，快速生成一个满足指定需求的元组。

元组推导式基本格式：

```python
(expression for item in Sequence )
或
(expression for item in Sequence if conditional )
```

```python
>>> a = (x for x in range(1,10))
>>> a
<generator object <genexpr> at 0x7faf6ee20a50>  # 返回的是生成器对象

>>> tuple(a)       # 使用 tuple() 函数，可以直接将生成器对象转换成元组
(1, 2, 3, 4, 5, 6, 7, 8, 9)
```



### 函数

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230805192519319.png" alt="image-20230805192519319" style="zoom: 55%;" />

```python
def 函数名（参数列表）:
    函数体
```

函数的参数传递：

- **不可变类型：**类似 C++ 的值传递，如整数、字符串、元组。如 fun(a)，传递的只是 a 的值，没有影响 a 对象本身。如果在 fun(a) 内部修改 a 的值，则是新生成一个 a 的对象。
- **可变类型：**类似 C++ 的引用传递，如 列表，字典。如 fun(la)，则是将 la 真正的传过去，修改后 fun 外部的 la 也会受影响

【python 中一切都是对象，严格意义我们不能说值传递还是引用传递，我们应该说传不可变对象和传可变对象。】



#### 匿名函数

Python 使用 **lambda** 来创建匿名函数。所谓匿名，意即不再使用 **def** 语句这样标准的形式定义一个函数。

- **lambda** 只是一个表达式，函数体比 **def** 简单很多。
- lambda 的主体是一个表达式，而不是一个代码块。仅仅能在 lambda 表达式中封装有限的逻辑进去。
- lambda 函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。
- 虽然 lambda 函数看起来只能写一行，却不等同于 C 或 C++ 的内联函数，内联函数的目的是调用小函数时不占用栈内存从而减少函数调用的开销，提高代码的执行速度。

语法格式：

```python
lambda [arg1 [,arg2,.....argn]]:expression
```

例如：

```python
# x + 10
x = lambda a : a + 10
print(x(5))
 
# x + y
sum = lambda arg1, arg2: arg1 + arg2
# 调用sum函数
print ("相加后的值为 : ", sum( 10, 20 ))	#结果为30
print ("相加后的值为 : ", sum( 20, 20 ))	#结果为40
```

也可以将匿名函数封装在一个函数内，这样可以使用同样的代码来创建多个匿名函数。

以下实例将匿名函数封装在 myfunc 函数中，通过传入不同的参数来创建不同的匿名函数：

```py
def myfunc(n):
	return lambda a : a * n
 
mydoubler = myfunc(2)
mytripler = myfunc(3)
 
print(mydoubler(11))
print(mytripler(11))
```



### math模块

#### math 模块常量

| 常量                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [math.e](https://www.runoob.com/python3/ref-math-e.html)     | 返回欧拉数 (2.7182...)                                       |
| [math.inf](https://www.runoob.com/python3/ref-math-inf.html) | 返回正无穷大浮点数                                           |
| [math.nan](https://www.runoob.com/python3/ref-math-nan.html) | 返回一个浮点值 NaN (not a number)                            |
| [math.pi](https://www.runoob.com/python3/ref-math-pi.html)   | π 一般指圆周率。 圆周率 PI (3.1415...)                       |
| [math.tau](https://www.runoob.com/python3/ref-math-tau.html) | 数学常数 τ = 6.283185...，精确到可用精度。Tau 是一个圆周常数，等于 2π，圆的周长与半径之比。 |

#### math 模块方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [math.acos(x)](https://www.runoob.com/python3/ref-math-acos.html) | 返回 x 的反余弦，结果范围在 0 到 pi 之间。                   |
| [math.acosh(x)](https://www.runoob.com/python3/ref-math-acosh.html) | 返回 x 的反双曲余弦值。                                      |
| [math.asin(x)](https://www.runoob.com/python3/ref-math-asin.html) | 返回 x 的反正弦值，结果范围在 -pi/2 到 pi/2 之间。           |
| [math.asinh(x)](https://www.runoob.com/python3/ref-math-asinh.html) | 返回 x 的反双曲正弦值。                                      |
| [math.atan(x)](https://www.runoob.com/python3/ref-math-atan.html) | 返回 x 的反正切值，结果范围在 -pi/2 到 pi/2 之间。           |
| [math.atan2(y, x)](https://www.runoob.com/python3/ref-math-atan2.html) | 返回给定的 X 及 Y 坐标值的反正切值，结果是在 -pi 和 pi 之间。 |
| [math.atanh(x)](https://www.runoob.com/python3/ref-math-atanh.html) | 返回 x 的反双曲正切值。                                      |
| [math.ceil(x)](https://www.runoob.com/python3/ref-math-ceil.html) | 将 x 向上舍入到最接近的整数                                  |
| [math.comb(n, k)](https://www.runoob.com/python3/ref-math-comb.html) | 返回不重复且无顺序地从 n 项中选择 k 项的方式总数。           |
| [math.copysign(x, y)](https://www.runoob.com/python3/ref-math-copysign.html) | 返回一个基于 x 的绝对值和 y 的符号的浮点数。                 |
| [math.cos()](https://www.runoob.com/python3/ref-math-cos.html) | 返回 x 弧度的余弦值。                                        |
| [math.cosh(x)](https://www.runoob.com/python3/ref-math-cosh.html) | 返回 x 的双曲余弦值。                                        |
| [math.degrees(x)](https://www.runoob.com/python3/ref-math-degrees.html) | 将角度 x 从弧度转换为度数。                                  |
| [math.dist(p, q)](https://www.runoob.com/python3/ref-math-dist.html) | 返回 p 与 q 两点之间的欧几里得距离，以一个坐标序列（或可迭代对象）的形式给出。 两个点必须具有相同的维度。 |
| [math.erf(x)](https://www.runoob.com/python3/ref-math-erf.html) | 返回一个数的误差函数                                         |
| [math.erfc(x)](https://www.runoob.com/python3/ref-math-erfc.html) | 返回 x 处的互补误差函数                                      |
| [math.exp(x)](https://www.runoob.com/python3/ref-math-exp.html) | 返回 e 的 x 次幂，Ex， 其中 e = 2.718281... 是自然对数的基数。 |
| [math.expm1()](https://www.runoob.com/python3/ref-math-expm1.html) | 返回 Ex - 1， e 的 x 次幂，Ex，其中 e = 2.718281... 是自然对数的基数。这通常比 math.e ** x 或 pow(math.e, x) 更精确。 |
| [math.fabs(x)](https://www.runoob.com/python3/ref-math-fabs.html) | 返回 x 的绝对值。                                            |
| [math.factorial(x)](https://www.runoob.com/python3/ref-math-factorial.html) | 返回 x 的阶乘。 如果 x 不是整数或为负数时则将引发 ValueError。 |
| [math.floor()](https://www.runoob.com/python3/ref-math-floor.html) | 将数字向下舍入到最接近的整数                                 |
| [math.fmod(x, y)](https://www.runoob.com/python3/ref-math-fmod.html) | 返回 x/y 的余数                                              |
| [math.frexp(x)](https://www.runoob.com/python3/ref-math-frexp.html) | 以 (m, e) 对的形式返回 x 的尾数和指数。 m 是一个浮点数， e 是一个整数，正好是 x == m * 2**e 。 如果 x 为零，则返回 (0.0, 0) ，否则返回 0.5 <= abs(m) < 1 。 |
| [math.fsum(iterable)](https://www.runoob.com/python3/ref-math-fsum.html) | 返回可迭代对象 (元组, 数组, 列表, 等)中的元素总和，是浮点值。 |
| [math.gamma(x)](https://www.runoob.com/python3/ref-math-gamma.html) | 返回 x 处的伽马函数值。                                      |
| [math.gcd()](https://www.runoob.com/python3/ref-math-gcd.html) | 返回给定的整数参数的最大公约数。                             |
| [math.hypot()](https://www.runoob.com/python3/ref-math-hypot.html) | 返回欧几里得范数，sqrt(sum(x**2 for x in coordinates))。 这是从原点到坐标给定点的向量长度。 |
| [math.isclose(a,b)](https://www.runoob.com/python3/ref-math-isclose.html) | 检查两个值是否彼此接近，若 a 和 b 的值比较接近则返回 True，否则返回 False。。 |
| [math.isfinite(x)](https://www.runoob.com/python3/ref-math-isfinite.html) | 判断 x 是否有限，如果 x 既不是无穷大也不是 NaN，则返回 True ，否则返回 False 。 |
| [math.isinf(x)](https://www.runoob.com/python3/ref-math-isinf.html) | 判断 x 是否是无穷大，如果 x 是正或负无穷大，则返回 True ，否则返回 False 。 |
| [math.isnan()](https://www.runoob.com/python3/ref-math-isnan.html) | 判断数字是否为 NaN，如果 x 是 NaN（不是数字），则返回 True ，否则返回 False 。 |
| [math.isqrt()](https://www.runoob.com/python3/ref-math-isqrt.html) | 将平方根数向下舍入到最接近的整数                             |
| [math.ldexp(x, i)](https://www.runoob.com/python3/ref-math-ldexp.html) | 返回 x * (2**i) 。 这基本上是函数 [math.frexp() 的反函数。](https://www.runoob.com/python3/ref-math-frexp.html) |
| [math.lgamma()](https://www.runoob.com/python3/ref-math-lgamma.html) | 返回伽玛函数在 x 绝对值的自然对数。                          |
| [math.log(x[, base\])](https://www.runoob.com/python3/ref-math-log.html) | 使用一个参数，返回 x 的自然对数（底为 e ）。                 |
| [math.log10(x)](https://www.runoob.com/python3/ref-math-log10.html) | 返回 x 底为 10 的对数。                                      |
| [math.log1p(x)](https://www.runoob.com/python3/ref-math-log1p.html) | 返回 1+x 的自然对数（以 e 为底）。                           |
| [math.log2(x)](https://www.runoob.com/python3/ref-math-log2.html) | 返回 x 以 2 为底的对数                                       |
| [math.perm(n, k=None)](https://www.runoob.com/python3/ref-math-perm.html) | 返回不重复且有顺序地从 n 项中选择 k 项的方式总数。           |
| [math.pow(x, y)](https://www.runoob.com/python3/ref-math-pow.html) | 将返回 x 的 y 次幂。                                         |
| [math.prod(iterable)](https://www.runoob.com/python3/ref-math-prod.html) | 计算可迭代对象中所有元素的积。                               |
| [math.radians(x)](https://www.runoob.com/python3/ref-math-radians.html) | 将角度 x 从度数转换为弧度。                                  |
| [math.remainder(x, y)](https://www.runoob.com/python3/ref-math-remainder.html) | 返回 IEEE 754 风格的 x 除于 y 的余数。                       |
| [math.sin(x)](https://www.runoob.com/python3/ref-math-sin.html) | 返回 x 弧度的正弦值。                                        |
| [math.sinh(x)](https://www.runoob.com/python3/ref-math-sinh.html) | 返回 x 的双曲正弦值。                                        |
| [math.sqrt(x)](https://www.runoob.com/python3/ref-math-sqrt.html) | 返回 x 的平方根。                                            |
| [math.tan(x)](https://www.runoob.com/python3/ref-math-tan.html) | 返回 x 弧度的正切值。                                        |
| [math.tanh(x)](https://www.runoob.com/python3/ref-math-tanh.html) | 返回 x 的双曲正切值。                                        |
| [math.trunc(x)](https://www.runoob.com/python3/ref-math-trunc.html) | 返回 x 截断整数的部分，即返回整数部分，删除小数部分          |

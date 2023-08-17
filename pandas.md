# pandas

**pandas**是python的核心**数据分析支持库**。

处理数据一般分为几个阶段：数据整理与清洗、数据分析与建模、数据可视化与制表，Pandas 是处理数据的理想工具。



### 数据结构

**Series** 是一种类似于一维数组的对象，它由一组数据（各种Numpy数据类型）以及一组与之相关的数据标签（即索引）组成。

**DataFrame** 是一个表格型的数据结构，它含有一组有序的列，每列可以是不同的值类型（数值、字符串、布尔型值）。DataFrame 既有行索引也有列索引，它可以被看做由 Series 组成的字典（共同用一个索引）。



### Series

Pandas Series 类似表格中的一个列（column），类似于一维数组，可以保存任何数据类型。

Series 由索引（index）和列组成，函数如下：

```
pandas.Series( data, index, dtype, name, copy)
```

参数说明：

- **data**：一组数据(ndarray 类型)。
- **index**：数据索引标签，如果不指定，**默认从 0 开始**。
- **dtype**：数据类型，默认会自己判断。
- **name**：设置名称。
- **copy**：拷贝数据，默认为 False。



可以指定索引值，如下实例：

```python
a = ["Google", "Runoob", "Wiki"]
myvar = pd.Series(a, index = ["x", "y", "z"], name="Series-TEST")
print(myvar)
print(myvar["y"]) #根据索引值读取数据

#输出结果：
x    Google
y    Runoob
z      Wiki
Name: Series-TEST, dtype: object
Runoob
```

输出结果：

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807095732678.png" alt="image-20230807095732678" style="zoom: 50%;" />



使用 key/value 对象，类似字典来创建 Series，此时key 变成了索引值：

```python
sites = {1: "Google", 2: "Runoob", 3: "Wiki"}
myvar = pd.Series(sites)
print(myvar)
myvar2 = pd.Series(sites, index = [1, 2]) #选定字典的一部分数据，从而指定需要的索引
print(myvar2)

#输出：
1    Google
2    Runoob
3      Wiki
dtype: object
1    Google
2    Runoob
dtype: object
```



### DataFrame

DataFrame 是一个**表格型**的数据结构，它含有一组有序的列，每列可以是不同的值类型（数值、字符串、布尔型值）。DataFrame 既有行索引也有列索引，它可以被看做由 Series 组成的字典（共同用一个索引）。DataFrame 是一个二维的数组结构，类似二维数组。

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807100457365.png" alt="image-20230807100457365" style="zoom:67%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807100514987.png" alt="image-20230807100514987" style="zoom:67%;" />

 DataFrame 数据类型一个表格，包含 rows（行） 和 columns（列）：

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807101117438.png" alt="image-20230807101117438" style="zoom:67%;" />



DataFrame 构造方法如下：

```
pandas.DataFrame( data, index, columns, dtype, copy)
```

参数说明：

- **data**：一组数据(ndarray、series, map, lists, dict 等类型)。
- **index**：索引值，或者可以称为**行标签**。
- **columns**：**列标签**，默认为 RangeIndex (0, 1, 2, …, n) 。
- **dtype**：数据类型。
- **copy**：拷贝数据，默认为 False。



##### 创建DataFrame

使用 列表 创建 DataFrame：

```python
data = [['Google',10],['Runoob',12],['Wiki',13]]
df = pd.DataFrame(data,columns=['Site','Age'])
print(df)

#输出：
     Site  Age
0  Google   10
1  Runoob   12
2    Wiki   13
```

使用 ndarrays 创建 DataFrame：

```python
data = {'Site':['Google', 'Runoob', 'Wiki'], 'Age':[10, 12, 13]}
df = pd.DataFrame(data)
print (df)

#输出：
     Site  Age
0  Google   10
1  Runoob   12
2    Wiki   13
```

使用字典（key/value）创建 DataFrame，其中字典的 key 为列名，没有对应的部分数据为 **NaN**：

```python
data = [{'a': 1, 'b': 2},{'a': 5, 'b': 10, 'c': 20}]
df = pd.DataFrame(data)
print (df)

#输出：
   a   b     c
0  1   2   NaN
1  5  10  20.0
```



##### 返回指定行

使用 **loc** 属性返回指定行的数据，返回结果是 Series 数据。

```python
data = {
    "calories": [420, 380, 390],
    "duration": [50, 40, 45]
}
# 数据载入到 DataFrame 对象
df = pd.DataFrame(data)
print(df)
# 返回第一行
print(df.loc[0])
# 返回第二行
print(df.loc[1])

#输出：
   calories  duration
0       420        50
1       380        40
2       390        45
calories    420
duration     50
Name: 0, dtype: int64
calories    380
duration     40
Name: 1, dtype: int64
```

使用 **loc** 属性返回多行数据，使用 **[[ ... ]]** 格式，**...** 为各行的索引，以逗号隔开，返回结果是 DataFrame 数据。：

```python
data = {
    "calories": [420, 380, 390],
    "duration": [50, 40, 45]
}
# 数据载入到 DataFrame 对象
df = pd.DataFrame(data)
# 返回第一行和第二行
print(df.loc[[0, 1]])

#输出：
   calories  duration
0       420        50
1       380        40
```

也可以指定索引值，如下实例：

```python
data = {
    "calories": [420, 380, 390],
    "duration": [50, 40, 45]
}
df = pd.DataFrame(data, index = ["day1", "day2", "day3"])
print(df)
print()
# 指定索引
print(df.loc["day2"])

#输出：
      calories  duration
day1       420        50
day2       380        40
day3       390        45

calories    380
duration     40
Name: day2, dtype: int64
```

##### 返回某一列

```python
df['name']			#得到的是不包含列索引的Series结构
df[['name']]		#得到是包含列索引的DataFrame结构
df.name				#得到是不包含列索引的Series结构
```

##### 遍历列

```python

```



### Pandas CSV 文件

CSV（Comma-Separated Values，逗号分隔值，有时也称为字符分隔值，因为分隔字符也可以不是逗号），其文件以纯文本形式存储表格数据（数字和文本）。

#### 显示文件内容

**to_string()** 用于返回 DataFrame 类型的数据。

如果不使用该函数，则输出结果为数据的前面 5 行和末尾 5 行，中间部分以 **...** 代替。

```python
import pandas as pd
df = pd.read_csv('E://DataFiles/Runoob_Data/nba.csv')
print(df)
print(df.to_string())
```

![image-20230807102559444](https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807102559444.png)

![image-20230807102629482](https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807102629482.png)



#### 存储文件

使用 **to_csv()** 方法将 DataFrame 存储为 csv 文件：

```python
import pandas as pd

# 三个字段 name, site, age
nme = ["Google", "Runoob", "Taobao", "Wiki"]
st = ["www.google.com", "www.runoob.com", "www.taobao.com", "www.wikipedia.org"]
ag = [90, 40, 80, 98]

# 字典
dict = {'name': nme, 'site': st, 'age': ag}
df = pd.DataFrame(dict)

# 保存 dataframe 为.csv文件
df.to_csv('E://DataFiles/Runoob_Data/site.csv')
```

在 excel 中查看文件内容：

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807102914657.png" alt="image-20230807102914657" style="zoom: 67%;" />



#### 数据处理

##### head()

**head( n )** 方法用于读取前面的 n 行，如果不填参数 n ，默认返回 5 行。

```python
df = pd.read_csv('E://DataFiles/Runoob_Data/nba.csv')
print(df.head(6))
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807103127164.png" alt="image-20230807103127164" style="zoom:67%;" />



##### tail()

**tail( n )** 方法用于读取尾部的 n 行，如果不填参数 n ，默认返回 5 行，空行各个字段的值返回 **NaN**。

```python
df = pd.read_csv('E://DataFiles/Runoob_Data/nba.csv')
print(df.tail())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807103308412.png" alt="image-20230807103308412" style="zoom:67%;" />



##### info()

info() 方法返回表格的一些基本信息：

```python
df = pd.read_csv('E://DataFiles/Runoob_Data/nba.csv')
print(df.info())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807103420410.png" alt="image-20230807103420410" style="zoom:67%;" />



### 查看数据

| 函数          | 说明                                                         |
| :------------ | :----------------------------------------------------------- |
| df.head(n)    | 显示前 n 行数据；                                            |
| df.tail(n)    | 显示后 n 行数据；                                            |
| df.info()     | 显示数据的信息，包括列名、数据类型、缺失值等；               |
| df.describe() | 显示数据的基本统计信息，包括均值、方差、最大值、最小值等；   |
| df.shape      | 显示数据的行数和列数。<br />(shape[0]返回行数，shape[1]返回列数) |

```python
# 删除包含缺失值的行或列
df.dropna()

# 将缺失值替换为指定的值
df.fillna(0)

# 将指定值替换为新值
df.replace('old_value', 'new_value')

# 检查是否有重复的数据
df.duplicated()

# 删除重复的数据
df.drop_duplicates()
```



### 数据选择和切片

| 函数                                          | 说明                                   |
| :-------------------------------------------- | :------------------------------------- |
| df[column_name]                               | 选择指定的列；                         |
| df.loc[row_index, column_name]                | 通过**标签**选择数据；                 |
| df.iloc[row_index, column_index]              | 通过**位置**选择数据；                 |
| df.ix[row_index, column_name]                 | 通过标签或位置选择数据；               |
| df.filter(items=[column_name1, column_name2]) | 选择指定的列；                         |
| df.filter(regex='regex')                      | 选择列名匹配正则表达式的列；           |
| df.sample(n)                                  | 随机选择 n 行数据。                    |
| df[df['column_name'] > value]                 | 选择列中满足条件的行。                 |
| df.query('column_name > value')               | 使用字符串表达式选择列中满足条件的行。 |

```python
# 选择指定的列
df['column_name']

# 通过标签选择数据
df.loc[row_index, column_name]

# 通过位置选择数据
df.iloc[row_index, column_index]

# 通过标签或位置选择数据
df.ix[row_index, column_name]

# 选择指定的列
df.filter(items=['column_name1', 'column_name2'])

# 选择列名匹配正则表达式的列
df.filter(regex='regex')

# 随机选择 n 行数据
df.sample(n=5)
```



### 数据排序

| 函数                                                         | 说明                 |
| :----------------------------------------------------------- | :------------------- |
| df.sort_values(column_name)                                  | 按照指定列的值排序； |
| df.sort_values([column_name1, column_name2], ascending=[True, False]) | 按照多个列的值排序； |
| df.sort_index()                                              | 按照索引排序。       |

```python
# 按照指定列的值排序
df.sort_values('column_name')

# 按照多个列的值排序
df.sort_values(['column_name1', 'column_name2'], ascending=[True, False])

# 按照索引排序
df.sort_index()
```



### 数据分组和聚合

| 函数                                            | 说明                         |
| :---------------------------------------------- | :--------------------------- |
| df.groupby(column_name)                         | 按照指定列进行分组；         |
| df.aggregate(function_name)                     | 对分组后的数据进行聚合操作； |
| df.pivot_table(values, index, columns, aggfunc) | 生成透视表。                 |

```python
# 按照指定列进行分组
df.groupby('column_name')

# 对分组后的数据进行聚合操作
df.aggregate('function_name')

# 生成透视表
df.pivot_table(values='value', index='index_column', columns='column_name', aggfunc='function_name')
```



### 数据合并

| 函数                               | 说明                             |
| :--------------------------------- | :------------------------------- |
| pd.concat([df1, df2])              | 将多个数据框按照行或列进行合并； |
| pd.merge(df1, df2, on=column_name) | 按照指定列将两个数据框进行合并.  |



### 数据统计和描述

| 函数          | 说明                                                 |
| :------------ | :--------------------------------------------------- |
| df.describe() | 计算基本统计信息，如均值、标准差、最小值、最大值等。 |
| df.mean()     | 计算每列的平均值。                                   |
| df.median()   | 计算每列的中位数。                                   |
| df.mode()     | 计算每列的众数。                                     |
| df.count()    | 计算每列非缺失值的数量。                             |
| df.max()      | 计算每一列的最大值。                                 |
| df.min()      | 计算每一列的最小值。                                 |



### 数据清洗

数据清洗是对一些没有用的数据进行处理的过程。很多数据集存在**数据缺失**、数据**格式错误**、**错误**数据或重复数据的情况，如果要使数据分析更加准确，就需要对这些没有用的数据进行处理。

| 函数                             | 说明                     |
| :------------------------------- | :----------------------- |
| df.dropna()                      | 删除包含缺失值的行或列； |
| df.fillna(value)                 | 将缺失值替换为指定的值； |
| df.replace(old_value, new_value) | 将指定值替换为新值；     |
| df.duplicated()                  | 检查是否有重复的数据；   |
| df.drop_duplicates()             | 删除重复的数据。         |



#### 清洗空值

##### **isnull()** 查询空值

可以通过 **isnull()** 判断各个单元格是否为空。

```python
df = pd.read_csv('E://DataFiles/Runoob_Data/property-data.csv')

print (df['NUM_BEDROOMS'])
print (df['NUM_BEDROOMS'].isnull())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807104112068.png" alt="image-20230807104112068" style="zoom: 67%;" />

也可以自己**指定空数据类型**：

```python
missing_values = ["n/a", "na", "--"]
df = pd.read_csv('E://DataFiles/Runoob_Data/property-data.csv', na_values = missing_values)

print (df['NUM_BEDROOMS'])
print (df['NUM_BEDROOMS'].isnull())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807104307985.png" alt="image-20230807104307985" style="zoom:67%;" />



##### dropna() 删除空值

如果我们要删除包含空字段的行，可以使用 **dropna()** 方法，语法格式如下：

```python
DataFrame.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)
```

**参数说明：**

- axis：默认为 **0**，表示逢空值剔除整行，如果设置参数 **axis＝1** 表示逢空值去掉整列。
- how：默认为 **'any'** 如果一行（或一列）里任何一个数据有出现 NA 就去掉整行，如果设置 **how='all'** 一行（或列）都是 NA 才去掉这整行。
- thresh：设置需要多少非空值的数据才可以保留下来的。
- subset：设置想要检查的列。如果是多个列，可以使用列名的 list 作为参数。
- inplace：如果设置 True，将计算得到的值直接覆盖之前的值并返回 None，修改的是源数据。



#####  **fillna()** 替换空值

```python
missing_values = ["n/a", "na", "--"]
df = pd.read_csv('E://DataFiles/Runoob_Data/property-data.csv', na_values = missing_values)
df.fillna(12345, inplace = True)
print(df.to_string())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807104453054.png" alt="image-20230807104453054" style="zoom:67%;" />

也可以指定某一个列来替换数据：

```python
missing_values = ["n/a", "na", "--"]
df = pd.read_csv('E://DataFiles/Runoob_Data/property-data.csv', na_values = missing_values)
df['PID'].fillna(12345, inplace = True)

print(df.to_string())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807104614538.png" alt="image-20230807104614538" style="zoom:67%;" />



##### 使用列的均值、中位数或众数替换空值

使用 **mean()** 方法计算列的均值并替换空单元格：

```python
missing_values = ["n/a", "na", "--"]
df = pd.read_csv('E://DataFiles/Runoob_Data/property-data.csv', na_values = missing_values)

x = df["ST_NUM"].mean()
df["ST_NUM"].fillna(x, inplace = True)
print(df.to_string())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807105016864.png" alt="image-20230807105016864" style="zoom:67%;" />

使用 **median()** 方法计算列的中位数并替换空单元格：

```python
missing_values = ["n/a", "na", "--"]
df = pd.read_csv('E://DataFiles/Runoob_Data/property-data.csv', na_values = missing_values)

x = df["ST_NUM"].median()
df["ST_NUM"].fillna(x, inplace = True)
print(df.to_string())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807105112541.png" alt="image-20230807105112541" style="zoom:67%;" />

使用 mode() 方法计算列的众数并替换空单元格：

```python
missing_values = ["n/a", "na", "--"]
df = pd.read_csv('E://DataFiles/Runoob_Data/property-data.csv', na_values = missing_values)

x = df["ST_NUM"].mode()
df["ST_NUM"].fillna(x, inplace = True)
print(df.to_string())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807105157749.png" alt="image-20230807105157749" style="zoom:67%;" />



#### 清洗 格式错误 数据

数据格式错误的单元格会使数据分析变得困难，甚至不可能。

我们可以通过包含空单元格的行，或者将列中的所有单元格转换为相同格式的数据。

以下实例会格式化日期：

```python
# 第三个日期格式错误
data = {
  "Date": ['2020/12/01', '2020/12/02' , '20201226'],
  "duration": [50, 40, 45]
}

df = pd.DataFrame(data, index = ["day1", "day2", "day3"])
df['Date'] = pd.to_datetime(df['Date'],format='mixed')
print(df.to_string())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807105603337.png" alt="image-20230807105603337" style="zoom:67%;" />



#### 清洗 错误数据

数据错误也是很常见的情况，我们可以对错误的数据进行替换或移除。

以下实例会替换错误年龄的数据：

```python
person = {
  "name": ['Google', 'Runoob' , 'Taobao'],
  "age": [50, 40, 12345]    # 12345 年龄数据是错误的
}

df = pd.DataFrame(person)
df.loc[2, 'age'] = 30 # 修改数据
print(df.to_string())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807105729918.png" alt="image-20230807105729918" style="zoom:67%;" />

也可以设置条件语句：

```python
person = {
  "name": ['Google', 'Runoob' , 'Taobao'],
  "age": [50, 40, 12345]    # 12345 年龄数据是错误的
}
df = pd.DataFrame(person)

for x in df.index:
  if df.loc[x, "age"] > 120:
    df.loc[x, "age"] = 120

print(df.to_string())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807105842759.png" alt="image-20230807105842759" style="zoom:67%;" />

也可以将错误数据的行删除：

```python
person = {
  "name": ['Google', 'Runoob' , 'Taobao'],
  "age": [50, 40, 12345]    # 12345 年龄数据是错误的
}
df = pd.DataFrame(person)

for x in df.index:
  if df.loc[x, "age"] > 120:
    df.drop(x, inplace = True)

print(df.to_string())
```

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230807105939972.png" alt="image-20230807105939972" style="zoom:67%;" />



#### 清洗 重复数据

使用 **duplicated()** 和 **drop_duplicates()** 方法。

如果对应的数据是重复的，**duplicated()** 会返回 True，否则返回 False。

```python
person = {
  "name": ['Google', 'Runoob', 'Runoob', 'Taobao'],
  "age": [50, 40, 40, 23]
}
df = pd.DataFrame(person)
print(df, end="\n\n")
print(df.duplicated(), end="\n\n")

df_unique = df.drop_duplicates() #删除重复数据
print(df_unique)

#输出：
     name  age
0  Google   50
1  Runoob   40
2  Runoob   40
3  Taobao   23

0    False
1    False
2     True
3    False
dtype: bool

     name  age
0  Google   50
1  Runoob   40
3  Taobao   23
```


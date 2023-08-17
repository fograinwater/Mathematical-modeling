## DataFrame、Series、list

**pandas**是python的核心**数据分析支持库**

处理数据一般分为几个阶段：数据整理与清洗、数据分析与建模、数据可视化与制表，Pandas 是处理数据的理想工具。

### 图示DataFrame和Series

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230805142834881.png" alt="image-20230805142834881" style="zoom:40%;" />



### DataFrame

#### 一、读取 `excel ` 表格

##### 1. `read_excel`用于读取表格，返回一个`DataFrame`

- `sheet_name`可用是对应的表单名，也可以用一个整数指定（索引默认从0开始）

```python
pd.read_excel("path_to_file.xls", sheet_name="Sheet1") #xls文件

pd.read_excel("path_to_file.xlsx", sheet_name="Sheet1") #xlsx文件
```

##### 2. 使用`ExcelFile`在同一个文件中读入多个表（只读入内存一次）

```python
with pd.ExcelFile("path_to_file.xls") as xls:
    df1 = pd.read_excel(xls, "Sheet1")
    df2 = pd.read_excel(xls, "Sheet2")
    
with pd.ExcelFile("E:/DataFiles/Stone_Data/rowSum附件.xlsx") as xlsx:
    df1 = pd.read_excel(xlsx, "Sheet1")
    df2 = pd.read_excel(xlsx, "Sheet2")
```




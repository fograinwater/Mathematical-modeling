#### 过采样算法

##### 过采样算法的作用：

处理不平衡数据集。在不平衡数据集中，某个类别的样本数量明显少于其他类别，导致模型在训练过程中对少数类别的学习不足。这是往往需要采用过采样技术重构数据集，从而实现类别平衡。

- **查看数据的结果分布情况：pd.value_counts(series)：**

  - 统计一个Series中每个唯一值出现的次数。

  - `series`是一个pandas Series对象，它可以是一维数组、列表或其他形式的一维数据



#### 随机过采样算法（Random Oversampling）

##### 算法原理：

通过**随机地复制**少数类别的样本来增加其数量，以实现类别平衡。

##### 具体步骤：

1. 统计数据集中每个类别的样本数量，找到样本数量最多的类别，记作N。
2. 对于每个少数类别的样本，随机地复制样本，直到其数量与样本数量最多的类别相等。
3. 将复制后的样本与原始数据集合并，形成新的平衡数据集。

##### 优点：

简单易实现，并且不需要额外的数据收集和处理过程。

##### 缺点：

可能引入过拟合问题和数据冗余。

##### python代码实现：

```python
from imblearn.over_sampling import RandomOverSampler
import numpy as np

# 假设我们有一个不平衡的数据集，X为特征矩阵，y为对应的标签
X = np.array([[1, 2], [2, 3], [3, 4], [4, 5], [5, 6], [6, 7]])
y = np.array([0, 0, 0, 1, 1, 1])

# 创建RandomOverSampler对象
ros = RandomOverSampler(random_state=42)

# 使用fit_resample函数进行过采样
X_resampled, y_resampled = ros.fit_resample(X, y)

# 输出过采样后的样本数量
print("过采样后样本数量:", len(X_resampled))

# 输出过采样后的标签分布
unique, counts = np.unique(y_resampled, return_counts=True)
print(dict(zip(unique, counts))) #将类别和数量打包成字典输出
```



#### SMOTE（Synthetic Minority Oversampling Technique）合成少数类过采样技术

##### 算法原理：

对少数类样本进行分析并根据少数类样本的临近点情况人工合成新样本添加到数据集中。

##### 具体步骤：

(1)对于少数类中每一个样本x，以欧氏距离为标准计算它到少数类样本集中所有样本的距离，得到其近邻。

(2)根据样本不平衡比例设置一个采样比例以确定采样倍率N，对于每一个少数类样本x，从其近邻中随机选择若干k个样本，假设选择的近邻为o。（k由采样倍率决定）

(3)对于每一个随机选出的近邻o，分别与原样本按照公式o(new)=x+rand(0,1)*(x-o)构建新的样本。

##### 举例：

假设现在有100个少数类样本，采样倍率为5，即要生成500个新样本

1. 对每一个少数类样本$x_i$，求该样本到其他少数类样本的欧氏距离，并从小到大排序得到 $d1,d2…d99$ 的序列

2. 采样倍率为5，所以就取 $ d1 $ 到 $d5$ ，再根据 $x_n = x_i + rand(0, 1) × (x_iˇ−x_i)$ 得到 $x_n$

   （$x_n$ 是根据 $x_i$ 新生成的 $x_i$ 的临近点，$(x_iˇ - x)$ 相当于 $d$ ）

3. 再接着对下一个样本点 $x$ 重复1，2操作
   

##### python代码实现：

```python
from imblearn.over_sampling import SMOTE
import numpy as np

# 假设我们有一个不平衡的数据集，X为特征矩阵，y为对应的标签
X = np.array([[1, 2], [2, 3], [3, 4], [4, 5], [5, 6], [6, 7]])
y = np.array([0, 0, 0, 1, 1, 1])

# 创建SMOTE对象
smote = SMOTE(random_state=42)

# 使用fit_resample函数进行SMOTE过采样
X_resampled, y_resampled = smote.fit_resample(X, y)

# 输出过采样后的样本数量
print("过采样后样本数量:", len(X_resampled))

# 输出过采样后的标签分布
unique, counts = np.unique(y_resampled, return_counts=True)
print(dict(zip(unique, counts))) #将类别和数量打包成字典输出
```



##### 调整sampling_strategy参数

`SMOTE` 类中的 `sampling_strategy` 参数用于指定生成合成样本的比例。这个参数控制合成样本数量与原始少数类样本数量的比例。

具体来说，`sampling_strategy` 参数可以接受多种不同的输入值：

1. 浮点数：例如，`sampling_strategy=0.5` 表示生成合成样本的数量为原始少数类样本数量的一半，即生成的样本数量为原始少数类样本数量的 `0.5 * 原始少数类样本数量`。

2. 字典：如果你希望生成不同类别之间不同比例的合成样本，可以通过字典来指定。例如，`sampling_strategy={1: 100, 0: 200}` 表示生成的合成样本中，类别为 1 的样本数量为类别为 0 的样本数量的两倍。

3. 字符串：`sampling_strategy` 还可以接受字符串参数，常用的有以下几种：
   - 'auto'：自动根据数据集的不平衡情况来设置合成样本的数量，使得所有类别的样本数量均衡。
   - 'minority'：生成的合成样本数量与少数类样本数量相等，达到类别平衡。

举个例子，假设原始数据集中有 1000 个样本，其中少数类样本数量为 100 个，多数类样本数量为 900 个。若使用 `sampling_strategy=0.5`，则生成的合成样本数量为 100 * 0.5 = 50 个，这样最终的合成数据集中少数类样本数量为 100 + 50 = 150 个。

示例代码：

```python
import pandas as pd
from imblearn.over_sampling import SMOTE

# 假设有一个 DataFrame df，其中 X 表示特征数据，y 表示目标标签
# 用 pd.read_excel() 读取数据时，省略了具体数据，可以根据实际情况修改
df = pd.read_excel("data.xlsx")
X = df.drop(columns=["目标标签"])
y = df["目标标签"]

# 创建 SMOTE 实例，指定合成样本数量为原始少数类样本数量的一半
smote = SMOTE(sampling_strategy=0.5)

# 使用 SMOTE 生成新的样本
X_resampled, y_resampled = smote.fit_resample(X, y)

# X_resampled 和 y_resampled 就是生成的平衡后的新样本
# 可以根据需要将它们用于后续的模型训练等任务
```




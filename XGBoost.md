# XGBoost 

XGBoost（eXtreme Gradient Boosting）极致梯度提升

【参考链接】：

[XGBoost的原理、公式推导、Python实现和应用 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/162001079)

[机器学习集成学习之XGBoost（基于python实现） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/143009353)

[XGBoost 重要参数、方法、函数理解及调参思路（附例子）_xgboost fit函数_VariableX的博客-CSDN博客](https://blog.csdn.net/VariableX/article/details/107238137)

## 算法原理

简单来说：基于GBDT进行了三个方向的优化

1、二阶泰勒展开，去除常数项，优化损失函数项；
2、正则化项展开，去除常数项，优化正则化项；
3、合并一次项系数、二次项系数，得到最终目标函数

- 优缺点：

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230728104100387.png" alt="image-20230728104100387" style="zoom:50%;" />

## 应用

1、数据挖掘（各指标对糖尿病的影响排名）

2、推荐算法（电商预估）



## 代码实现

现有两种方法实现xgboost：使用xgboost原生接口 和 使用xgboost的sklearn接口



### xgboost原生接口

#### 模型参数

##### booster

指定弱学习器的类型，默认值为 ‘**gbtree**’，表示使用基于树的模型进行计算。‘gblinear’ 表示使用线性模型作为弱学习器。

##### eta / learning_rate

为了防止过拟合，引入了"Shrinkage"的思想，即不完全信任每个弱学习器学到的残差值。给每个弱学习器拟合的残差值都乘上取值范围在(0, 1] 的 eta，设置较小的 eta 就可以多学习几个弱学习器来弥补不足的残差。**推荐值：[0.01, 0.015, 0.025, 0.05, 0.1]**

##### gamma

指定叶节点进行分支所需的损失减少的最小值，默认值为0。设置的值越大，模型就越保守。**推荐值：[0, 0.05 ~ 0.1, 0.3, 0.5, 0.7, 0.9, 1] **

##### alpha / reg_alpha

L1正则化权重项，增加此值将使模型更加保守。

##### lambda / reg_lambda

L2正则化权重项，增加此值将使模型更加保守。

##### max_depth

指定树的最大深度，防止过拟合，默认值为6。**推荐值：[3, 5, 6, 7, 9, 12, 15, 17, 25]**。

##### min_child_weight

指定孩子节点中最小的样本权重和，如果一个叶子节点的样本权重和小于min_child_weight则拆分过程结束，默认值为1。

##### subsample

默认值1，指定采样出 subsample * n_samples 个样本用于训练弱学习器。取值在(0, 1)之间，设置为1表示使用所有数据训练弱学习器。如果取值小于1，则只有一部分样本会去做GBDT的决策树拟合。选择小于1的比例可以减少方差，即防止过拟合，但是会增加样本拟合的偏差，因此取值不能太低。**推荐的值：[0.6, 0.7, 0.8, 0.9, 1]**

##### colsample_bytree

构建弱学习器时，对特征随机采样的比例，默认值为1。**推荐值为：[0.6, 0.7, 0.8, 0.9, 1]**

##### objective

用于指定学习任务及相应的学习目标，常用的可选参数值如下：

- “reg:linear”，线性回归（默认值）
- “reg:logistic”，逻辑回归
- “binary:logistic”，二分类的逻辑回归问题，输出为概率
- “multi:softmax”，采用softmax函数处理多分类问题，同时需要设置参数num_class用于指定类别个数

##### num_class

用于设置多分类问题的类别个数

##### eval_metric

用于指定评估指标，可以传递各种评估方法组成的list。常用的评估指标如下：

- ‘rmse’，用于回归任务
- ‘mlogloss’，用于多分类任务
- ‘error’，用于二分类任务
- ‘auc’，用于二分类任务

##### silent

表示是否输出运行过程的信息，默认值为0，表示打印信息。设置为1时，不输出任何信息。**推荐设置为 0** 。

##### seed / random_state

指定随机数种子。



#### 训练参数

对于xgboost.train，参数及默认值如下：

```python
xgboost.train(params, dtrain, num_boost_round=10, evals=(),
				 obj=None, feval=None, maximize=False, 
				 early_stopping_rounds=None,  evals_result=None, 
				 verbose_eval=True, xgb_model=None, callbacks=None)

```

##### params

字典类型，用于指定各种模型参数，例如：{‘booster’:‘gbtree’,‘eta’:0.1}

##### dtrain

用于训练的数据，通过给下面的方法传递数据和标签来构造：

```python
dtrain = xgb.DMatrix(data, label=label)
```

##### num_boost_round

指定最大迭代次数，默认值为10

##### evals

列表类型，用于指定训练过程中用于评估的数据及数据的名称。例如：[(dtrain,‘train’),(dval,‘val’)]

##### obj

可以指定二阶可导的自定义目标函数

##### feval

自定义评估函数

##### maximize

是否对评估函数最大化，默认值为False

##### early_stopping_rounds

指定迭代多少次没有得到优化则停止训练，默认值为None，表示不提前停止训练。如果设置了此参数，则模型会生成三个属性：

- best_score
- best_iteration
- best_ntree_limit

> 注意：evals 必须非空才能生效，如果有多个数据集，则以最后一个数据集为准。

##### verbose_eval

可以是bool类型，也可以是整数类型。如果设置为整数，则每间隔verbose_eval次迭代就输出一次信息。

##### xgb_mosdel

加载之前训练好的 xgb 模型，用于增量训练



#### 预测函数

主要是下面的两个函数：

1、predict(data)，返回每个样本的预测结果

2、predict_proba(data)，返回每个样本属于每个类别的概率

> 注意：data 是由 DMatrix 函数封装后的数据



#### 绘制特征重要性

```python
from xgboost import plot_importance
# 显示重要特征，model 为训练好的xgb模型
plot_importance(model)
plt.show()
```



#### 使用xgboost进行分类的示例代码

```python
from sklearn.datasets import load_iris
import xgboost as xgb
from xgboost import plot_importance
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# 加载鸢尾花数据集
iris = load_iris()
X,y = iris.data,iris.target
# 数据集分割
X_train,X_test,y_train,y_test = train_test_split(X,y,test_size=0.2,random_state=123457)

# 参数
params = {
    'booster': 'gbtree',
    'objective': 'multi:softmax',
    'num_class': 3,
    'gamma': 0.1,
    'max_depth': 6,
    'lambda': 2,
    'subsample': 0.7,
    'colsample_bytree': 0.7,
    'min_child_weight': 3,
    'slient': 1,
    'eta': 0.1
}

# 构造训练集
dtrain = xgb.DMatrix(X_train,y_train)
num_rounds = 500
# xgboost模型训练
model = xgb.train(params,dtrain,num_rounds)

# 对测试集进行预测
dtest = xgb.DMatrix(X_test)
y_pred = model.predict(dtest)

# 计算准确率
accuracy = accuracy_score(y_test,y_pred)
print('accuarcy:%.2f%%'%(accuracy*100))

# 显示重要特征
plot_importance(model)
plt.show()
```

【绘制特征重要性】：

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230802195141382.png" alt="image-20230802195141382" style="zoom:67%;" />



#### 使用xgboost进行回归的示例代码

```python
import xgboost as xgb
from xgboost import plot_importance
from matplotlib import pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.datasets import fetch_california_housing
from sklearn.metrics import mean_squared_error

# 加载加利福尼亚州房价数据集
california_housing = fetch_california_housing()
X, y = california_housing.data, california_housing.target

# 数据集分割
X_train,X_test,y_train,y_test = train_test_split(X,y,test_size=0.2,random_state=0)

# 参数
params = {
    'booster': 'gbtree',
    'objective': 'reg:gamma',
    'gamma': 0.1,
    'max_depth': 5,
    'lambda': 3,
    'subsample': 0.7,
    'colsample_bytree': 0.7,
    'min_child_weight': 3,
    'slient': 1,
    'eta': 0.1,
    'seed': 1000,
    'nthread': 4,
}

dtrain = xgb.DMatrix(X_train,y_train)
num_rounds = 300
model = xgb.train(params,dtrain,num_rounds)

# 对测试集进行预测
dtest = xgb.DMatrix(X_test)
ans = model.predict(dtest)
print('mse:', mean_squared_error(y_test, ans))

# 显示重要特征
plot_importance(model)
plt.show()
```

【绘制特征重要性】：

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230802201312513.png" alt="image-20230802201312513" style="zoom:67%;" />



### xgboost的sklearn风格接口

### XGBClassifier

#### 重要参数

```python
from xgboost import XGBClassifier

xgb_model = XGBClassifier(max_depth=3,
                    learning_rate=0.1,
                    n_estimators=100, # 使用多少个弱分类器
                    objective='binary:logistic',
                    booster='gbtree',
                    gamma=0,
                    min_child_weight=1,
                    max_delta_step=0,
                    subsample=1,
                    colsample_bytree=1,
                    reg_alpha=0,
                    reg_lambda=1,
                    seed=0 # 随机数种子
                 )
```



#### 模型训练

与原生的xgboost相比，XGBClassifier并不是调用train方法进行训练，而是使用fit方法：

```python
xgb_model.fit(
    X, # array, DataFrame 类型
    y, # array, Series 类型
    eval_set=None, # 用于评估的数据集，例如：[(X_train, y_train), (X_test, y_test)]
    eval_metric=None, # 评估函数，字符串类型，例如：'mlogloss'
    early_stopping_rounds=None, 
    verbose=True, # 间隔多少次迭代输出一次信息
    xgb_model=None
)
```



#### 进行预测

```python
xgb_model.predict(data) # 返回预测值
xgb_model.predict_proba(data) # 返回各个样本属于各个类别的概率
```



#### XGBClassifier进行分类的示例代码

```python
from xgboost import XGBClassifier
from sklearn.datasets import load_iris
from xgboost import plot_importance
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# 加载样本数据集
iris = load_iris()
X,y = iris.data,iris.target
X_train,X_test,y_train,y_test = train_test_split(X,y,test_size=0.2,random_state=12343)

model = XGBClassifier(
    max_depth=3,
    learning_rate=0.1,
    n_estimators=100, # 使用多少个弱分类器
    objective='multi:softmax',
    num_class=3,
    booster='gbtree',
    gamma=0,
    min_child_weight=1,
    max_delta_step=0,
    subsample=1,
    colsample_bytree=1,
    reg_alpha=0,
    reg_lambda=1,
    seed=0 # 随机数种子
)

model.fit(X_train,y_train, eval_set=[(X_train, y_train), (X_test, y_test)], 
			eval_metric='mlogloss', verbose=50, early_stopping_rounds=50)

# 对测试集进行预测
y_pred = model.predict(X_test)
# 计算准确率
accuracy = accuracy_score(y_test,y_pred)
print('accuracy:%2.f%%'%(accuracy*100))

# 显示重要特征
plot_importance(model)
plt.show()
```



### XGBRegressor

#### 重要参数
```python
from xgboost import XGBRegressor

xgb_model = XGBRegressor(
    max_depth=3,
    learning_rate=0.1,
    n_estimators=100,
    objective='reg:linear', # 此默认参数与 XGBClassifier 不同
    booster='gbtree',
    gamma=0,
    min_child_weight=1,
    subsample=1,
    colsample_bytree=1,
    reg_alpha=0,
    reg_lambda=1,
    random_state=0
)
```



#### 示例代码

```python
import xgboost as xgb
from xgboost import plot_importance
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
from sklearn.datasets import fetch_california_housing

# 加载加利福尼亚州房价数据集
california_housing = fetch_california_housing()
X, y = california_housing.data, california_housing.target
X_train,X_test,y_train,y_test = train_test_split(X,y,test_size=0.2,random_state=0)

model = xgb.XGBRegressor(max_depth=3,
                        learning_rate=0.1,
                        n_estimators=100,
                        objective='reg:linear', # 此默认参数与 XGBClassifier 不同
                        booster='gbtree',
                        gamma=0,
                        min_child_weight=1,
                        subsample=1,
                        colsample_bytree=1,
                        reg_alpha=0,
                        reg_lambda=1,
                        random_state=0)
model.fit(X_train,y_train, eval_set=[(X_train, y_train), (X_test, y_test)],
			eval_metric='rmse', verbose=50, early_stopping_rounds=50)

# 对测试集进行预测
ans = model.predict(X_test)
mse = mean_squared_error(y_test,ans)
print('mse:', mse)

# 显示重要特征
plot_importance(model)
plt.show()
```



#### 其他应用：

##### 糖尿病评价指标排序

```python
import pandas as pd
from sklearn import metrics
from sklearn.model_selection import train_test_split
import xgboost as xgb
import matplotlib.pyplot as plt

# 设置画图的坐标可以显示中文和负号
plt.rcParams['font.sans-serif']=['SimHei']
plt.rcParams['axes.unicode_minus'] = False

# 导入数据集
df = pd.read_csv("E:\DataFiles\Diabetes_Data\diabetes.csv")
data = df.iloc[:, :8]
target = df.iloc[:, -1]

# 切分训练集和测试集
train_x, test_x, train_y, test_y = train_test_split(data, target, test_size=0.2, random_state=7)

# xgboost模型初始化设置
dtrain = xgb.DMatrix(train_x, label=train_y)
dtest = xgb.DMatrix(test_x)
watchlist = [(dtrain, 'train')]

# booster:
params = {'booster': 'gbtree',
          'objective': 'binary:logistic',
          'eval_metric': 'auc',
          'max_depth': 5,
          'lambda': 10,
          'subsample': 0.75,
          'colsample_bytree': 0.75,
          'min_child_weight': 2,
          'eta': 0.025,
          'seed': 0,
          'nthread': 8,
          'gamma': 0.15,
          'learning_rate': 0.01}

# 建模与预测：50棵树
bst = xgb.train(params, dtrain, num_boost_round=50, evals=watchlist)
ypred = bst.predict(dtest)

# 设置阈值、评价指标
y_pred = (ypred >= 0.5) * 1
print('Precesion: %.4f' % metrics.precision_score(test_y, y_pred))
print('Recall: %.4f' % metrics.recall_score(test_y, y_pred))
print('F1-score: %.4f' % metrics.f1_score(test_y, y_pred))
print('Accuracy: %.4f' % metrics.accuracy_score(test_y, y_pred))
print('AUC: %.4f' % metrics.roc_auc_score(test_y, ypred))

ypred = bst.predict(dtest)
print("测试集每个样本的得分\n", ypred)
ypred_leaf = bst.predict(dtest, pred_leaf=True)
print("测试集每棵树所属的节点数\n", ypred_leaf)
ypred_contribs = bst.predict(dtest, pred_contribs=True)
print("特征的重要性\n", ypred_contribs)

xgb.plot_importance(bst, height=0.8, title='影响糖尿病的重要特征', ylabel='特征')
plt.rc('font', family='Arial Unicode MS', size=14)
plt.show()
```



##### 预测：预测未来CO2排放量

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import xgboost as xgb
from sklearn.model_selection import cross_val_score
from sklearn.metrics import mean_squared_error
from sklearn.metrics import r2_score

data = pd.read_csv('E:\DataFiles\CO2_Data\co2.csv')

#特征工程
data['Month'] = data.YYYYMM.astype(str).str[4:6].astype(float)
data['Year'] = data.YYYYMM.astype(str).str[0:4].astype(float)
data.drop(['YYYYMM'], axis=1, inplace=True)
data.replace([np.inf, -np.inf], np.nan, inplace=True)

#查询各列特征缺失值数量（本代码无重复值，不做处理）
print(data.isnull().sum())

#将数据划分为训练数据、特征
X = data.loc[:,['Month', 'Year']].values
y = data.loc[:,'Value'].values

#将数据转换为XGBoost可以使用的格式
data_dmatrix = xgb.DMatrix(X,label=y)

#划分训练集、测试集
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
print(X_train.shape)
print(y_train.shape)
print(X_test.shape)
print(y_test.shape)

#模型训练
reg_mod = xgb.XGBRegressor(
    n_estimators=1000,
    learning_rate=0.08,
    subsample=0.75,
    colsample_bytree=1,
    max_depth=7,
    gamma=0,
)
reg_mod.fit(X_train, y_train)

scores = cross_val_score(reg_mod, X_train, y_train,cv=10)
print("Mean cross-validation score: %.2f" % scores.mean())

# 训练模型并指定评估数据集
eval_set = [(X_train, y_train), (X_test, y_test)]
reg_mod.fit(X_train, y_train, eval_set=eval_set, eval_metric='rmse', verbose=False)
# 绘制损失曲线
sns.set_style("white")
palette = sns.color_palette("Set2", n_colors=2)

plt.plot(reg_mod.evals_result()['validation_0']['rmse'], label='train', color=palette[0], linewidth=2)
plt.plot(reg_mod.evals_result()['validation_1']['rmse'], label='test', color=palette[1], linewidth=2)
plt.xlabel('Iteration')
plt.ylabel('RMSE')
plt.legend()
plt.savefig('Loss.png')
plt.show()

predictions = reg_mod.predict(X_test)

rmse = np.sqrt(mean_squared_error(y_test, predictions))
print("RMSE: %f" % (rmse))


r2 = np.sqrt(r2_score(y_test, predictions))
print("R_Squared Score : %f" % (r2))

plt.figure(figsize=(10, 5), dpi=300)
sns.lineplot(x='Year', y='Value', data=data,errorbar='sd', err_style='band',color="#ec661f")
plt.savefig('co2_emissions.png')


sns.set_style("white")
palette = sns.color_palette("husl", n_colors=2)

# 设置画布大小和分辨率
plt.figure(figsize=(10, 5), dpi=300)

# 绘制测试集数据的真实值和模型预测值的折线图
x_ax = range(len(y_test))
plt.plot(x_ax, y_test, label="True Values", color=palette[0], linewidth=1)
plt.plot(x_ax, predictions, label="Predicted Values", color=palette[1], linewidth=1)

# 添加标题和标签
plt.title("Carbon Dioxide Emissions - True vs Predicted Values")
plt.xlabel("Sample Number")
plt.ylabel("CO2 Emissions")

# 显示图例
plt.legend()
plt.savefig('True vs Predicted Values.png')
# 显示图形
plt.show()

sns.set_style("white")
palette = sns.color_palette("husl", n_colors=1)

# 设置画布大小和分辨率
plt.figure(figsize=(10, 5), dpi=300)

# 将预测值转换为DataFrame格式，并添加日期列
df_pred = pd.DataFrame(predictions, columns=['Predicted Values'])
df_pred['Date'] = pd.date_range(start='8/1/2016', periods=len(df_pred), freq='M')

# 绘制预测值的折线图
sns.lineplot(x='Date', y='Predicted Values', data=df_pred, color=palette[0], linewidth=1)

# 添加标题和标签
plt.title("Carbon Dioxide Emissions - Forecast")
plt.xlabel("Date")
plt.ylabel("CO2 Emissions")
plt.savefig('Emissions - Forecast.png')

# 显示图形
plt.show()
```


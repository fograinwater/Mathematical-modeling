#### 利用逻辑斯蒂回归/对数几率回归可以实现**线性模型做分类**

#### 原理：

[(85条消息) logistic回归原理解析及Python应用实例_python中statsmodels.api库多元logistic回归分析怎么解释结果_CHEONG_KG的博客-CSDN博客](https://blog.csdn.net/feilong_csdn/article/details/64128443?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-4-64128443-blog-88933345.235^v38^pc_relevant_sort_base1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromBaidu~Rate-4-64128443-blog-88933345.235^v38^pc_relevant_sort_base1&utm_relevant_index=9)

- 密度函数$f(x)$可以理解为结果为x的概率
- 如果已知模型的密度函数，要求模型参数，可使用最大似然估计法
- 最大似然估计法是让已发生的事情（得到的样本）的概率尽可能大，即让联合概率密度函数的值尽可能大，这个联合概率密度函数就是最大似然函数
- 最大和最小的转换可以通过添加一个负号来实现
- 梯度下降算法是用于求损失函数最小的算法

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230727205109022.png" alt="image-20230727205109022" style="zoom:50%;" />



<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230727205132421.png" alt="image-20230727205132421" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230727205156115.png" alt="image-20230727205156115" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230727205208403.png" alt="image-20230727205208403" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230727205220660.png" alt="image-20230727205220660" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230727205232302.png" alt="image-20230727205232302" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230727205251463.png" alt="image-20230727205251463" style="zoom:50%;" />

#### python代码实现

##### 使用最大似然估计、梯度下降法求系数

```python
import numpy as np

def sigmoid(z):
    return 1 / (1 + np.exp(-z))

def log_likelihood(X, y, w, b): #极大似然估计，这个函数没有用到
    z = np.dot(X, w) + b
    prob = sigmoid(z)
    log_like = np.sum(y*np.log(prob) + (1-y)*np.log(1-prob))
    return -log_like

def logistic_regression(X, y, learning_rate=0.01, epochs=1000):
    n_features = X.shape[1]
    w = np.zeros(n_features)
    b = 0

    for _ in range(epochs):
        z = np.dot(X, w) + b
        prob = sigmoid(z)

        # 计算梯度
        dw = np.dot(X.T, (prob - y)) / len(y)
        db = np.sum(prob - y) / len(y)

        # 参数更新
        w -= learning_rate * dw
        b -= learning_rate * db

    return w, b

def predict(X, w, b):
    # 添加常数项1作为偏置项，扩展特征矩阵X（要进行跟训练数据一样的扩展处理）
    X_extended = np.hstack((np.ones((X.shape[0], 1)), X))

    # 计算预测概率
    z = np.dot(X_extended, w) + b
    prob = sigmoid(z)

    # 根据阈值进行分类预测
    predictions = (prob >= 0.5).astype(int)

    return predictions

# 示例数据
X_train = np.array([[2.3, 3.5], [1.5, 4.2], [3.5, 2.2], [4.2, 5.3], [3.7, 6.7], [6.1, 7.5]])
y_train = np.array([0, 0, 0, 1, 1, 1])

# 添加常数项1作为偏置项，扩展特征矩阵X
X_train_extended = np.hstack((np.ones((X_train.shape[0], 1)), X_train))

# 训练逻辑回归模型，得到系数w和偏置b
coefficients, bias = logistic_regression(X_train_extended, y_train)

print("系数w：", coefficients)
print("偏置b：", bias)

# 预测
w = coefficients
b = bias
X_new = np.array([[1.2, 2.5], [3.1, 4.7], [2.0, 3.0]])
predictions = predict(X_new, w, b)

print("新样本分类预测结果：", predictions)
```


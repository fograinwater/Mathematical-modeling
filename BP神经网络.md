### BP神经网络

#### 算法思想

通过误差反向传播优化网络的权值，使模型的误差减小。

反向传播的策略是按照梯度下降最快的方向

#### 算法流程

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230726131616661.png" alt="image-20230726131616661" style="zoom:67%;" />

#### 网络架构

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20230726131916398.png" alt="image-20230726131916398" style="zoom:50%;" />



#### matlab代码实现

纯纯码：使用**newff()函数**构建BP神经网络

##### newff()函数使用方法：

[(85条消息) Matlab中newff函数使用方法和搭建BP神经网络的方法_Karthus_冲冲冲的博客-CSDN博客](https://blog.csdn.net/weixin_44248258/article/details/122064776)

```matlab
net = newff(data,label,[8,8],{'tansig','purelin'},'trainlm')
```

- data：训练时网络的输入数据。newff函数会把data的一列当作一个样本，如果数据集s是将一行当作一个样本，要输入数据矩阵转置data'

- label：对应输入数据的标签，可看作真实输出。同上，newff函数会把label的一列当作一个样本的标签，如果数据集是一行当作一个样本，记得将你的输入数据矩阵转置label.‘

  （一般而言，data和label都要先进行归一化）

- [8,8]：hiddenLayerSizes，确定隐藏层的层数以及每层的神经单元个数。[8,8]表示包含两个隐藏层，每个隐藏层有8个神经单元。

- {‘tansig’,‘purelin’}：隐藏层所用的激活函数。{‘tansig’,‘purelin’}表示第一层用tansig激活函数，第二个隐藏层用purelin激活函数。

  常见的激活函数：

  ```matlab
  logsig：对数S型函数
  tansig：正切S型函数
  purelin：线性型函数
  ```

- ‘trainlm’：训练函数，默认为trainlm函数，该方法需要占用更大的存储空间，使用了Levenberg-Marquardt算法,对于中等规模的BP神经网络有最快的收敛速度

  常见的训练函数： 

  ```matlab
  traingd：梯度下降算法
  traingdm：带动量的梯度下降算法
  traingda：学习率变化的梯度下降算法
  traingdx：学习率变化带动量的梯度下降算法
  trainrp：RPROP算法，内存需求小，适用于大型网络
  trainoss：OneStep Secant Algorithm，计算量与内存需求较小，适用于大型网络
  ```

-  网络参数的设置：net.trainParam的常用属性：（假定已经定义了一个BP网络net） 
  ```matlab
  %     (1)* net.trainParam.epochs: 最大训练次数 
  %     (2)* net.trainParam.lr: 网络的学习速率 
  %     (3)* net.trainParam.goal: 训练网络所要达到的目标误差 
  %     (4)* net.trainParam.time: 最长训练时间（秒）
  %     (5)* net.trainParam.show: 两次显示之间的训练次数 
  ```



##### 使用示例：

[(85条消息) 菜鸟的数学建模之路（四）：BP神经网络_bp神经网络中的mse_最强菜鸟的博客-CSDN博客](https://blog.csdn.net/qq_40298902/article/details/100903964)

[(85条消息) BP神经网络通俗教程（matlab实现方法）_bp神经网络结构图怎么画_唐BiuBiu的博客-CSDN博客](https://blog.csdn.net/tangbiubiu/article/details/108417780)

```matlab
% % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % 
% matlab实现BP网络步骤(以"BP神经网络.docx"里的公路运输为例)：
% BP网络创建：
% 1.准备好训练集（以矩阵的方式存储）
%   输入层数据：p = [numberOfPeople; numberOfAutomobile; roadArea];
%   输出数据：t = [passengerVolume; freightVolume];
% 2.对训练集中的输入数据矩阵和目标数据矩阵进行归一化处理
%   [pn, inputStr] = mapminmax(p);
%   [tn, outputStr] = mapminmax(t);
% 3.建立BP神经网络
%   net = newff(pn, tn, [3 7 2], {'purelin', 'logsig', 'purelin'});
%   [3 7 2]:3为输入层的节点个数，7为隐含层的“神经元”节点个数（可由l =
%   sqrt(n+m)+a得出，具体可看“BP神经网络.docx”），2为输出层的节点个数
% 4.神经网络参数设置
%   net.trainParam.show = 10;%每10轮回显示一次结果
%   net.trainParam.epochs = 5000;%最大训练次数
%   net.trainParam.lr = 0.05;%网络的学习速率
%   net.trainParam.goal = 0.65 * 10^(-3);%训练网络所要达到的目标误差
%   net.divideFcn = '';%网络误差如果连续6次迭代都没变化，则matlab会默认终止训练。为了让程序继续运行，用以下命令取消这条设置
% 5.开始训练网络
%   net = train(net, pn, tn);
% 到此BP网络训练完成！！！！！
% 
% 
% 使用BP网络进行预测：
% 1.新输入要用于预测的数据
%   newInput = [73.39 75.55; 3.9635 4.0975; 0.9880 1.0268]; 
% 2.利用原始输入数据(训练集的输入数据)的归一化参数对新输入数据进行归一化
%  newInput = mapminmax('apply', newInput, inputStr);
% 3.进行仿真
%  newOutput = sim(net, newInput);
% 4.反归一化得到结果
%  newOutput = mapminmax('reverse',newOutput, outputStr);
%  newOutput为预测的结果，以矩阵的方式存储
% % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % % 


clc
clear
%准备好训练集
%人数(单位：万人)
numberOfPeople=[20.55 22.44 25.37 27.13 29.45 30.10 30.96 34.06 36.42 38.09 39.13 39.99 41.93 44.59 47.30 52.89 55.73 56.76 59.17 60.63];
%机动车数(单位：万辆)
numberOfAutomobile=[0.6 0.75 0.85 0.9 1.05 1.35 1.45 1.6 1.7 1.85 2.15 2.2 2.25 2.35 2.5 2.6 2.7 2.85 2.95 3.1];
%公路面积(单位：万平方公里)
roadArea=[0.09 0.11 0.11 0.14 0.20 0.23 0.23 0.32 0.32 0.34 0.36 0.36 0.38 0.49 0.56 0.59 0.59 0.67 0.69 0.79];
%公路客运量(单位：万人)
passengerVolume = [5126 6217 7730 9145 10460 11387 12353 15750 18304 19836 21024 19490 20433 22598 25107 33442 36836 40548 42927 43462];
%公路货运量(单位：万吨)
freightVolume = [1237 1379 1385 1399 1663 1714 1834 4322 8132 8936 11099 11203 10524 11115 13320 16762 18673 20724 20803 21804];

%输入数据矩阵
p = [numberOfPeople; numberOfAutomobile; roadArea];
%目标（输出）数据矩阵
t = [passengerVolume; freightVolume];

%对训练集中的输入数据矩阵和目标数据矩阵进行归一化处理
[pn, inputStr] = mapminmax(p);
[tn, outputStr] = mapminmax(t);

%建立BP神经网络
net = newff(pn, tn, [3 7 1], {'purelin', 'logsig', 'purelin'});

%每10轮回显示一次结果
net.trainParam.show = 10;

%最大训练次数
net.trainParam.epochs = 5000;

%网络的学习速率
net.trainParam.lr = 0.05;

%训练网络所要达到的目标误差
net.trainParam.goal = 0.65 * 10^(-3);

%网络误差如果连续6次迭代都没变化，则matlab会默认终止训练。为了让程序继续运行，用以下命令取消这条设置
net.divideFcn = '';

%开始训练网络
net = train(net, pn, tn);

%使用训练好的网络，基于训练集的数据对BP网络进行仿真得到网络输出结果
%(因为输入样本（训练集）容量较少，否则一般必须用新鲜数据进行仿真测试)
answer = sim(net, pn);
% 
% %反归一化
answer1 = mapminmax('reverse', answer, outputStr);


%-----------------绘制测试样本神经网络输出和实际样本输出的对比图(figure(1))--------------------
t = 1990:2009;

%测试样本网络输出客运量
a1 = answer1(1,:); 
%测试样本网络输出货运量
a2 = answer1(2,:);

figure(1);
subplot(2, 1, 1); 
plot(t, a1, 'ro', t, passengerVolume, 'b+');
legend('网络输出客运量', '实际客运量');
xlabel('年份'); ylabel('客运量/万人');
title('神经网络客运量学习与测试对比图');
grid on;

subplot(2, 1, 2); plot(t, a2, 'ro', t, freightVolume, 'b+');
legend('网络输出货运量', '实际货运量');
xlabel('年份'); ylabel('货运量/万吨');
title('神经网络货运量学习与测试对比图');
grid on;
%-----------------绘制测试样本神经网络输出和实际样本输出测试结束--------------------



%-----------------开始新输入数据进行预测的对比图(figure(2))--------------------
%使用训练好的神经网络对新输入数据进行预测
%新输入数据(2010年和2011年的相关数据)
newInput = [73.39 75.55; 3.9635 4.0975; 0.9880 1.0268]; 

%利用原始输入数据(训练集的输入数据)的归一化参数对新输入数据进行归一化
newInput = mapminmax('apply', newInput, inputStr);

%进行仿真
newOutput = sim(net, newInput);

%反归一化
newOutput = mapminmax('reverse',newOutput, outputStr);

disp('预测2010和2011年的公路客运量分别为(单位：万人)：');
newOutput(1,:)
disp('预测2010和2011年的公路货运量分别为(单位：万吨)：');
newOutput(2,:)

%在figure(1)的基础上绘制2010和2011年的预测情况-------------------------------------------------------
figure(2);
t1 = 1990:2011;

subplot(2, 1, 1); 
plot(t1, [a1 newOutput(1,:)], 'ro', t, passengerVolume, 'b+');
legend('网络输出客运量', '实际客运量');
xlabel('年份'); ylabel('客运量/万人');
title('神经网络客运量学习与测试对比图(添加了预测数据)');
grid on;

subplot(2, 1, 2); plot(t1, [a2 newOutput(2,:)], 'ro', t, freightVolume, 'b+');
legend('网络输出货运量', '实际货运量');
xlabel('年份'); ylabel('货运量/万吨');
title('神经网络货运量学习与测试对比图(添加了预测数据)');
grid on;
```


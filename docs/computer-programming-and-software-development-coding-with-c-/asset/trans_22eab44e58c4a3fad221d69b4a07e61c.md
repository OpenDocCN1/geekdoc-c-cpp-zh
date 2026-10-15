

一部分处理参数 X 并计算 theta 参数，另一部分激活函数，在本例中为 sigmoid 函数，以计算概率。这就是神经网络中每个节点所做的事情。唯一的区别是，在逻辑回归中，我们使用的是只有一个节点的神经网络。然后我们用以下函数激活 h_θ(X)：

\[
h_\theta(X) = w_0 + \sum_{j=1}^{m} X_{ij} w_j
\]

\[
\hat{y}_i = \sigma(h_\theta(X)) = \frac{1}{1 + e^{-h_\theta(X)}}
\]

现在我们可以得到一些预测。问题在于我们不知道这些预测有多好。为了找到逻辑函数最优的参数 θ，我们需要使用另一个公式来计算函数的成本，即预测结果与实际结果之间的误差。因此，很明显，sigmoid 函数的最佳参数使成本函数最小化。逻辑回归算法的成本函数如下所示：

\[
J(\theta) = -\frac{1}{m} \sum_{i=1}^{m} \left[ y^{(i)} \log(h_\theta(x^{(i)})) + (1 - y^{(i)}) \log(1 - h_\theta(x^{(i)})) \right]
\]

该成本函数寻找的是平均差异，即真实结果、标记数据与预测值之间的误差。逻辑回归算法以及许多其他参数算法都需要优化算法来帮助找到能降低成本函数的最佳 theta 参数。这些优化算法是创造性的过程，违背了使用暴力方法根据成本函数的输出来寻找最佳参数。我们可以使用一些非常棒的优化算法来帮助逻辑回归找到这些 theta 参数，例如 SGD 或 Adam。好消息是，所有主要机器学习框架，如 Keras、TensorFlow、Caffe 和 PyTorch 都已包含它们可供使用，因此只是一个测试问题，看哪个框架表现最好。

以下是使用逻辑回归时你需要记住的一些最重要的要点：

- 我们使用逻辑回归进行二元分类，例如，批准或拒绝，好或坏，生病或健康。
- 你可以使用逻辑回归进行分类；然而，它将是一个分类器。其他算法可以更好地进行分类。
- 请记住，与许多其他 ML 算法一样，输入数据必须是数值型的，因此需要使用编码来编码标签和分类数据。
- 为了获得最佳性能，即分类准确率，输入特征必须尽可能具有正态或高斯分布。
- 逻辑回归假设所有变量，即特征，都是独立的，因此请检查协变量并在可能的情况下将其消除。

我将向你展示我通常使用特定 ML 算法解决问题的步骤。也许我即将展示的内容中的某些东西可以帮助你解决你的问题。

```python
import pandas as pd
import numpy as np

stroke = pd.read_csv("healthcare-dataset-stroke-data.csv")
stroke.dropna(inplace=True)
stroke.head()
```

|   | id | gender | age | hypertension | heart_disease | ever_married | work_type | Residence_type | avg_glucose_level | bmi | smoking_status |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 9046 | Male | 67.0 | 0 | 1 | Yes | Private | Urban | 228.69 | 36.6 | formerly smoked |
| 1 | 31112 | Male | 80.0 | 0 | 1 | Yes | Private | Rural | 105.92 | 32.5 | never smoked |
| 2 | 60182 | Male | 49.0 | 0 | 0 | Yes | Private | Urban | 171.23 | 34.4 | never smoked |
| 3 | 1665 | Female | 79.0 | 1 | 0 | Yes | Self-employed | Rural | 174.12 | 24.0 | never smoked |
| 4 | 56669 | Male | 81.0 | 0 | 0 | Yes | Private | Urban | 186.21 | 29.0 | formerly smoked |

对于第一个分类示例，我将检查逻辑回归算法是否可以根据性别、年龄、各种疾病和吸烟状况等特征预测患者是否可能中风。

![](img/0155736aec718cf18821e9f10a5d308d_239_0.png)

作为良好的实践，始终检查输入数据是否存在异常值、空值或脏数据非常重要。最简单的方法是通过描述数据集。一旦我了解了数据集，我就会进行一些特征工程，删除不相关的列，然后对每个分类特征进行编码。

![](img/0155736aec718cf18821e9f10a5d308d_239_1.png)

你需要记住的一件事是，逻辑回归假设所有变量都是独立的，因此检查特征之间的相关性很重要。特别是当数据遵循正态分布时，该算法的工作效果更好，即执行时间和收敛性。因此，我使用直方图验证特征的分布。

### Normalization

```python
In [7]: from sklearn.preprocessing import StandardScaler

age_scaler = StandardScaler()
stroke['age'] = age_scaler.fit_transform(stroke[['age']])

avg_glucose_level_scaler = StandardScaler()
stroke['avg_glucose_level'] = avg_glucose_level_scaler.fit_transform(stroke[['avg_glucose_level']])

bmi_scaler = StandardScaler()
stroke['bmi'] = bmi_scaler.fit_transform(stroke[['bmi']])
```

```python
In [8]: from sklearn.preprocessing import PowerTransformer
#pt = PowerTransformer()
#pt_data['body_mass_power_trans'] = pt.fit_transform(pt_data[['body_mass_g']])
```

拟合模型前的最后一步是归一化特征，使所有特征具有相似的范围。我现在准备 X 和 y。

### 2. Feature Selection

```python
In [9]: X = stroke.drop(['stroke'], axis=1)
y = stroke['stroke']
```

```python
In [10]: from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.20, random_state=42)
```

### 3. Algorithm

```python
In [12]: from sklearn.linear_model import LogisticRegression

model = LogisticRegression(class_weight='balanced', penalty='l2', solver='liblinear', max_iter=1000)
model.fit(X_train, y_train)
Out[12]: LogisticRegression(class_weight='balanced', max_iter=1000, solver='liblinear')
```

![](img/0155736aec718cf18821e9f10a5d308d_242_0.png)

在这种情况下，散点代表样本所属的真实目标或类别。轮廓代表模型预测。每个标记的颜色代表实际类别，符号代表预测的正确性。点表示样本被正确预测，x 表示样本被错误预测。

## Chapter 6 Naive Bayes & Support Vector Machines

机器学习算法的好处之一是，它们是完美的例子，说明你可以用多种不同的方法解决一个问题。在这种情况下，让我们谈谈朴素贝叶斯分类器，这是一类基于贝叶斯定理并对特征之间存在强，即朴素，独立性假设的简单概率分类器。让我用一个快速的例子来解释。如果我问你，如果你抽一张牌，黑桃 A 在一副牌中出现的频率是多少？好吧，这是一个直接的答案。得到黑桃 A 的概率是已知的，因为每副 52 张牌中只有 1 张。但，如果我们在抽出红桃 A 后抽牌，得到黑桃 A 的概率是多少？好吧，这是一个典型的条件概率示例。它是在我们已经抽出红桃 A 的情况下得到黑桃 A 的概率。我们使用贝叶斯定理求解这种条件概率。贝叶斯定理说明了如果事件 B 首先发生，事件 A 发生的概率。我们这样写公式。


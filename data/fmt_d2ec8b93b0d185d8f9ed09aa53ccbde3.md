
```python
In [3]: import plotly.express as px

fig = px.imshow(
    mushrooms.corr(),
    x=mushrooms.columns,
    y=mushrooms.columns
)

fig.update_layout(height=1000, width=1000)

fig.update_yaxes(showticklabels=False)

fig.update_xaxes(showticklabels=False)

fig.show()
```

我还可以探索特征之间以及特征与标签之间的相关性。

### 直方图

```python
In [4]: import plotly.graph_objects as go
from plotly.subplots import make_subplots

fig = make_subplots(
    rows=(mushrooms.shape[1]//3)+1,
    cols=3,
    subplot_titles=mushrooms.columns
)

for i, col in enumerate(mushrooms.columns):
    fig.add_trace(go.Histogram(x=mushrooms[col], name=col), row=(i//3)+1, col=(i%3)+1)

fig.update_layout(height=2000, showlegend=False)

fig.show()
```

我绘制直方图来查看我拥有的分布，并确定它们是否需要归一化。

![](img/0155736aec718cf18821e9f10a5d308d_254_0.png)

经过所有这些可视化和探索后，我可以执行转换、缩放和归一化，如果需要的话。

#### 4. 预测

```python
from sklearn.metrics import accuracy_score, f1_score, log_loss
```

```python
y_pred = model.predict(X_train)

acc = accuracy_score(y_train, y_pred)
f1 = f1_score(y_train, y_pred)
ll = log_loss(y_train, y_pred)

print(f"(train) accuracy_score: {acc}")
print(f"(train) f1_score: {f1}")
print(f"(train) log_loss: {ll}")

(train) accuracy_score: 0.9898445914756117
(train) f1_score: 0.9893719806763286
(train) log_loss: 0.35075587635849087
```

在这种情况下，一个极其简单的支持向量分类器，在几乎没有任何数据预处理的情况下，就能相当好地预测蘑菇是否可食用，使用支持向量机。

![](img/0155736aec718cf18821e9f10a5d308d_255_0.png)

我可以使用预测轮廓来理解我的模型如何进行预测。在这种情况下，预测相当准确。

### 第 7 章 K 最近邻

`KNN`是最直接的分类算法之一，但它有一个缺点。它必须在每次预测时使用所有数据，如果数据集太大，这可能会很麻烦。让我解释一下原因。`KNN`使用欧几里得或曼哈顿等距离算法来衡量数据集中一个特定条目与所有其他条目之间的距离。例如，如果我们选择`K = 3`的值，我们会说被分析的元素属于`K`个最近邻居中最常见的类别，在本例中为`3`，因为每个元素都需要与每个`K`个邻居进行分析。随着数据集中元素的数量增加，所需的分析次数也会增加，呈指数级增长。要衡量元素之间的距离，有几种不同的方法。

![](img/0155736aec718cf18821e9f10a5d308d_256_0.png)

正如我提到的，欧几里得距离是其中之一。这是公式，给出了两点之间的直线距离。另一方面，曼哈顿，这个公式在这里，寻找最短的实际路径。例如，在棋盘上，有直线和路径。曼哈顿可以考虑所有这些。你可能还想查看的其他距离公式有`Chebyshev`、`WMinkowski`、`SEuclidean`、`Mahalanobis`等。使用`KNN`时需要牢记的一些重要事项。`KNN`如此简单，无需优化算法。它直接且易于解释。它在分类设置中效果非常好。它可用于分类和回归。你可能想要选择合适的距离算法。如果不确定，欧几里得可能就能解决问题，但建立对其他算法的直觉并尝试它们是个好主意。`KNN`在数据很多时很慢，并且没有最佳`K`的配方，但如果你可以尝试偶数，如果类别数为奇数，并且`KNN`对异常值非常敏感。如果可能，请将其删除。`KNN`在不平衡的数据集上表现不佳，因为最近的邻居很可能总是属于示例最多的类别。

#### K-最近邻

#### 何时以及如何使用 K 最近邻

#### 1. 数据

```python
In [1]: import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
```

```python
In [2]: recruitment = pd.read_csv("Placement_Data_Full_Class.csv")
recruitment.drop(['sl_no', 'salary'], axis=1, inplace=True)
recruitment.dropna(inplace=True)
recruitment.head()
```

下一个分类算法是`KNN`，对于这个示例，我将预测学生在特定校园的安置情况。这些是我数据中包含的列。

列描述：

- `gender` : 性别- 男性=`'M'`，女性=`'F'`
- `ssc_p` : 中学教育百分比- 10 年级
- `ssc_b` : 教育委员会- 中央/其他
- `hsc_p` : 高中教育百分比- 12 年级
- `hsc_b` : 教育委员会- 中央/其他
- `hsc_s` : 高中教育专业
- `degree_p` : 学位百分比
- `degree_t` : 本科（学位类型）- 学位教育领域
- `workex` : 工作经验
- `etest_p` : 就业能力测试百分比（由学院进行）
- `specialisation` : 研究生（MBA）- 专业
- `mba_p` : MBA 百分比
- `status` : 安置状态- 已安置/未安置
- `salary` : 企业向候选人提供的薪资

现在，让我们开始预测`status`，它是名义且分类的。

1. 我们想要预测什么变量？

   学生的状态

我将执行归一化，因为`KNN`是一个几何算法。

#### 归一化

```python
In [6]: from sklearn.preprocessing import StandardScaler

ssc_p_scaler = StandardScaler()
recruitment['ssc_p'] = ssc_p_scaler.fit_transform(recruitment[['ssc_p']])

hsc_p_scaler = StandardScaler()
recruitment['hsc_p'] = hsc_p_scaler.fit_transform(recruitment[['hsc_p']])

degree_p_scaler = StandardScaler()
recruitment['degree_p'] = degree_p_scaler.fit_transform(recruitment[['degree_p']])

mba_p_scaler = StandardScaler()
recruitment['mba_p'] = mba_p_scaler.fit_transform(recruitment[['mba_p']])
```

这意味着它对不同范围内的异常值很敏感。然后我进行了一点特征选择。

#### 3. 算法

```python
In [10]: from sklearn.neighbors import KNeighborsClassifier
```

```python
In [11]: model = KNeighborsClassifier(n_neighbors=3, weights='distance')
model.fit(X, y)
Out[11]: KNeighborsClassifier(n_neighbors=3, weights='distance')
```

最后，我现在使用`KNN`算法创建模型，将值设置为`3`。这就是分析时将使用的邻居数量。

#### 4. 预测

```python
In [12]: from sklearn.metrics import accuracy_score, f1_score, log_loss
```

```python
In [13]: y_pred = model.predict(X_train)
acc = accuracy_score(y_train, y_pred)
f1 = f1_score(y_train, y_pred)
ll = log_loss(y_train, y_pred)
print(f"(train) accuracy_score: {acc}")
print(f"(train) f1_score: {f1}")
print(f"(train) log_loss: {ll}")
(train) accuracy_score: 1.0
(train) f1_score: 1.0
(train) log_loss: 9.992007221626413e-16
```

```python
In [14]: y_pred = model.predict(X_test)
acc = accuracy_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)
ll = log_loss(y_test, y_pred)
print(f"(test) accuracy_score: {acc}")
print(f"(test) f1_score: {f1}")
```

邻居的数量起着非常重要的作用，如果这个数字有点高并且数据集相对较大，则分析的数量可能会爆炸，并且过程会相当缓慢。正如我刚才向你展示的那样，两类元素的彼此之间非常相似，因此我们可以准确预测某人是否会被安置，只要根据其他人的状态信息即可。

### 第 8 章 决策树和随机森林

决策树是一种决策支持工具，它使用决策及其可能后果的模型。例如，我们可以使用决策树来确定今天是否可以打网球。我们做出的每个决定都会让我们更接近是或否。在每个阶段，都有多种方式来分割树。那么，算法如何确定分割条件呢？选择分割的方法有很多。其中两种最流行的方法是基尼系数和信息熵。两个公式都计算数据上的分布，并找到哪个条件产生最高的 不平等。换句话说，我们查看应用基尼或熵，以查看集合中哪个元素的公式值最低。这是不平等最高。元素随后被认为是分割条件。有几件事会影响分割，例如所需的高度，即深度，叶子的数量或分割函数。这可能导致一棵树可以转变为许多不同的树。单个决策树被认为是一个弱分类器，因为只有一种方法可以分离树。那么，如果你使用不同的标准创建多个树，比如函数或分割条件来生成同一棵树的 100 个变体，会发生什么？这就引出了一个新的概念，随机森林。随机森林是生成了 n 次的决策树。最后，我们将所有生成树的 结果组合起来，每棵树为每个元素投票给特定类别。所有树投票的组合使随机森林成为一个强分类器。随机森林只是一堆普通的决策树投票以

#### 相关性

```python
In [3]: import seaborn as sns
import matplotlib.pyplot as plt

sns.set(rc = {'figure.figsize':(15, 10)})

sns.heatmap(water.corr(), annot=True);
```

![](img/0155736aec718cf18821e9f10a5d308d_265_0.png)

一如既往，探索数据是一个良好的实践，了解特征之间的相关性及其分布，使用直方图。

![](img/0155736aec718cf18821e9f10a5d308d_266_0.png)

值得注意的是，这些特征具有相当正常的分布。然而，算法对脏数据集非常有抵抗力。在这种情况下，一切看起来都不错。

#### 3. 算法

```python
In [7]: from sklearn.ensemble import RandomForestClassifier
model = RandomForestClassifier()
model.fit(X_train, y_train)

Out[7]: RandomForestClassifier()
```

我分割了数据集并训练随机森林分类算法。让我们看看它的表现如何。

```python
In [9]: y_pred = model.predict(X_train)

acc = accuracy_score(y_train, y_pred)
f1 = f1_score(y_train, y_pred)
ll = log_loss(y_train, y_pred)

print(f"(train) accuracy_score: {acc}")
print(f"(train) f1_score: {f1}")
print(f"(train) log_loss: {ll}")
```

(train) accuracy_score: 1.0

(train) f1_score: 1.0

(train) log_loss: 9.992007221626413e-16

```python
In [10]: y_pred = model.predict(X_test)

acc = accuracy_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)
ll = log_loss(y_test, y_pred)

print(f"(test) accuracy_score: {acc}")
print(f"(test) f1_score: {f1}")
print(f"(test) log_loss: {ll}")
```

(test) accuracy_score: 0.652605459057072

(test) f1_score: 0.49640287769784175

(test) log_loss: 11.998655782611447

为此，我检查了训练和测试的准确率分数。训练分数为 1，但测试为 0.65。的确，正如我刚才提到的，这种算法很容易过拟合。

#### 分类报告

```python
from sklearn.metrics import classification_report

y_pred = model.predict(X)

print(classification_report(y, y_pred, target_names=['Safe for Human', 'Not Potable'], zero_division=0))
```

|  | precision | recall | f1-score | support |
|---|---:|---:|---:|---:|
| Safe for Human | 0.92 | 0.97 | 0.94 | 1200 |
| Not Potable | 0.95 | 0.87 | 0.91 | 811 |
| accuracy |  |  | 0.93 | 2011 |
| macro avg | 0.93 | 0.92 | 0.93 | 2011 |
| weighted avg | 0.93 | 0.93 | 0.93 | 2011 |

这里也发生了这种情况，这可能表明我可以尝试另一种算法，考虑到所涉及的风险，这可能是有意义的。基本上，如果模型预测水不安全而实际上是安全的，没人会受伤。但另一方面，如果我们的模型说你可以喝水而实际上不安全，有人可能会生病，甚至更糟，死亡。

![](img/0155736aec718cf18821e9f10a5d308d_268_0.png)

查看最终的图，可饮用和不安全的水样彼此非常接近。我们可以从算法中获得的最有用的信息之一是特征重要性。在这里，我们可以观察到一些特征对于确定一个样本是否属于类别 A 或类别 B 更相关。

### 第 9 章 神经网络

当我向你展示逻辑回归时，我向你展示了一个单节点神经网络。与人类神经元相比，我们假设一组输入，我们称之为 `X` 值，结合一组权重，我们称之为 `W`，将产生一个信号，该信号可以被一个函数放大或减弱。这个函数称为激活函数。

![](img/0155736aec718cf18821e9f10a5d308d_270_0.png)

正如你在这个图中看到的，我们可能有一个单节点神经网络，它会将所有 `X` 值乘以 `W` 权重，就像线性回归中一样，此操作的 结果然后传递给激活函数。在这种情况下，激活函数是 S 形函数，计算 `X` 值属于类别 0 或 1 的概率。虽然这是最直接的神经网络，但它并不强大。当添加更多神经元和层时，神经网络可以发展出非常灵活的决策边界和强大的分类能力。这就引出了深度学习的概念。

![](img/0155736aec718cf18821e9f10a5d308d_271_0.png)

深度学习不过是具有多于一层且具有多个节点的神经网络。看下面的图作为示例。正如你所观察到的，添加更多节点会增加复杂性，其背后的数学并不复杂，但如果与神经网络相比，它会很棘手。以下是你需要从深度学习架构中了解的一些事情，例如图中所示的架构。神经网络是参数化的，因此 `W` 权重相当于逻辑回归中的 `theta` 参数。这意味着你需要一个优化算法来帮助你获得这些参数，例如随机梯度下降或 `Adam`。没有关于你可以添加多少层的配方。这是试错，或者也许我们可以称之为实验。深度学习神经网络使用两种主要算法，前向传播来计算神经网络的输出，也就是最终的概率，以及反向传播，它学习真实类别与预测类别之间的误差。反向传播在每次迭代中调整 `W` 权重以减少误差。顺便说一下，神经网络中的每次训练迭代称为一个 `epoch`。

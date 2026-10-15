
预测响应 $\hat{y}$。目标是使 $J(\beta)$ 最小化，仅此而已。实现起来并不难，但非常高效。在前面的例子中，我们能够做出良好的预测，但仍远未达到最佳效果。如何改进这个模型？只要快速看一下这张图，尽管线性回归似乎能提供不错的预测，但我能看出数据看起来更像一条曲线，而不是直线。

![](img/0155736aec718cf18821e9f10a5d308d_221_0.png)

为了更清楚地说明这一点，我回到数据，选取更少的特征，然后绘图。确实，现在更明显的是，曲线能做得更好。

![](img/0155736aec718cf18821e9f10a5d308d_223_0.png)

同时使用训练数据和测试数据来检查。看这条曲线，预测现在更好地拟合了输入数据。现在，用新数据做出的预测更加准确。

## 模型质量

```python
In [97]: from sklearn.metrics import mean_absolute_error

y_pred_train = model.predict(np.array(X_train).reshape(-1,1))
y_pred_test = model.predict(np.array(X_test).reshape(-1,1))

training_set_MAE = mean_absolute_error(y_train, y_pred_train)
test_set_MAE = mean_absolute_error(y_test, y_pred_test)

print('Training set MAE', training_set_MAE)
print('Test set MAE', test_set_MAE)
```

Training set MAE 85.605640636258
Test set MAE 70.89259587638183

我检查了平均绝对误差，我们的误差指标降低了近 20%，与之前的指标相比，准确度提高了很多。

简单线性回归和多项式回归都表现良好；然而，在某些情况下，你可能需要更多的功能。在这里，让我介绍 Lasso。Lasso 是线性回归的一种扩展。简单线性回归会尽最大努力为模型拟合一条直线，该模型会考虑所有数据点，即特征；但是，如果数据中存在离群值，它们会使线性回归线向离群值移动。例如，如果你有大量中等收入房屋的价格列表，同时还有迈克尔·乔丹的房屋，那么预测就不会太准确。为了改进预测，可以添加一个惩罚项，即正则化项，来找到最佳的 beta 参数，以防止这种情况发生。关于 Lasso 回归，需要了解的一些重要事项是：它有助于减少数据集中的特征数量；它会将其中一些特征变为 0。L1 正则化可以对抗过拟合，并会创建一个更松散的模型。L1 提高了泛化能力。L1 正则化适用于线性回归和多项式回归。让我们在较高层面上简要探讨 Lasso（即 L1）正则化。还记得我们的线性回归方程吗？

![](img/0155736aec718cf18821e9f10a5d308d_224_0.png)

我们可以这样重写它，并重用线性回归的代价函数 $J(\beta)$，加上 L1 惩罚项。如果 $\lambda$ 等于 0，那么这就是简单线性回归；这意味着我们可以通过调整 lambda 的值来调整拟合。请记住，有些库将变量 lambda 称为 alpha。当 lambda 取较小值（例如 0.0001）时，L1 惩罚项会导致某些 beta 系数变为 0；这也会导致某些 $x_j\beta_j$ 多项式项变为 0。换句话说，Lasso 会自动进行特征选择，通过移除（即变为 0）那些对模型拟合没有贡献的特征。多项式回归提高了我们模型的准确性，我们可以尝试使用更大的多项式次数，但在新数据上可能效果不佳，因为模型可能过拟合。

```python
In [19]: from sklearn.preprocessing import PolynomialFeatures
from sklearn.model_selection import train_test_split
from sklearn.pipeline import make_pipeline
from sklearn import linear_model

degree = 3

X_train, X_test, y_train, y_test = train_test_split(x_width, y_weight, test_size=0.30, random_state=42)
model = make_pipeline(PolynomialFeatures(degree), linear_model.Lasso(alpha=1.5, max_iter=1500, tol=0.01))

x_tr = np.array(X_train).reshape(-1,1)
y_tr = np.array(y_train).reshape(-1,1)
model.fit(x_tr, y_tr)

#predict
x_ts = np.array(X_test).reshape(-1,1)
y_ts = np.array(y_test).reshape(-1,1)

y_pred = model.predict(x_ts)

plt.title('Test Set - Polynomial Degree 3')
plt.xlabel('Width (X)')
plt.ylabel('Weight (y)')
plt.scatter(X_test, y_test)
plt.scatter(x_ts, y_pred, c="green", marker='.')
plt.show()
```

对于这些场景，我们还可以做其他事情，例如使用 Lasso 回归。让我们看看在鱼类样本中如何使用 Lasso。我们将 alpha 的值设置为 1.5；这样，我们可以使用所有特征和一个多项式次数。该算法会自行丢弃特征。

![](img/0155736aec718cf18821e9f10a5d308d_226_0.png)

你可以看到，我们的预测并非完全线性，但也不是多项式形式。该算法找到了一个中间状态，既能良好预测，又不会过于复杂。

## 第 4 章 岭回归与感知机回归

岭回归与 Lasso 一样，也是线性回归的一种扩展。从宏观角度来看，Lasso（即 L1 正则化）会使一些系数变为 0，从而完全移除它们。当只有少数参数显著而其余参数不显著时，即只有少数预测变量影响响应时，这种技术效果很好。如果有一些参数不应该被移除，而应该被缩小，那么你应该使用岭回归。对于 L2（即岭回归），beta 系数可以取一些值，但不会完全为 0。换句话说，L1 移除系数，而 L2 保留它们，但以最小的值使它们留在方程中。关于岭回归需要记住的一些重要事项：它保留模型中的所有特征，不像 Lasso 那样进行特征选择，当你需要保留所有特征时非常有用。L2 公式是什么样的？如果你还记得我们的线性回归方程，我们可以将其重写如下，然后使用线性回归的代价函数 $J(\beta)$，并加上 L2 惩罚项。如果 $\lambda$ 等于 0，那么这就是简单线性回归。可以通过调整 lambda 的值来调整它。

$$\hat{y} = \beta_0 \cdot 1 + \beta_1 x_1 + \beta_2 x_2 + \dots + \beta_k x_k$$

$$\hat{y}_i = \beta_0 + \sum_{j=1}^{m} x_j \beta_j$$

$$J(\beta) = \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 + \lambda \sum_{j=1}^{m} (\beta_j)^2$$

当 lambda 取较小值（例如 0.0001）时，L2 惩罚项会使一些 beta 系数非常接近 0，但不会等于 0。换句话说，这就是岭回归如何保留模型中的所有特征，即使它们非常小。

```python
In [4]: from sklearn.preprocessing import PolynomialFeatures
from sklearn.model_selection import train_test_split
from sklearn.pipeline import make_pipeline
from sklearn.linear_model import Ridge

degree = 3

X_train, X_test, y_train, y_test = train_test_split(x_width, y_weight, test_size=0.30, random_state=42)
model = make_pipeline(PolynomialFeatures(degree), Ridge(alpha=1.5, max_iter=1500, tol=0.01))

x_tr = np.array(X_train).reshape(-1,1)
y_tr = np.array(y_train).reshape(-1,1)
model.fit(x_tr, y_tr)

#predict
x_ts = np.array(X_test).reshape(-1,1)
y_ts = np.array(y_test).reshape(-1,1)

y_pred = model.predict(x_ts)

plt.title('Test Set - Polynomial Degree 3')
plt.xlabel('Width (X)')
plt.ylabel('Weight (y)')
plt.scatter(X_test, y_test)
plt.scatter(x_ts, y_pred, c="green", marker='.')
plt.show()
```

如前所述，岭回归的工作原理与 Lasso 非常相似，但主要区别在于 Lasso 可以通过将系数设为 0 来将某个特征归零或忽略。岭回归不会使系数变为 0。它不会移除特征。相反，它会为不太重要的特征分配非常低的系数，这在自变量高度相关时非常有用。下面是你如何在 sklearn 中使用岭回归。

![](img/0155736aec718cf18821e9f10a5d308d_229_0.png)

预测线既不是线性的，也不是多项式的，但预测结果可能会比其他更简单的方法有所改进。当然，这完全取决于你的数据。

之前的算法效果不错，但故事并未就此结束。还有其他算法可以使用，例如感知机，它是在 20 世纪 50 年代和 60 年代发展起来的。你可以在 1969 年 Marvin Minsky 和 Seymour Papert 所著的《感知机》一书中了解它。感知机是一种具有单个隐藏层的简单神经网络。最初，感知机被用作二元分类器，但如果不对特征和权重的点积应用激活函数，感知机算法的行为与线性回归非常相似。


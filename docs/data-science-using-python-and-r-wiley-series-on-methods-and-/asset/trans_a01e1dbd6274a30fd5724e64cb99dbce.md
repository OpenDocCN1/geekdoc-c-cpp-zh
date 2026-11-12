
要运行 PCA，我们必须先安装并打开 *psych* 包。

```
install.packages("psych"); library(psych)
```

打开包后，我们使用 *principal()* 命令执行 PCA。

```
pca01 <- principal(r = X_z, rotate = "varimax", nfactors = 5)
```

我们使用带有三个输入值的 *principal()* 命令。输入 r = X_z 指定我们要分析的变量。rotate = "varimax" 告诉 R 在呈现结果前对组件执行 varimax 旋转。最后，nfactors = 5 输入表示我们想要五个组件。我们将 PCA 输出保存为 pca01。

我们关注 pca01 结果的载荷。

```
print(pca01$loadings, cutoff = 0.49)
```

我们使用 cutoff = 0.49 来抑制较小的 PCA 权重。上述代码生成的输出如图 12.8 所示。

要创建特征值图，我们需要旋转组件的特征值。这些值位于图 12.8 的 "SS Loadings" 下方。将这些值保存为独立向量后，使用 plot() 命令绘制它们。

```
ss.load <- c(1.566, 1.045, 1.035, 1.006, 0.348)
plot(ss.load, type = "b", main = "Plot of Eigenvalues",
ylab = "Value",
xlab = "Component"); abline(h = 1, lty = 2)
```

输入 type = "b" 使用点和连接线同时绘制特征值。main、xlab 和 ylab 输入自定义标题和轴标签。abline() 命令向图中添加一条线。输入值 h = 1 添加水平位置为 1 的线，输入 lty = 2 指定虚线。结果如图 12.9 所示。

要比较无旋转与 varimax 旋转的结果，请使用 rotate = "none" 运行 principal() 命令以进行无旋转，使用 rotate = "varimax" 进行 varimax 旋转。

```
pca02_notorot <- principal(r = X, rotate = "none",
nfactors = 4)
print(pca02_notorot$loadings, cutoff = 0.5)
pca02_rot <- principal(r = X, rotate = "varimax",
nfactors = 4)
print(pca02_rot$loadings, cutoff = 0.5)
```

*pca02_notorot$loadings* 的 *print()* 输出摘录如图 12.10a 所示，而 *pca02_rot$loadings* 的 *print()* 输出摘录如图 12.10b 所示。请注意，两个命令都使用 *cutoff = 0.5* 来抑制低于 0.5 的权重。

要验证 PCA 结果，请在测试数据上运行该算法。首先，标准化数据。

```
X_test_z <- scale(X_test)
```

然后，确认推荐四个组件。

```
pca02_test <- principal(r = X_test_z, rotate =
"varimax", nfactors = 5)
pca02_test$loadings
```

输出摘录如图 12.11 所示。确认推荐四个组件后，检查组件权重。

```
pca02_test <- principal(r = X_test_z, rotate =
"varimax", nfactors = 4)
print(pca02_test$loadings, cutoff = 0.5)
```

输出摘录如图 12.12 所示。

要获取训练数据集中组件的相关性，请在 **pca02_rot** 的得分上运行 **round(cor())** 命令。

```
round(cor(pca02_rot$scores),2)
```

在此例中，我们保留两位有效数字。结果如图 12.13 所示。要将目标变量回归到组件上，您可能希望将每个组件保存为独立变量。如下所示。

```
PC1 <- pca02_rot$scores[,1]; PC2 <- pca02_rot$scores[,2]
PC3 <- pca02_rot$scores[,3]; PC4 <- pca02_rot$scores[,4]
```

现在您可以运行回归模型并获取 VIF。代码如下所示。

```
model.pca <- lm(y ~ PC1 + PC2 + PC3 + PC4) ; vif(model.pca)
```

vif() 命令的输出如图 12.14 所示。

## 12.11 多重共线性何时不是问题？

现在，取决于分析师面临的任务，多重共线性实际上可能并非致命缺陷。Weiss 指出，多重共线性“不会不利影响样本回归方程预测响应变量的能力”。他补充说，多重共线性不会显著影响目标变量的点估计、平均响应值的置信区间或随机选择的响应值的预测区间。然而，数据科学家必须因此将多重共线性模型的使用严格限制在目标变量的估计和预测上。在存在多重共线性的情况下，模型解释将不合适，因为单个系数可能没有意义。总结来说，未考虑多重共线性的模型可用于估计，但不可用于描述或解释。

## 参考文献

car 包的名称代表应用回归伴侣，详情可在此处找到：John Fox 和 Sanford Weisberg。An {R} Companion to Applied Regression，第二版，Sage，Thousand Oaks，CA，2011。psych 包（让我们能够进行带有 varimax 旋转的 PCA）的文档可在此处找到：W. Revelle。Psych: Procedures for Personality and Psychological Research，Northwestern University，Evanston，IL，2018。

## 练习

### 澄清概念

- 1. 在数据科学中，高维性是什么意思？
- 2. 为什么我们需要降维方法？
- 3. 主成分用什么取代原来的 m 个预测变量？
- 4. 哪个主成分解释了最多的变异性？
- 5. 其他哪个主成分与第一个主成分相关？
- 6. 为什么我们使用旋转？
- 7. 解释特征值准则？
- 8. 什么是解释方差比例准则？
- 9. 判断正误：不需要对主成分进行验证。
- 10. 当我们将主成分用作回归模型中的预测变量时，VIF 取什么值？这表示什么？

### 使用数据

对于以下练习，请使用 clothing_store_PCA_training 和 clothing_store_PCA_test 数据集。使用 Python 或 R 解决每个问题。

- 11. 标准化或归一化预测变量。
- 12. 为预测变量 Purchase Visits、Days on File、Days between Purchases、Different Items Purchased 和 Days since Purchase 构建相关矩阵。哪些变量高度相关？
- 13. 计算每个预测变量的 VIF。哪个预测变量的 VIF 表明多重共线性是一个问题？
- 14. 使用 varimax 旋转和五个组件运行 PCA。一个组件解释了多少百分比的变异性？两个组件呢？所有五个组件呢？
- 15. 绘制特征值图。使用特征值准则，你会保留多少个组件？
- 16. 假设我们想要解释至少 80% 的变异性。你会保留多少个组件？
- 17. 使用 varimax 旋转和四个组件运行 PCA。四个组件解释了多少百分比的变异性？
- 18. 每个组件包含哪些变量？
- 19. 将四个组件用作回归模型中的预测变量来估计 Sales per Visit。四个组件的回归系数是多少？
- 20. 回归模型中四个组件的 VIF 是多少？

### 实践分析

对于以下练习，请使用 cereals 数据集。使用 Python 或 R 解决每个问题。

- 21. 标准化或归一化预测变量 Sugars、Fiber 和 Potass。
- 22. 为 Sugars、Fiber 和 Potass 构建相关矩阵。哪些变量高度相关？
- 23. 构建回归模型以根据 Sugars、Fiber 和 Potass 估计 Rating。从模型中获取 VIF。哪些 VIF 表明多重共线性是一个问题？
- 24. 使用 varimax 旋转和三个组件运行 PCA。一个组件解释了多少百分比的变异性？两个组件呢？所有三个组件呢？
- 25. 绘制三个组件的特征值图。使用特征值准则，你会保留多少个组件？
- 26. 假设我们想要解释至少 70% 的变异性。你会保留多少个组件？
- 27. 使用 varimax 旋转和两个组件运行 PCA。两个组件解释了多少百分比的变异性？
- 28. 组件 1 包含哪些变量？组件 2 包含哪些变量？
- 29. 将两个组件用作回归模型中的预测变量来估计 Rating。两个组件的回归系数是多少？
- 30. 回归模型中两个组件的 VIF 是多少？

对于以下练习，请使用 red_wine_PCA_training 和 red_wine_PCA_test 数据集。使用 Python 或 R 解决每个问题。目标变量是葡萄酒质量。预测变量是酒精、残糖、pH 值、密度和固定酸度。



addmargins()命令的结果显示在图8.2的列联表中。

我们还可以创建图8.3中所示的并排条形图。核心代码是ggplot()代码，本文前面已介绍过。但是，为了将图表并排放置，我们将调整核心代码。

首先，安装允许我们将图表并排放置的包：gridExtra包。

```
install.packages("gridExtra"); library(gridExtra)
```

然后，运行如所示的ggplot()代码。

```
plot1 <- ggplot(wine_tr, aes(Type)) + geom_bar(aes(fill =
Alcohol_flag), position = "fill") +
ylab("Proportion")
```

```
plot2 <- ggplot(wine_tr, aes(Type)) + geom_bar(aes(fill =
Sugar_flag), position = "fill") +
ylab("Proportion")
```

```
grid.arrange(plot1, plot2, nrow = 1)
```

ggplot()代码本身来自第4章，应该很熟悉。请注意，我们为每个图保存自己的名称；plot1用于Alcohol_flag叠加，plot2用于Sugar_flag叠加。保存每个图后，我们运行grid.arrange()命令，包含三个输入值：plot1、plot2和nrow = 1，以指定我们希望图表在一行中并排显示。结果显示在图8.3的并排图表中。

现在我们有了列联表和图表，接下来进入朴素贝叶斯算法。e1071包包含朴素贝叶斯分类算法。安装并打开该包。

```
install.packages("e1071"); library(e1071)
```

运行朴素贝叶斯估计器。

```
nb01 <- naiveBayes(formula = Type ~ Alcohol_flag +
Sugar_flag, data = wine_tr)
```

naiveBayes()命令将构建模型。formula输入将波浪号左侧的目标变量Type和波浪号右侧的两个预测变量Alcohol_flag和Sugar_flag（用加号分隔）作为输入。data输入指定这些变量来源的数据集。我们将模型保存为nb01。

要观察朴素贝叶斯模型中使用的先验概率和条件概率，请单独运行模型名称。

```
nb01
```

离散预测器的朴素贝叶斯分类器
调用：
naiveBayes.default(x = X, y = Y, laplace = laplace)

先验概率：

| Y | 概率 |
|---|-------------|
| Red | 0.5 |
| White | 0.5 |

条件概率：

Alcohol_flag

| Y | High | Low |
|---|------|-----|
| Red | 0.436 | 0.564 |
| White | 0.536 | 0.464 |

Sugar_flag

| Y | High | Low |
|---|------|-----|
| Red | 0.232 | 0.768 |
| White | 0.600 | 0.400 |

图8.7 R中朴素贝叶斯模型的输出。

输出显示在图8.7中。

输出中两个主要关注项是**先验概率**和**条件概率**。先验概率是p(Y)的值，条件概率是p(X|Y)的结果值。

要预测测试数据集中每种葡萄酒的类型，我们使用**predict()**命令

```
ypred <- predict(object = nb01, newdata = wine_test)
```

object = nb01指定我们使用的是我们的朴素贝叶斯模型，newdata = wine_test说明要使用的测试数据集。该算法将测试数据集中的每条记录分类为白葡萄酒或红葡萄酒，并将分类字符串保存为ypred。

最后，我们创建实际与预测葡萄酒类型的列联表。

```
t.preds <- table(wine_test$Type, ypred)
rownames(t.preds) <- c("Actual: Red", "Actual: White")
colnames(t.preds) <- c("Predicted: Red", "Predicted: White")
addmargins(a = t.preds, FUN = list(Total = sum), quiet = TRUE)
```

addmargins()命令的结果显示在图8.4中。

## 参考文献

我们使用了一个新包gridExtra来格式化多个ggplot图表。如果您想了解新包的内部工作原理的更多细节，请查看此处：Baptiste Auguie, gridExtra: “Grid”图形的杂项函数。R包版本2.3，2017年。https://CRAN.R-project.org/package=gridExtra.

e1071包远不止朴素贝叶斯！有关完整描述，请参阅引用：David Meyer, Evgenia Dimitriadou, Kurt Hornik, Andreas Weingessel, 和 Friedrich Leisch, e1071: 维也纳科技大学统计学、概率论小组（原E1071）的杂项函数。R包版本1.6-8，2017年。http://CRAN.R-project.org/package=e1071.

## 练习

### 澄清概念

- 1. 贝叶斯定理使用什么信息来更新我们对数据参数的先前知识？
- 2. 先验概率代表什么？
- 3. 什么公式表示数据在目标变量的类别值内的表现？
- 4. 什么公式表示数据在不参考类别值的情况下的表现？
- 5. 上一练习中的公式称为什么？
- 6. 后验概率代表什么？
- 7. 如果我们对参数没有任何先验知识，使用什么作为先验概率？
- 8. 最大后验假设如何帮助我们对记录进行分类？
- 9. 类条件独立性假设是什么？
- 10. 如果有多个预测变量，当有两个预测变量X = [X1, x2, X3]时，如何写出p(X|Y = y')？

### 使用数据

对于以下练习，使用wine_flag_training和wine_flag_test数据集。使用Python或R解决每个问题。

- 11. 创建两个列联表，一个包含Type和Alcohol_flag，另一个包含Type和Sugar_flag。
- 12. 使用上一练习中的表格计算：
  - a. Type = Red和Type = White的先验概率。
  - b. 高和低酒精含量的概率。
  - c. 高和低糖含量的概率。
  - d. 条件概率p(Alcohol_flag = High| Type = Red)和p(Alcohol_flag = Low| Type = Red)。
  - e. 条件概率p(Alcohol_flag = High| Type = White)和p(Alcohol_flag = Low| Type = White)。
  - f. 条件概率p(Sugar_flag = High | Type = Red)和p(Sugar_flag = Low | Type = Red)。
  - g. 条件概率p(Sugar_flag = High | Type = White)和p(Sugar_flag = Low | Type = White)。

- 13. 使用上一练习中的概率讨论：
  - a. 随机选取的葡萄酒是红葡萄酒的可能性有多大。
  - b. 随机选取的葡萄酒具有高酒精含量的可能性有多大。
  - c. 随机选取的葡萄酒具有低糖含量的可能性有多大。

- 14. 使用之前找到的条件概率讨论：
  - a. 典型白葡萄酒的酒精和糖含量可能是多少。
  - b. 典型红葡萄酒的酒精和糖含量可能是多少。

- 15. 为Type创建并排条形图，一个叠加Alcohol_flag，另一个叠加Sugar_flag。将图表与您计算的条件概率进行比较。

- 16. 计算酒精含量低且糖含量高的葡萄酒的Type = Red的后验概率。计算同一葡萄酒的Type = White的后验概率。

- 17. 使用您对上一练习的回答，确定对于酒精含量低且糖含量高的葡萄酒，红葡萄酒还是白葡萄酒更可能。朴素贝叶斯分类器会将此葡萄酒分类为什么类型？

- 18. 计算酒精含量高且糖含量低的葡萄酒的Type = Red的后验概率。计算同一葡萄酒的Type = White的后验概率。

- 19. 使用您对上一练习的回答，确定对于酒精含量高且糖含量低的葡萄酒，红葡萄酒还是白葡萄酒更可能。朴素贝叶斯分类器会将此葡萄酒分类为什么类型？

- 20. 运行朴素贝叶斯分类器，根据酒精和糖含量将葡萄酒分类为白葡萄酒或红葡萄酒。

- 21. 在wines_test数据集上评估朴素贝叶斯模型。在列联表中显示结果。编辑表格的行名和列名，使表格更易读。包含总计行和列。

- 22. 根据您在上一练习中的表格，找出朴素贝叶斯模型的以下值：
  - a. 准确率
  - b. 错误率

- 23. 根据您的列联表，找出朴素贝叶斯模型的以下值：
  - a. 它正确分类红葡萄酒的频率。
  - b. 它正确分类白葡萄酒的频率。


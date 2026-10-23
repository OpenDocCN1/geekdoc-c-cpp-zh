

### 图 5.12 扩展估计表

![](img/a858f3b35ed4923af65c22e8829ee5a8_94_0.png)

将扩展估计与此模型的预测公式进行比较，如下所示。

```
16.9641526057058
+Match(Method) {"Alpha Amalyze" => -6.1326090308367, "Caustic Soda" => 4.55240663376582, "Pumice Stone" => 1.58020239707087, else => .}
+0.0465825281069*Size of Load (lbs)
+Match(Sand blasted?) {"no" => -1.8002952999013, "yes" => 1.80029529990132, else => .}
```

## 自定义检验

在入门统计学课程中，原假设通常关于一个变量，经常假设某个参数为零。然而，可以检验比这更复杂的原假设。例如，检验多个参数为零、为一或为其他值是合理的，或者检验某些参数等于其他参数。这些检验在统计学中称为广义线性假设，并使用 JMP 的 Custom Test 命令进行检验。

要进行自定义假设检验，请从 Estimates 弹出菜单中选择 **Custom Test**，将显示如图 5.13 所示的对话框。

### 图 5.13 自定义检验启动

您可以为此检验输入描述性标签——如果您进行多个检验，这很有用。

![](img/a858f3b35ed4923af65c22e8829ee5a8_94_1.png)

Custom Test 标题栏下方的空间是用于输入检验名称的可编辑区域。

Parameter 列出模型参数的名称。在参数列表右侧是对应于这些参数的零列。单击这些单元格以输入对应于所需检验的假设参数值。

其中一个参数标记为“=”。在其右侧的编辑框中，输入您要检验对比的值。例如，您可能要检验某些因子组合之和为 1。您将在此对话框中“=”旁边输入 1。

**Add Column** 添加另一列零，以便可以联合检验参数的多个线性函数。使用 **Add Column** 按钮根据需要向检验添加尽可能多的列。

当检验被指定时，单击 **Done** 以查看检验的执行结果。结果将附加到对话框底部。

完成自定义检验后，报告列出检验名称、所检验参数的函数值、标准误差以及对话框中每个检验列的其他统计量。所有列的联合 F 检验位于底部。对自定义检验（检验负载大小系数是否等于 1）的示例输出显示在图 5.14 中。

### 图 5.14 自定义检验输出

![](img/a858f3b35ed4923af65c22e8829ee5a8_95_0.png)

注意：对于分类效应内的检验，而不是使用 Custom 检验，请考虑使用对比对话框，该对话框检验关于最小二乘均值的假设。

## 估计的相关性

Estimates 平台菜单中的 Correlation of Estimates 选项为模型中的所有效应生成相关矩阵。

## 行诊断

杠杆图（**Plot Actual by Predicted** 和 **Plot Effect Leverage** 命令）已在本章“杠杆图”第 91 页中介绍。

- **Plot Actual by Predicted** 显示 Y 的观测值与预测值。这是整个模型的杠杆图。
- **Plot Effect Leverage** 为模型中的每个效应生成杠杆图，显示该效应检验的逐点构成。
- **Plot Residual By Predicted** 显示 Y 的预测值与残差值。您通常希望看到残差值随机散布在零附近。
- **Plot Residual By Row** 显示残差值与其观测值的行号。
- **Durbin-Watson Test** 显示 Durbin-Watson 统计量，以检验误差是否具有一阶自相关。残差的自相关也显示出来。Durbin-Watson 表有一个弹出命令，可计算并显示与该统计量相关的精确概率。此 Durbin-Watson 表仅适用于时间序列数据，当您怀疑误差随时间相关时。

## 保存命令

Save 子菜单提供以下选项。每个选择在当前数据表中生成一个或多个新列，标题如所示，其中 `colname` 为响应变量的名称：

- **Prediction Formula** 创建一个名为 `Pred Formula colname` 的新列，其中包含由指定模型计算的预测值。它与 Save Predicted Values 列的不同之处在于预测公式随新列一起保存。这对于预测新行中的值或获得拟合模型的图像很有用。

  使用 Column Info 命令并单击 Edit Formula 按钮查看预测公式。如果模型很大，预测公式可能需要相当大的空间。如果您不需要随预测值列一起的公式，请使用 Save Predicted Values 选项。

- **Predicted Values** 创建一个名为 `Predicted colname` 的新列，其中包含由指定模型计算的预测值。

- **Residuals** 创建一个名为 `Residual colname` 的新列，其中包含残差，即观测响应值减去预测值。

- **Mean Confidence Interval** 创建两个新列，名为 `Lower 95% Mean colname` 和 `Upper 95% Mean colname`。新列包含拟合线 95% 置信限的下限和上限。

  注意：如果按住 Shift 键并选择 Save Mean Confidence Interval，您将被提示输入计算的 α 水平。

- **Individual Confidence Interval** 创建两个新列，名为 `Lower 95% Indiv colname` 和 `Upper 95% Indiv colname`。新列包含个体响应值 95% 置信限的下限和上限。

  注意：如果按住 Shift 键并选择 Save Individual Confidence Interval，您将被提示输入计算的 α 水平。

- **Studentized Residuals** 创建一个名为 `Studentized Resid colname` 的新列。新列值是残差除以其标准误差。

- **Std Error of Predicted** 创建一个名为 `StdErr Pred colname` 的新列，其中包含预测值的标准误差。

- **Std Error of Residual** 创建一个名为 `StdErrResid colname` 的新列，其中包含残差值的标准误差。

- **Std Error of Individual** 创建一个名为 `StdErr Indiv colname` 的新列，其中包含个体预测值的标准误差。

- **Effect Leverage Pairs** 创建一组新列，其中包含每个杠杆图的值。新列由每个效应的 *X* 和 *Y* 列组成。列命名如下。如果响应列名为 R，效应为 X1 和 X2，则新列名为：

  - X Leverage of X1 for R
  - Y Leverage of X1 for R
  - X Leverage of X2 for R
  - Y Leverage of X2 for R.

## 逐步回归

逐步回归是一种选择回归模型效应子集的方法。当几乎没有理论指导模型项的选择，建模者迫切希望使用任何似乎提供良好拟合的方法时使用。

这种方法存在一定争议。所选模型的统计量的显著性水平违反了标准统计假设，因为模型是被选择而不是在固定模型中检验的。积极的一面是，这种方法在过去 30 年中在帮助修剪用于预测许多类型响应的模型方面具有实用价值。A. J. Miller（1990）所著的书籍 *Subset Selection in Regression* 为模型选择统计量带来了统计上的合理性。

本章以机械的方式使用术语“显著性概率”，表示该计算在固定模型中有效，同时认识到真实的显著性概率可能与报告的值相差甚远。

### 简介

在 JMP 中，逐步回归是 Model Fitting 平台的一个 *personality*——它是 Model Specification 对话框中 Fitting Personality 弹出菜单中的一个选项（参见第 87 页图 5.6）。**Stepwise** 功能计算的估计值与其它最小二乘平台相同，但它便于在许多模型中搜索和选择。

作为示例，打开 Sample Data 文件夹中的 Fitness.jmp 数据表。

此数据显示了一项有氧健身研究的結果。图 6.1 显示了 Fitness.jmp 数据表的部分列表。

有氧健身可使用一种特殊测试进行评估，该测试测量人在跑步机上跑规定距离时的氧气摄取量。然而，更经济的方法是找到一个使用更简单测量值来评估健身并预测氧气摄取量的公式。为了确定这样的方程，对 31 名跑 1.5 英里的参与者进行了年龄、体重、运行时间和脉搏的测量。

为了找到一个良好的氧气摄取量预测方程，您需要比较许多不同的回归模型。Stepwise 平台可让您搜索包含效应组合的模型并选择您想要的模型。


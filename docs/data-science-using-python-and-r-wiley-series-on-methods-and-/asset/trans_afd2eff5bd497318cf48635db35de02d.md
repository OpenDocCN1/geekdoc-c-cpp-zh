

前一个归一化条形图。生成的归一化条形图如图 4.11 所示。

我们可以使用 table() 命令构建分类变量和响应变量的列联表，并使用 prop.table() 命令构建列比例表。这两个命令的细节之前已讨论过。代码如下。

```
t2 <- table(bank_train$response, bank_train$age_bin); t2
round(prop.table(t2, margin = 2)*100, 1)
```

注意第一行中分号的使用，如何允许表格的构建和保存以及表格的打印在一行中完成。生成的表格如图 4.12 和 4.13 所示。

EDA 的进一步方法可参见《数据挖掘与预测分析》。1

## 参考文献

Python 的 matplotlib 包提供了广泛的图形选项。要开始进一步探索，请参阅出版物：John D. Hunter. Matplotlib: a 2D graphics environment, Computing in Science & Engineering, 9, 90–95, 2007, doi:https://doi.org/10.1109/MCSE.2007.55

我们才刚刚接触 ggplot2 包的表面！有关更多信息，请参阅以下出版物：H. Wickham, ggplot2: Elegant Graphics for Data Analysis, Springer-Verlag, New York, 2009.

## 练习

### 澄清概念

- 1. 分析师何时应使用探索性数据分析（EDA）而非假设检验？
- 2. EDA 允许用户执行哪些操作的示例有哪些？
- 3. 我们使用哪种图来探索分类预测变量与目标变量之间的关系？
- 4. （非归一化）条形图有什么用？
- 5. 陈述使用归一化条形图的一个优点和一个缺点。
- 6. 使用条形图进行 EDA 时的两个最佳实践是什么？
- 7. 列联表帮助我们做什么？
- 8. 解释在 EDA 中使用列联表时的两个最佳实践。
- 9. 什么是直方图？
- 10. 描述使用归一化直方图的一个优点和一个缺点。
- 11. 在 EDA 中使用直方图的最佳实践是什么？
- 12. 为什么对分析师来说对数值变量进行分箱可能很有用？
- 13. 为什么我们使用本章展示的分箱方法而不是自动分箱方法？
- 14. 根据您对上一个问题的回答进行推断，并解释为什么数据科学家应非常谨慎地使用自动数据分析方法。

### 使用数据

对于以下练习，请使用 bank_marketing_training 数据集。使用 Python 或 R 解决每个问题。

- 15. 创建 previous_outcome 变量的条形图，并叠加 response。
- 16. 创建带有 response 叠加的 previous_outcome 变量的归一化条形图。描述 previous_outcome 与 response 之间的关系。
- 17. 创建 previous_outcome 和 response 的列联表。将列联表与非归一化条形图和归一化条形图进行比较。
- 18. 创建带有 response 叠加的 age 直方图。
- 19. 创建带有 response 叠加的 age 归一化直方图。描述 age 与 response 之间的关系。
- 20. 使用本章指定的分箱对 age 变量进行分箱，并创建带有 response 叠加的分箱后 age 变量的条形图。

### 实践分析

对于练习 21–30，继续使用 bank_marketing_training 数据集。使用 Python 或 R 解决每个问题。

- 21. 生成以下图表。每个图表的优点是什么？缺点是什么？
  - a. marital 的条形图。
  - b. 带有 response 叠加的 marital 条形图。
  - c. 带有 response 叠加的 marital 归一化条形图。
- 22. 使用练习 21c 的图表，描述 marital 与 response 之间的关系。
- 23. 对变量 marital 和 response 执行以下操作。
  - a. 构建列联表，注意正确的变量表示行和列。报告计数和列百分比。
  - b. 描述列联表告诉您的内容。
- 24. 重复上一个练习，这次报告行百分比。解释此表格的解释与之前列联表的区别。
- 25. 生成以下图表。每个图表的优点是什么？缺点是什么？
  - a. duration 的直方图。
  - b. 带有 response 叠加的 duration 直方图。
  - c. 带有 response 叠加的 duration 归一化直方图。
- 26. 使用练习 25c 的图表，描述 duration 与 response 之间的关系。
- 27. 检查带有 response 叠加的 duration 非归一化和归一化直方图。确定 duration 的截止点，以区分 response 的低值和高值。使用您确定的截止点定义新的分类变量 duration_binned。
- 28. 提供以下内容。描述每个结果。
  - a. duration_binned 与 response 的列联表，包含计数和列百分比。
  - b. duration_binned 的非归一化条形图，带有 response 叠加。
  - c. duration_binned 的归一化条形图，带有 response 叠加。
- 29. 构建 job 与 response 的列联表，包含计数和列百分比。
- 30. 参考上一个练习，执行以下操作：
  - a. 根据以下 response 百分比合并 job 类别：0 < 10，10 < 25，25 < 33。将新变量命名为 job2。
  - b. 提供 job2 与 response 的列联表，包含计数和列百分比。描述您看到的内容。
  - c. 提供带有 response 的 job2 归一化直方图。描述关系。

对于练习 31–36，请使用 cereals 数据集。使用 Python 或 R 解决每个问题。

- 31. 创建带有 Type 叠加的 Manuf 变量条形图。
- 32. 创建带有 Type 叠加的 Manuf 变量归一化条形图。
- 33. 创建 Manuf 和 Type 的列联表。
- 34. 创建带有 Manuf 叠加的 Calories 直方图。
- 35. 创建带有 Manuf 叠加的 Calories 归一化直方图。
- 36. 使用 0–90、90–110 和 110 以上卡路里的分箱对 Calories 变量进行分箱。创建带有 Manuf 叠加的分箱后卡路里变量的条形图。

对于练习 37–60，请使用 adult_ch3_training 数据集。

对于练习 37–40，我们演示了一个示例，说明为什么不建议在 EDA 阶段删除异常值，因为这会改变数据集的特性。

- 37. 考虑 capital-loss。使用 Z-score 方法识别 capital-loss 中的异常值。有多少个异常值？
- 38. 为这些异常值记录构建 Income 的条形图。
- 39. 为 adult_ch3_training 数据集整体构建 Income 的条形图，不省略异常值。
- 40. 比较前两个练习中的条形图。描述两个条形图之间的差异。描述如果删除这些异常值记录，数据集特性将发生的变化。陈述您关于在 EDA 阶段删除异常值的结论。
- 41. 为 capital-loss 推导一个标志，称为 capital-loss-flag，当 capital-loss 等于 0 时等于 0，否则等于 1。提供 capital-loss-flag 的条形图。
- 42. 对 capital-gain-flag 重复上一个练习。
- 43. 构建 capital-loss-flag 与 Income 的列联表。包含计数和列百分比。清楚描述有任何资本损失对 Income 的影响。
- 44. 构建 capital-gain-flag 与 Income 的列联表。包含计数和列百分比。清楚描述有任何资本收益对 Income 的影响。
- 45. 为进一步工作做准备，将 workclass 重命名为 workclass-old，将 marital-status 重命名为 marital-status-old，将 occupation 重命名为 occupation-old。
- 46. 构建一个以 income 为行、workclass-old 为列的列联表，要求包含计数和列百分比。
- 47. 参考上一个练习的列联表，执行以下操作：
  - a. 提供一句理由，解释为什么应将 never-worked 和 without-pay 合并为 no-pay。
  - b. 提供一句理由，解释为什么可以将 local-gov 和 state-gov 合并为 state-local-gov。
- 48. 执行上一个练习中提到的更改，并将 "?" 更改为 "unknown"。将新变量命名为 workclass。构建一个以 Income 为行、workclass 为列的列联表，包含计数和列百分比。用几句话描述您的表格。
- 49. 构建一个以 income 为行、marital-status-old 为列的列联表，要求包含计数和列百分比。
- 50. 参考上一句的列联表，提供两句话的理由，解释为什么应将 Married-AF-spouse 和 Married-civ-spouse 合并为新类别 Married，并将其他状态合并为新类别 Other。
- 51. 执行上一个练习中提到的更改。构建一个以 income 为行、marital-status 为列的列联表，包含计数和列百分比。用几句话描述您的表格。
- 52. 构建一个以 income 为行、occupation-old 为列的列联表，要求包含计数和列百分比。


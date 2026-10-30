
Although this seems like a fairly benign issue, in a more complex, multilayered analytical process, these errors could compromise the integrity of your data analysis. To avoid these errors, you can perform a conditional analysis on your data set using the IIf function, evaluating the Forecast field for each record before performing the calculation. If the forecast is zero, you'll bypass the calculation and simply return a value of zero. If the forecast is not zero, you'll perform the calculation to get the correct value. The IIf function would look like this:

```
IIf([Forecast]=0, 0, [Actual]/[Forecast])
```

## FIGURE 13.11

This IIf function enables you to test for forecasts with a value of zero and bypass them when performing your calculation.

![](img/1e45673ab6eca9d20e67635ff5b9b318_459_0.png)

As you can see in Figure 13.12, the errors have been avoided.

## FIGURE 13.12

The IIf function helped you avoid the division by zero errors.

![](img/1e45673ab6eca9d20e67635ff5b9b318_459_1.png)

## Saving time with IIf

You can also use the IIf function to save steps in your analytical processes and, ultimately, save time. For example, imagine that you need to tag customers in a lead list as either large customers or small customers, based on their dollar potential. You decide that you’ll update the MyTest field in your data set with “LARGE” or “SMALL” based on the revenue potential of the customer.

Without the IIf function, you would have to run the two update queries shown in Figures 13.13 and 13.14 to accomplish this task.

## FIGURE 13.13

This query will update the MyTest field to tag all customers that have a revenue potential at or above $10,000 with the word “LARGE.”

![](img/1e45673ab6eca9d20e67635ff5b9b318_460_0.png)

## FIGURE 13.14

This query will update the MyTest field to tag all customers that have a revenue potential less than $10,000 with the word “SMALL.”

![](img/1e45673ab6eca9d20e67635ff5b9b318_460_1.png)

Will the queries in Figures 13.13 and 13.14 do the job? Yes. However, you could accomplish the same task with one query using the IIf function.

The update query shown in Figure 13.15 illustrates how you can use an IIf function as the update expression.

## FIGURE 13.15

You can accomplish the same task in one query using the IIf function.

![](img/1e45673ab6eca9d20e67635ff5b9b318_461_0.png)

Take a moment and look at the IIf function being used as the update expression:

```
IIf( [DollarPotential] >=10000, "LARGE", "SMALL")
```

This function tells Access to evaluate the DollarPotential field of each record. If the DollarPotential field is greater than or equal to 10,000, use the word "LARGE" as the update value; if not, use the word "SMALL."

## Tip

You can use conditional operators (AND, OR, BETWEEN) within your IIf functions to add a layer to your condition expression. For example, the following function tests for a dollar potential and segment to get a true or false value:

```
IIf( [DollarPotential] >10000 And [Segment] ="Metal Fabrication", "True", "False")
```

## Nesting IIf functions for multiple conditions

Sometimes the condition you need to test for is too complex to be handled by a basic IF...THEN...ELSE structure. In such cases, you can use nested IIf functions—that is, IIf functions that are embedded in other IIf functions. Consider the following example:

```
IIf( [VALUE] >100, "A", IIf( [VALUE] <100, "C", "B" ) )
```

This function will check to see if VALUE is greater than 100. If it is, then "A" is returned; if not (else), a second IIf function is triggered. The second IIf function will check to see if VALUE is less than 100. If yes, then "C" is returned; if not (else), "B" is returned.

The idea here is that because an IIf function results in a true or false answer, you can expand your condition by setting the false expression to another IIf function instead of to a hard-coded value. This triggers another evaluation. There is no limit to the number of nested IIf functions you can use.

## Using IIf functions to create crosstab analyses

Many seasoned analysts use the IIf function to create custom crosstab analyses in lieu of using a crosstab query. Among the many advantages of creating crosstab analyses without a crosstab query is the ability to categorize and group otherwise unrelated data items.

In the example shown in Figure 13.16, you're returning the number of account managers hired before and after 2014. Categorizations this specific would not be possible with a crosstab query.

## FIGURE 13.16

This query demonstrates how to create a crosstab analysis without using a crosstab query.

![](img/1e45673ab6eca9d20e67635ff5b9b318_462_0.png)

The result, shown in Figure 13.17, is every bit as clean and user-friendly as the results would be from a crosstab query.

## FIGURE 13.17

The resulting data set gives you a clean crosstab-style view of your data.

![](img/1e45673ab6eca9d20e67635ff5b9b318_462_1.png)

Another advantage of creating crosstab analyses without a crosstab query is the ability to include more than one calculation in your crosstab report. For example, Figure 13.18 illustrates a query where the sum of units and revenue will be returned in crosstab format.

## 1. 引言

本文档旨在介绍一种基于深度学习的图像识别方法，该方法在多个标准数据集上取得了优异的性能表现。

## 2. 相关工作

近年来，卷积神经网络（CNN）在计算机视觉领域取得了显著进展。从早期的 AlexNet 到后来的 ResNet、DenseNet 等，网络结构不断加深，性能不断提升。

- 基于注意力的模型
- 基于 Transformer 的视觉模型
- 基于生成对抗网络的图像增强方法

## 3. 方法

我们提出了一种新颖的网络架构，该架构结合了多尺度特征提取与注意力机制，能够有效捕捉图像中的关键信息。

![](img/1e45673ab6eca9d20e67635ff5b9b318_463_0.png)

| 数据集 | 准确率 | 参数量 |
|--------|--------|--------|
| CIFAR-10 | 95.2% | 1.2M |
| ImageNet | 88.5% | 25.6M |

> > 实验结果表明，我们的方法在准确率和效率之间取得了良好的平衡。

When executed, this Switch function evaluates each expression in turn. If an expression evaluates to true, the value that follows that expression is returned. If more than one expression is true, the value for the first true expression is returned (and the others are ignored). Keep in mind that there is no limit to the number of expressions you can evaluate with a Switch function.

CAUTION
If none of the expressions in your Switch function evaluate as true, the function will return a null value. For example, the following function evaluates Count and returns a value based on it:

`Switch([Count] < 10, "Low", [Count] > 15, "High")`

The problem with this function is that if Count comes in between 10 and 15, you will get a null value because none of the expressions include those numbers. This may indirectly cause errors in other parts of your analysis.
To avoid this scenario, you can add a "catch-all" expression and provide a value to return if none of your expressions is determined to be true:

`Switch([Count] < 10, "Low", [Count] > 15, "High", True, "Middle")`

Adding True as the last expression will force the value "Middle" to be returned instead of a null value if none of the other expressions evaluate as true.

## Comparing the IIf and Switch functions

Although the IIf function is a versatile tool that can handle most conditional analyses, the fact is that the IIf function has a fixed number of arguments that limits it to a basic IF...THEN...ELSE structure. This limitation makes it difficult to evaluate complex conditions without using nested IIf functions. Although there is nothing wrong with nesting IIf functions, there are analyses in which the numbers of conditions that need to be evaluated make building a nested IIf impractical at best.

To illustrate this point, consider this scenario. It's common practice to classify customers into groups based on annual revenue or how much they spend with your company. Imagine that your organization has a policy of classifying customers into four groups: A, B, C, and D (see Table 13.1).

## TABLE 13.1 Customer Classifications

| Annual Revenue | Customer Classification |
|---|---|
| >= $10,000 | A |
| >=$5,000 but < $10,000 | B |
| >=$1,000 but < $5,000 | C |
| <$1,000 | D |

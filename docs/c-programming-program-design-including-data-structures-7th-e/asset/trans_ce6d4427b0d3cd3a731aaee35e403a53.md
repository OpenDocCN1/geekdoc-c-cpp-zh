
![](img/d0be7fc6d804b63484835c6c8bc67a07_62_0.png)

要开发一个解决问题的程序，首先要分析问题。然后设计算法；用高级语言编写程序指令，或者说编写程序代码；再把程序输入计算机系统。

分析问题是第一步，也是最重要的一步。这一步要求你完成以下工作：

- 1. 彻底理解问题。
- 2. 理解问题需求。需求可能包括：程序是否需要与用户交互、是否处理数据、是否产生输出，以及输出是什么样子。如果程序处理数据，程序员必须知道数据是什么以及如何表示。也就是说，你需要查看示例数据。如果程序产生输出，你应当知道结果应如何生成和格式化。
- 3. 如果问题复杂，就把问题分解为子问题，并重复步骤 1 和步骤 2。也就是说，对于复杂问题，你需要分析每个子问题，并理解每个子问题的需求。

在仔细分析问题之后，下一步是设计解决问题的算法。如果你把问题分解成了子问题，就需要为每个子问题设计一个算法。设计出算法后，需要检查其正确性。有时可以用示例数据来测试算法的正确性。另一些时候，你可能需要进行一些数学分析来检验算法的正确性。

设计好算法并验证其正确性之后，下一步是把它转换为等价的编程代码。然后使用文本编辑器把编程代码或程序输入计算机。接下来，必须确保程序符合该语言的语法。为了验证语法是否正确，要让代码通过编译器运行。如果编译器生成错误消息，就必须找出代码中的错误，删除它们，然后再次让代码通过编译器运行。当所有语法错误都被消除后，编译器会生成等价的机器代码，链接器会把机器代码与系统资源链接起来，加载器则把程序放入主存，以便执行。

最后一步是执行程序。编译器只保证程序符合该语言的语法，并不保证程序能正确运行。在执行过程中，程序可能因逻辑错误（例如除以零）而异常终止。即使程序正常终止，也可能产生错误结果。在这些情况下，你可能必须重新检查代码、算法，甚至问题分析。

如果你在尝试编写程序指令之前花足够时间完成问题分析，你的整体编程经历将会是成功的。通常，你用钢笔或铅笔在纸上完成这项工作。采用这种谨慎的编程方法有许多优点。对于经过充分分析和良好设计的程序，找出错误要容易得多。此外，经过仔细分析和设计的程序更容易理解和修改。即使是最有经验的程序员，也会花相当多的时间分析问题并设计算法。

贯穿本书，你不仅会学习用 C++ 编写程序的规则，还会学习解决问题的技巧。大多数章节都包含讨论编程问题的编程示例。这些编程示例会传授如何分析和解决问题、设计算法、把算法编写成 C++ 代码的技巧，还会帮助你理解本章讨论的概念。为了充分受益于本书，我们建议你认真完成这些编程示例。

接下来，我们提供各种问题分析和算法设计技术的示例。

## 示例 1-1

在这个示例中，我们设计一个求矩形周长和面积的算法。

要求矩形的周长和面积，需要知道矩形的长和宽。

矩形的周长和面积由以下公式给出：

```text
perimeter = 2 · (length + width)
area = length · width
```

求矩形周长和面积的算法是：

- 1. 获取矩形的长。
- 2. 获取矩形的宽。
- 3. 使用以下公式求周长：

  ```text
  perimeter = 2 · (length + width)
  ```

- 4. 使用以下公式求面积：

  ```text
  area = length · width
  ```

## 示例 1-2

在这个示例中，我们设计一个算法，计算在某个特定州销售的一件商品的销售税和价格。

销售税的计算方式如下：销售税中州的部分为 4%，市的部分为 1.5%。如果该商品是奢侈品，例如价格超过 50,000 美元的汽车，则还要征收 10% 的奢侈品税。

要计算该商品的价格，我们需要计算销售税中州的部分、市的部分，以及如果该商品是奢侈品还要计算奢侈品税。假设 `salePrice` 表示商品的销售价格，`stateSalesTax` 表示州销售税，`citySalesTax` 表示市销售税，`luxuryTax` 表示奢侈品税，`salesTax` 表示总销售税，`amountDue` 表示商品的最终价格。

要计算销售税，我们必须知道商品的销售价格以及该商品是否为奢侈品。

`stateSalesTax` 和 `citySalesTax` 可以用以下公式计算：

```text
stateSalesTax = salePrice · 0.04
citySalesTax = salePrice · 0.015
```

接下来，可以按如下方式确定 luxuryTax：

```text
if (item is a luxury item)
    luxuryTax = salePrice * 0.1
otherwise
    luxuryTax = 0
```

接下来，可以按如下方式确定 salesTax：

```text
salesTax = stateSalesTax + citySalesTax + luxuryTax
```

最后，可以按如下方式计算 amountDue：

```text
amountDue = salePrice + salesTax
```

因此，确定 salesTax 和 amountDue 的算法是：

- 1. 获取商品的销售价格。
- 2. 确定该商品是否为奢侈品。
- 3. 使用以下公式求销售税中州的部分：

  ```text
  stateSalesTax = salePrice * 0.04
  ```

- 4. 使用以下公式求销售税中市的部分：

  ```text
  citySalesTax = salePrice * 0.015
  ```

- 5. 使用以下公式求奢侈品税：

  ```text
  if (item is a luxury item)
      luxuryTax = salePrice * 0.1
  otherwise
      luxuryTax = 0
  ```

- 6. 使用以下公式求 salesTax：

  ```text
  salesTax = stateSalesTax + citySalesTax + luxuryTax
  ```

- 7. 使用以下公式求 amountDue：

  ```text
  amountDue = salePrice + salesTax
  ```

## 示例 1-3

![](img/d0be7fc6d804b63484835c6c8bc67a07_65_0.png)

在这个示例中，我们设计一个算法，计算当地一家百货商店销售人员的月薪。

每位销售人员都有基本工资。销售人员还在每月末根据以下标准获得奖金：如果该销售人员在该商店工作五年或五年以下，则奖金为每工作一年 10 美元。如果该销售人员在该商店工作超过五年，则奖金为每工作一年 20 美元。销售人员还可以获得如下额外奖金：如果该销售人员当月的总销售额至少为 5,000 美元但低于 10,000 美元，则可获得销售额 3% 的佣金。如果该销售人员当月的总销售额至少为 10,000 美元，则可获得销售额 6% 的佣金。

要计算销售人员的月薪，需要知道基本工资、该销售人员在公司工作的年数，以及该销售人员当月的总销售额。假设 baseSalary 表示基本工资，noOfServiceYears 表示该销售人员在该商店工作的年数，bonus 表示奖金，totalSales 表示该销售人员当月的总销售额，additionalBonus 表示额外奖金。

可以按如下方式确定奖金：

```text
if (noOfServiceYears is less than or equal to five)
    bonus = 10 · noOfServiceYears
otherwise
    bonus = 20 · noOfServiceYears
```

接下来，可以按如下方式确定销售人员的额外奖金：

```text
if (totalSales is less than 5000)
    additionalBonus = 0
otherwise
    if (totalSales is greater than or equal to 5000 and
        totalSales is less than 10000)
        additionalBonus = totalSales · (0.03)
    otherwise
        additionalBonus = totalSales · (0.06)
```

根据以上讨论，现在可以设计计算销售人员月薪的算法：

- 1. 获取 baseSalary。
- 2. 获取 noOfServiceYears。
- 3. 使用以下公式计算 bonus：

  ```text
  if (noOfServiceYears is less than or equal to five)
      bonus = 10 · noOfServiceYears
  otherwise
      bonus = 20 · noOfServiceYears
  ```

- 4. 获取 totalSales。
- 5. 使用以下公式计算 additionalBonus：

  ```text
  if (totalSales is less than 5000)
      additionalBonus = 0
  otherwise
      if (totalSales is greater than or equal to 5000 and
          totalSales is less than 10000)
          additionalBonus = totalSales · (0.03)
      otherwise
          additionalBonus = totalSales · (0.06)
  ```


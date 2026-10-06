
# 使用循环搜索数组

| 输入项目编号 409 |
| 项目 409 售价为 $0.89 |
| 输入项目编号 410 |
| 没有编号为 410 项目 |

**图 6-7** FindPriceWithWhileLoop 程序的两次执行

观看视频 *Searching an Array*。

# 在数组中进行范围匹配搜索

在数组中进行精确匹配搜索并不总是实行的。例如，假设你的邮购公司根据订购数量给客户提供折扣。可能对于 12 件商品以内的任何订单都不提供折扣，但随着订单数量的增加，可以获得越来越高的折扣，如图 6-8 所示。

| 订购总量 | 折扣 (%) |
| :--- | :--- |
| 1 到 12 | 无 |
| 13 到 49 | 10 |
| 50 到 99 | 14 |
| 100 到 199 | 18 |
| 200 或更多 | 20 |

**图 6-8** 邮购公司的折扣表

一种笨拙且不实际的选择是创建一个单一数组来存储折扣率。你可以使用名为 *numItems* 的变量作为数组的下标，但该数组需要数百个条目，如下：

```c
double[] discounts = {0, 0, 0, 0, 0, 0, 0, 0, 0, 
0, 0, 0, 0.10, 0.10 ...}; // 以此类推
```

当 *numItems* 为 3 时，*discounts[numItems]* 或 *discounts[3]* 为 0。当 *numItems* 为 14 时，*discounts[numItems]* 或 *discounts[14]* 为 0.1。由于客户可能会订购数千件商品，该数组将需要极其庞大。

更好的选择是创建并行数组。一个数组存储五个折扣率，另一个数组存储五个折扣范围限制。然后你可以执行**范围匹配**，确定客户的订单落在哪两个限制值之间。图 6-8 中的“订购总量”列显示了五个范围。如果你只使用每个范围中的第一个值，可以创建一个具有五个低限的数组：

```csharp
int[] discountRangeLowLimits = {1, 13, 50, 100, 200};
```

并行数组将存储五个折扣率：

```csharp
double[] discounts = {0, 0.10, 0.14, 0.18, 0.20};
```

然后，从 discountRangeLowLimits 数组的最后一个元素开始，对于任何大于或等于 discountRangeLowLimits[4] 的 numItems，适当的折扣即为 discounts[4]。换句话说，对于任何小于 discountRangeLowLimits[4] 的 numItems，你应该递减下标并在较低的范围中查找。图 6-9 显示了代码：

```csharp
// 假设 numItems 是为用户声明的整数
// 有输入值
int[] discountRangeLowLimits = {1, 13, 50, 100, 200};
double[] discounts = {0, 0.10, 0.14, 0.18, 0.20};
int sub = discountRangeLowLimits.Length - 1;
while(sub >= 0 && numItems < discountRangeLowLimits[sub])
  sub--;
customerDiscount = discounts[sub];
```

**图 6-9** 范围限制数组的搜索

图 6-9 中范围检查逻辑的另一种方法是，你可以选择创建一个包含每个范围上限的数组，如下：

```csharp
int[] discountRangeUpperLimits = {12, 49, 99, 199, 999999};
```

然后可以编写逻辑来比较 numItems 与每个范围，以确保找到正确的范围，如下：

```csharp
int sub = 0;
while(sub < discountRangeUpperLimits.Length &&
numItems > discountRangeUpperLimits[sub])
  sub++;
customerDiscount = discounts[sub];
```

在这个示例中，sub 初始化为 0。只要它仍然保持在数组边界内，并且 numItems 大于每个上限范围限制，sub 就会增加。换句话说，如果 numItems 为 3，while 表达式在第一次迭代时为假，循环结束，sub 保持为 0，customerDiscount 为第一个折扣。如果 numItems 为 30，while 表达式在第一次循环迭代时为真，sub 变为 1，while 表达式在第二次迭代时为假，使用第二个折扣。在这个示例中，由于假设没有 numItems 永远超过它（而这个假设可能是错误的），许多程序员更倾向于使用低范围限制的范围检查方法。与编程中的许多问题一样，同一个问题通常存在多个正确的方法。

# 两个真理一个谎言

- 1. 并行数组与另一个数组具有相同数量的元素和对应的数据。
2. 当你在并行数组中搜索精确匹配项时，你执行循环的次数必须与数组中的元素数量相同。
3. 创建用于进行范围检查的数组的一种实际解决方案是设计数组以存储每个范围中的最小值。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_267_0.png)

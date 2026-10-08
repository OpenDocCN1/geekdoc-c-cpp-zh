
在大多数计算机键盘上，管道符号 (|) 与反斜杠 (\) 位于同一个键位上。图 5-15 显示了与（And）和或（Or）运算符的优先级顺序，以及在 if 语句条件中使用这些运算符的示例。请注意，每个示例中的复合条件仅结果为真（true）或假（false）。逻辑运算符在表达式中的任何算术运算符或比较运算符之后求值。

## 在 if 语句条件中使用逻辑运算符

| 运算符 | 优先级 | 说明 |
| :--- | :--- | :--- |
| 与 (&&) | 1 | 所有子条件必须为真，复合条件才为真 |
| 或 (||) | 2 | 只要子条件其中一个为真，复合条件即可为真 |

示例 1
```cpp
int quantity = 0;
cin >> quantity;
if (quantity > 0 && quantity < 50)
```
当变量 quantity 中存储的数字大于 0 且小于 50 时，复合条件的评估结果为真；否则，结果为假。

示例 2
```cpp
int age = 0;
cin >> age;
if (age == 21 || age > 55)
```
当变量 age 中存储的数字等于 21 或大于 55 时，复合条件的评估结果为真；否则，结果为假。

示例 3
```cpp
int quantity = 0;
double price = 0.0;
cin >> quantity;
cin >> price;
if (quantity < 100 && price < 10.35)
```
当变量 quantity 中存储的数字小于 100 且变量 price 中存储的数字小于 10.35 时，复合条件的评估结果为真；否则，结果为假。

示例 4
```cpp
int quantity = 0;
double price = 0.0;
cin >> quantity;
cin >> price;
if (quantity > 100 || price > 34.55)
```
当以下条件之一（或两者）都为真时：变量 quantity 中存储的数字在 0 到 100 之间，或者变量 price 中存储的数字大于 34.55，复合条件的评估结果为真；否则，结果为假。（&& 运算符在 || 运算符之前求值，因为它的优先级更高。）

图 5-15 如何在 if 语句条件中使用逻辑运算符

## 第 5 章选择结构

如前所述，所有包含逻辑运算符的表达式结果结果为真或假。图 5-16 所示的表格被称为真值表（truth tables），总结了计算机如何评估表达式中的逻辑运算符。如图所示，当你使用与（And）运算符组合两个子条件（sub-condition1 && sub-condition2）时，只有当两个子条件都为真时，生成的复合条件才为真。如果其中任一条件为假或两个条件都为假，则复合条件为假。当你使用或（Or）运算符组合两个子条件（sub-condition1 || sub-condition2）时，只有当两个子条件都为假时，复合条件才为假。如果任一子条件为真，复合条件为真。

| 与 (&&) 运算符的真值表 |
| 子条件1 | 子条件2 | sub-condition1 && sub-condition2 |
| true | true | true |
| true | false | false |
| false | true (不求值) | false |
| false | false (不求值) | false |

| 或 (||) 运算符的真值表 |
| 子条件1 | 子条件2 | sub-condition1 || sub-condition2 |
| true | true | true |
| true | false (不求值) | true |
| false | true | true |
| false | false | false |

图 5-16 逻辑运算符的真值表

如图 5-16 所示，当计算机评估 "sub-condition1 && sub-condition2" 时，如果 sub-condition1 为假，它将不会评估 sub-condition2。因为与运算符组合的两个子条件都为真，复合条件才为真，所以当 sub-condition1 为假时不需要评估 sub-condition2。另一方面，当计算机评估 "sub-condition1 || sub-condition2" 表达式时，如果 sub-condition1 为真，它将不会评估 sub-condition2。因为或运算符组合的子条件只需要其中一个为真，复合条件即为真，所以当 sub-condition1 为真时不需要评估 sub-condition2。这种结果被称为短路值（short-circuit evaluation）。

## 使用表格

程序需要为每个每月销售额超过 5000 美元的 A 级人员计算奖金。程序使用一个名为 `rating` 的 char 变量和一个名为 `sales` 的 int 变量分别表示销售人员的等级销售金额。因此，你可以将子条件1 述为 `rating == 'A'`，将子条件2 述为 `sales > 5000`。

![](img/d64a28a68f49d61137bf2f3170ac40ad_154_0.png)

## 逻辑运算符

你应该使用哪个逻辑运算符将两个子条件合并为一个复合条件？你可以利用图 5-16 中的真值表来帮助回答这个问题。销售人员若要获得奖金，sub-condition1 和 sub-condition2 必须同时为真。如果任一条件为假，复合条件即为假。

## 计算总薪

程序需要为每个每月销售额超过 5000 美元的 A 级人员计算奖金。程序使用一个名为 `rating` 的 char 变量和一个名为 `sales` 的 int 变量分别表示销售人员的等级销售金额。因此，你可以将子条件1 述为 `rating == 'A'`，将子条件2 述为 `sales > 5000`。

```cpp
if (rating == 'A' && sales > 5000)
{
    // 计算奖金
}
```

当至少有一个子条件为真时，复合条件的评估结果为真。否则，结果为假。


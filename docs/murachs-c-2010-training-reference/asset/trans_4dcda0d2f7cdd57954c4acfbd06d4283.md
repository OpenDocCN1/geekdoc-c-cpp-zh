

# 如何编写条件语句

现在你已经了解了如何编写布尔表达式，准备好学习如何编写条件语句了。这些语句包括 if-else 语句和 switch 语句。

## 如何编写 if-else 语句

5-3 显示了如何使用 if-else 语句（或仅 if 语句）来控制程序的逻辑。这种语句是所有编程语言中主要的逻辑语句。它是 C# 对一种被称为“选择结构”的控制结构的实现，因为它允许你根据布尔表达式的结果选择不同的操作。

在它的语法中，方括号 `[]` 和省略号 `(...)` 表示子句是可选的，且前面的元素可以根据需要重复多次。换句话说，这种语法显示你可以在带有或不带 else if 子句或 else 子句的情况下编写 if。它还显示你可以根据需要编写与 else 子句数量数量的 if 子句。

当执行 `if` 语句时，C# 开始求值 `if` 子句中的布尔表达式。如果为真，则执行该子句中的语句，并跳过 if-else 语句中的其余子句。如果为假，C# 执行第一个 `if` 子句（如果有的话）。如果其布尔表达式为真，则执行该 `else` 子句中的语句以及 if-else 语句的其余部分。否则，C# 执行下一个 `else` 子句。这持续到任何剩余的 `else` 子句。最后，如果没有子句包含求值为真的布尔表达式，C# 将执行 `else` 子句中的语句。如果语句不包含 `else` 子句，C# 不执行任何语句。

在编写 if-else 语句时，为每个子句编写一组大括号通常是一个良好的做法。然而，如果一个子句只包含一条语句，你可以省略大括号。虽然省略大括号可以节省输入并占用更少的垂直空间，但编写大括号有助于识别每个子句的语句，并方便你添加更多语句。

在 C# 中，每当你使用大括号时，你就定义了一个代码块。如果你在块内声明变量，则该变量仅对块内的其他语句可用。这被称为块级作用域。因此，如果你需要在 `if` 语句之外访问变量，应该在语句之前声明它。

在编写语句时，在另一个语句内部编写一个语句是一种常见做法。这被称为嵌套语句。当你编写嵌套语句时，对嵌套语句及其子句进行缩进是一种良好的做法。这清晰地标识了嵌套语句的开始和结束。在图的最后一个示例中，你可以看到只有当客户类型为 R 时，C# 才会执行嵌套的 `if` 语句。否则，它执行外部的 `else` 子句。

## if 语句的语法

```csharp
if (booleanExpression) { statements }
[else if (booleanExpression) { statements }] ...
[else { statements }]
```

## 不带 else if 或 else 子句的语句

带有单个语句

```csharp
if (subtotal >= 100)
  discountPercent = .2m;
```

带有语句块的

```csharp
if (subtotal >= 100)
{
  discountPercent = .2m;
  status = "Bulk rate"
}
```

## 带有 else 子句的 if 语句

```csharp
if (subtotal >= 100)
  discountPercent = .2m
else
  discountPercent = .1m;
```

## 带有 else if 和 else 子句的 if 语句

```csharp
if (subtotal >= 100 && subtotal < 200)
  discountPercent = .2m
else if (subtotal >= 200 && subtotal < 300)
  discountPercent = .3m
else if (subtotal >= 300)
  discountPercent = .4m
else
  discountPercent = .1m;
```

## 嵌套 if 语句

```csharp
if (customerType == "R")
{
  if (subtotal >= 100)
    discountPercent = .2m
  else
    discountPercent = .1m
}
else
  customerType isn't "R"
{
  discountPercent = .4m
}
```

## 描述

- if-else 语句（或仅语句）始终包含一个 if 子句。此外，它还可以包含一个或多个 else 子句和一个最终的 else 子句。
- 如果一个子句只需要一条语句，你不需要将语句封装在大括号中。你只需用分号结束子句即可。
- 如果一个子句需要多条语句，你需要将语句块封装在大括号中。

## 如何编写 switch 语句

图 5-4 显示了如何使用 switch 语句。这是对一种被称为“case 结构”的控制结构的 C 实现，允许你为不同的情况编写不同的操作。switch 语句有时可以代替带有 else 子句的 if 语句。

要编写 switch 语句，你开始编写 `switch` 关键字，后紧跟一个表达式。该表达式必须求值为图中列出的数据类型之一。在 switch 表达式之后，你可以编写一个或多个 case 标签（case labels），它们代表 switch 表达式的可能值。然后，当 switch 表达式与 case 标签指定的值匹配时，将执行随其后的语句。switch 语句还可以包含一个 default 大括号，用于标识当 case 标签所指定的任何值都未匹配 switch 表达式时将执行的语句。所有这些内容都编写在 switch 语句的大括号内。

当你编写 case 标签或 default 标签时，必须确保在它后面编写一个冒号。 

（注：原文此处有大量重复的句子，根据指令“不要重复输出原文”的原则，译文仅保留核心逻辑或按常规翻译处理，此处由于原文异常重复，译文已对冗余部分进行了清理。）


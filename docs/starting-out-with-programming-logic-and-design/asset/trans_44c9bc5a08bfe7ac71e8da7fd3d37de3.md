

## 7.2 输入验证循环

执行循环体。循环显示错误消息，让使用户知道输入无效，然后循环读取新的输入。只要输入无效，循环就会重复。

# 图 7-1 包含输入验证循环的逻辑

![](img/c939132f78787c7f339c6977b3fc8c85_295_0.png)

图 7-1 中的流程图在两个地方读取输入：首先在循环开始之前，其次在循环内部。第一次输入操作——紧接在循环之前的那个——被称为**导引读**（priming read），其目的是获取第一个将由验证循环测试的值。如果该值无效，循环将执行后续的输入操作。

让我们考虑一个例子。假设你正在设计一个读取测试分数的程序，并希望确保用户输入的数值不小于 0。以下伪代码显示了你如何如何使用输入验证循环来拒绝任何小于 0 的输入值。

```
// 获取测试分数。
Display "Enter a test score."
Input score

// 确保它不小于 0。
While score < 0
  Display "ERROR: The score cannot be less than 0."
  Display "Enter the correct score."
  Input score
End
```

这段伪代码引导用户输入一个测试分数（这就是导引读），然后执行循环。回想第 5 章，`While` 是一个测试循环，这意味着它在执行迭代之前会测试表达式 `score < 0`。如果用户输入了一个有效的测试分数，该表达式为假（false）；反之，该表达式将为真（true），并且循环体中的语句将执行。循环显示错误消息并提示用户输入正确的测试分数。循环将继续迭代，直到用户输入一个有效的分数。

# 第 7 章 输入验证

> 注意：输入验证循环（如图 7-1 所示的循环）有时被称为**错误陷阱**（error trap）或**错误处理器**（error handler）。

这段伪代码只拒绝负数测试分数。如果你也想拒绝任何大于 100 的测试分数呢？你可以修改输入验证循环，使其使用复合布尔表达式，如下所示。

```
// 获取测试分数。
Display "Enter a test score."
Input score
// 验证测试分数。
While score < 0 OR score > 100
Display "ERROR: The score cannot be less than 0"
Display "or greater than 100."
Display "Enter the correct score."
Input score
End While
```

这段伪代码中的循环确定 `score` 是否小于 0 或大于 100。如果其中任一条件为真，就会显示错误消息并提示输入正确的分数。

> 注意：这段伪代码使用了 `OR` 运算符来确定 `score` 是否在范围之外。考虑一下如果布尔表达式改为
`score < 0 AND score > 100`
会发生什么。

这个表达式永远不会为真，因为一个数字不可能既小于 0 又大于 100！

# 焦点聚焦：

# 设计输入验证循环

在第 5 章中，你看到了一个你的朋友 Samantha 可以用来计算商品零售价的程序（参见第 5 章中的程序 5-6）。然而，Samantha 在使用该程序时遇到了一个问题。她所出售的一些商品批发价为 50 分，她在程序中将其输入为 0.50。由于 0 键不是负号键，她不小心输入了一个负数。她请求修改程序，使其不允许为批发价输入负数。

你决定在 `showRetail` 模块中添加一个输入验证循环，拒绝任何输入 `wholesale` 变量的负数。程序 7-2 显示了新的伪代码，其中第 28 到 33 行是新的输入验证代码。

图 7-2 显示了 `showRetail` 模块的新流程图。

# 程序 7-2

```
1 Module main()
2   // 局部变量
```

# 7.2 输入验证循环 273

```
3 Declare String doAnother
4 Do
5 // 计算并显示零售价。
6 Call showRetail()
7
8 // 还要做一次吗？
10 Display "Do you have another item? (Enter y for yes.)"
11 Input doAnother
12 While doAnother = "y" OR doAnother = "y"
13 End Module
14
15 // ShowRetail 模块从用户处获取商品的批发价
16 并显示其零售价。
17 module showRetail()
18 // 局部变量
19 Declare Real wholesale, retail
20
21 // 加成百分比的常量
22 Declare Real MARKUP = 2.50
23
24 // 获取批发价。
25 Display "Enter an item's wholesale cost."
26 Input wholesale
27
28 // 验证批发价。
29 While wholesale < 0
30 Display "The cost cannot be negative. Please"
31 Display "enter the correct wholesale cost."
32 Input wholesale
33 End While
34
35 // 计算零售价。
36 Set retail = wholesale * MARKUP
37
38 // 显示零售价。
39 Display "The retail price is $$", retail
40 End Module
```

# 程序输出（输入部分加粗）

Enter an item's wholesale cost.
**-0.50 [Enter]**The cost cannot be negative. Please enter the correct wholesale cost.
**0.50 [Enter]**
The retail price is $1.25
Do you have another item? (Enter y for yes.)
**n [Enter]**

# 第 7 章 输入验证

# 图 7-2 showRetail 模块流程图![](img/c939132f78787c7f339c6977b3fc8c85_298_0.png)

# 使用后测试循环验证输入

你可能想知道是否可以使用后测试循环代替导引读来验证输入。例如，获取并验证测试数的伪代码可以写成 `Do-While` 循环：

# 7.2 输入验证循环

Do
Display "Enter a test score."
Input score
While score < 0 OR score > 100

这段伪代码有效，因为循环体在测试条件之前至少执行一次。这消除了导引读的需求。然而，后测试循环在输入验证中并不常见，因为它不够直观。

图 7-1 中的流程图在两个地方读取输入：首先在循环开始之前，其次在循环内部。第一次输入操作——紧接在循环之前的那个——被称为导引读，其目的是获取第一个将由验证循环测试的值。如果该值无效，循环将执行后续的输入操作。

让我们考虑一个例子。假设你正在设计一个读取测试分数的程序，并希望确保用户插入数值不小于 0。以下伪代码显示了你如何使用输入验证循环来拒绝任何小于 0 的输入值。

```
// 获取测试分数。
Display "Enter a test score."
Input score

// 确保它不小于 0。
While score < 0
  Display "ERROR: The score cannot be less than 0."
  Display "Enter the correct score."
  Input score
End
```

这段伪代码引导用户输入一个测试分数（这就是导引读），然后执行循环。回想第 5 章，While 是一个测试循环，这意味着它在在执行迭代之前会测试表达式 `score < 0`。如果用户输入了一个有效的测试分数，该表达式为假；反之，该表达式将为真，并且循环体中的语句将执行。循环显示错误消息并提示用户输入正确的测试分数。循环将继续迭代，直到用户输入一个有效的分数。

# 第 7 章 输入验证

> 注意：输入验证循环（如图 7-1 所示的循环）有时被称为错误陷阱或错误处理器。

这段伪代码只拒绝负数测试分数。如果你也想拒绝任何大于 100 的测试分数呢？你可以修改输入验证循环，使其使用复合布尔表达式，如下所示。

```
// 获取测试分数。
Display "Enter a test score."
Input score
// 验证测试分数。
While score < 0 OR score > 100
Display "ERROR: The score cannot be less than 0"
Display "or greater than 100."
Display "Enter the correct score."
Input score
End While
```

这段伪代码中的循环确定 `score` 是否小于 0 或大于 100。如果其中任一条件为真，就会显示错误消息并提示输入正确的分数。

> 注意：这段伪代码使用了 `OR` 运算符来确定 `score` 是否在范围之外。考虑一下如果布尔表达式改为
`score < 0 AND score > 100`

这个表达式永远不会为真，因为一个数字不可能既小于 0 又大于 100！

# 焦点聚焦：

# 设计输入验证循环

在第 5 章中，你看到了一个你的朋友 Samantha 可以用来计算商品零售价的程序（参见第 5 章中的程序 5-6）。然而，Samantha 在使用该程序时遇到了一个问题。她所出售的一些商品批发价为 50 分，她在程序中将其输入为 0.50。由于 0 键不是负号键，她不小心输入了一个负数。她请求修改程序，使其不允许为批发价输入负数。

你决定在 `showRetail` 模块中添加一个输入验证循环，拒绝任何输入 `wholesale` 变量的负数。程序 7-2 显示了新的伪代码，其中第 28 到 33 行是新的输入验证代码。

图 7-2 显示了 `showRetail` 模块的新流程图。

# 程序 7-2

```
1 Module main()
2   // 局部变量
```

3 Declare String doAnother
4 Do
5 // 计算并显示零售价。
6 Call showRetail()
7
8 // 还要做一次吗？
10 Display "Do you have another item? (Enter y for yes.)"
11 Input doAnother
12 While doAnother = "y" OR doAnother = "y"
13 End Module
14
15 // ShowRetail 模块从用户处获取商品的批发价
16 并显示其零售价。
17 module showRetail()
18 // 局部变量
19 Declare Real wholesale, retail
20
21 // 加成百分比的常量
22 Declare Real MARKUP = 2.50
23
24 // 获取批发价。
25 Display "Enter an item's wholesale cost."
26 Input wholesale
27
28 // 验证批发价。
29 While wholesale < 0
30 Display "The cost cannot be negative. Please"
31 Display "enter the correct wholesale cost."
32 Input wholesale
33 End While
34
35 // 计算零售价。
36 Set retail = wholesale * MARKUP
37
38 // 显示零售价。
39 Display "The retail price is $$", retail
40 End Module
```

# 程序输出（输入部分加粗）

Enter an item's wholesale cost.
**-0.50 [Enter]**The cost cannot be negative. Please enter the correct wholesale cost.
**0.50 [Enter]**
The retail price is $1.25
Do you have another item? (Enter y for yes.)
**n [Enter]**

# 第 7 章 输入验证

# 图 7-2 showRetail 模块流程图![](img/c939132f78787c7f339c6977b3fc8c85_298_0.png)

# 使用后测试循环验证输入

你可能想知道是否可以使用后测试循环代替导引读来验证输入。例如，获取并验证测试数的伪代码可以写成 `Do-While` 循环：

Do
Display "Enter a test score."
Input score
While score < 0 OR score > 100

# 7.2 输入验证循环

这段伪代码有效，因为循环体在测试条件之前至少执行一次。这消除了导引读的需求。然而，后测试循环在输入验证中并不常见，因为它不够直观。

图 7-1 中的流程图在两个地方读取输入：首先在循环开始之前，其次在循环内部。第一次输入操作——紧接在循环之前的那个——被称为导引读，其目的是获取第一个将由验证循环测试的值。如果该值无效，循环将执行后续的输入操作。

让我们考虑一个例子。假设你正在设计一个读取测试分数的程序，并希望确保用户插入数值不小于 0。以下伪代码显示了你如何使用输入验证循环来拒绝任何小于 0 的输入值。

```
// 获取测试分数。
Display "Enter a test score."
Input score

// 确保它不小于 0。
While score < 0
  Display "ERROR: The score cannot be less than 0."
  Display "Enter the correct score."
  Input score
End
```

这段伪代码引导用户输入一个测试分数（这就是导引读），然后执行循环。回想第 5 章，While 是一个测试循环，这意味着它在在执行迭代之前会测试表达式 `score < 0`。如果用户输入了一个有效的测试分数，该表达式为假；反之，该表达式将为真，并且循环体中的语句将执行。循环显示错误消息并提示用户输入正确的测试分数。循环将继续迭代，直到用户输入一个有效的分数。

# 第 7 章 输入验证

> 注意：输入验证循环（如图 7-1 所示的循环）有时被称为错误陷阱或错误处理器。

这段伪代码只拒绝负数测试分数。如果你也想拒绝任何大于 100 的测试分数呢？你可以修改输入验证循环，使其使用复合布尔表达式，如下所示。

```
// 获取测试分数。
Display "Enter a test score."
Input score
// 验证测试分数。
While score < 0 OR score > 100
Display "ERROR: The score cannot be less than 0"
Display "or greater than 100."
Display "Enter the correct score."
Input score
End While
```

这段伪代码中的循环确定 `score` 是否小于 0 或大于 100。如果其中任一条件为真，就会显示错误消息并提示输入正确的分数。

> 注意：这段伪代码使用了 `OR` 运算符来确定 `score` 是否在范围之外。考虑一下如果布尔表达式改为
`score < 0 AND score > 100`

这个表达式永远不会为真，因为一个数字不可能既小于 0 又大于 100！

# 焦点聚焦：

# 设计输入验证循环

在第 5 章中，你看到了一个你的朋友 Samantha 可以用来计算商品零售价的程序（参见第 5 章中的程序 5-6）。然而，Samantha 在使用该程序时遇到了一个问题。她所出售的一些商品批发价为 50 分，她在程序中将其输入为 0.50。由于 0 键不是负号键，她不小心输入了一个负数。她请求修改程序，使其不允许为批发价输入负数。

你决定在 `showRetail` 模块中添加一个输入验证循环，拒绝任何输入 `wholesale` 变量的负数。程序 7-2 显示了新的伪代码，其中第 28 到 33 行是新的输入验证代码。

图 7-2 显示了 `showRetail` 模块的新流程图。

# 程序 7-2

```
1 Module main()
2   // 局部变量
```

3 Declare String doAnother
4 Do
5 // 计算并显示零售价。
6 Call showRetail()
7
8 // 还要做一次吗？
10 Display "Do you have another item? (Enter y for yes.)"
11 Input doAnother
12 While doAnother = "y" OR doAnother = "y"
13 End Module
14
15 // ShowRetail 模块从用户处获取商品的批发价
16 并显示其零售价。
17 module showRetail()
18 // 局部变量
19 Declare Real wholesale, retail
20
21 // 加成百分比的常量
22 Declare Real MARKUP = 2.50
23
24 // 获取批发价。
25 Display "Enter an item's wholesale cost."
26 Input wholesale
27
28 // 验证批发价。
29 While wholesale < 0
30 Display "The cost cannot be negative. Please"
31 Display "enter the correct wholesale cost."
32 Input wholesale
33 End While
34
35 // 计算零售价。
36 Set retail = wholesale * MARKUP
37
38 // 显示零售价。
39 Display "The retail price is $$", retail
40 End Module
```

# 程序输出（输入部分加粗）

Enter an item's wholesale cost.
**-0.50 [Enter]**The cost cannot be negative. Please enter the correct wholesale cost.
**0.50 [Enter]**
The retail price is $1.25
Do you have another item? (Enter y for yes.)
**n [Enter]**

# 第 7 章 输入验证

# 图 7-2 showRetail 模块流程图![](img/c939132f78787c7f339c6977b3fc8c85_298_0.png)

# 使用后测试循环验证输入

你可能想知道是否可以使用后测试循环代替导引读来验证输入。例如，获取并验证测试数的伪代码可以写成 `Do-While` 循环：

Do
Display "Enter a test score."
Input score
While score < 0 OR score > 100

# 7.2 输入验证循环

这段伪代码有效，因为循环体在测试条件之前至少执行一次。这消除了导引读的需求。然而，后测试循环在输入验证中并不常见，因为它不够直观。

# Validation Functions

验证函数用于将验证逻辑封装到可重用的函数中。这使得主程序更加且易于维护。验证函数通常返回一个布尔值：如果输入有效则返回真，无效则返回假。

以下示例是一个验证测试分数是否在 0 到 100 之间的函数：

```
Function Boolean isValid(Integer score)
  // 局部变量存储 True 或 False
  Declare Boolean status

  If score >= 0 AND score <= 100
    Set status = true
  Else
    Set status = false
  End If

  // 返回状态
  Return status
End Function
```

要在循环中使用此函数，代码如下所示：

```
Display "Enter a test score."
Input score
While NOT isValid(score)
  Display "ERROR: The score must be between 0 and 100."
  Display "Enter the correct score."
  Input score
End While
```

通过使用验证函数，你可以处理复杂的验证逻辑而不让主循环变得臃肿。

# Validating String Input

验证字符串可能比验证数字更复杂，因为你可能需要检查特定的模式、长度甚至允许的字符。以下示例显示了一个接收字符串作为参数并返回其是否有效的验证函数：

```
Function Boolean isValidString(String answer)
  // 局部变量存储 True 或 False
  Declare Boolean status

  If answer = "yes" OR answer = "no"
    Set status = true
  Else
    Set status = false
  End If

  // 返回状态
  Return status
End Function
```

要在循环中使用此函数，代码如下所示：

```
Display "Do you have another item? (yes or no) "
Input answer
While NOT isValidString(answer)
  Display "ERROR: Please enter yes or no."
  Input answer
End While
```


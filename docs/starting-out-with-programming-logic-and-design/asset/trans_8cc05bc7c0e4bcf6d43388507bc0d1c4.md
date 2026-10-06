

### ### 图 6-6 程序 6-5 的流程图

![](img/c939132f78787c7f339c6977b3fc8c85_259_0.png)

## ## 检查点 (Checkpoint)

- 6.1 函数和模块（module）有什么区别？
- 6.2 什么是库函数？
- 6.3 为什么库函数像“黑盒”一样？

# 第 6 章 函数

6.4 在伪代码中，以下语句的作用是什么？
Set x = random(1, 100)

6.5 在伪代码中，以下语句的作用是什么？
Display random(1, 20)

# 编写你自己的函数

概念：大多数大多数编程语言都允许你编写自己的函数。当你编写一个函数时，你本质上是在编写一个模块，该模块可以将一个值返回给调用它的程序部分。

回想第 3 章，当你创建一个模块时，你会编写它的定义。函数的定义方式与模块类似。以下是函数定义的重要特征。

![](img/c939132f78787c7f339c6977b3fc8c85_260_0.png)

- 函数定义的第一行是函数头（function header），它指定了函数返回的值的数据类型、函数名称以及函数用于接收参数的任何参数变量。
- 紧随函数之后的是函数体（function body），它由在函数被调用时执行的一个或多个语句组成。
- 函数体中的语句之一必须是 Return 语句（返回语句）。Return 语句指定了函数结束时返回的值。

以下是我们在伪代码中编写函数时使用的通用格式：
FunctionName(ParameterList)
statement
statement

> 函数必须有一个 Return 语句。这会导致一个值被发送回给调用它的程序部分。

Return value
End Function

这段伪代码的第一行是函数头，它以函数名开始，后面跟着这些项目：

- DataType 是函数返回的值的数据类型。例如，如果函数返回一个整数，这里将出现 `Integer` 单词。如果函数返回一个实数，这里将出现 `Real` 单词。同样地，如果函数返回一个字符串，这里将出现 `String` 单词。
- FunctionName 是函数的名称。和模块一样，你应该给它一个描述函数功能的名称。在大多数语言中，你遵循与命名变量和模块相同的函数命名规则。
- 可选的参数列表（parameter list）出现在一组括号内。如果函数不接受参数，则将出现一个空参数集。

在函数头之后的行中，会出现一个或多个语句。这些语句即函数体，在每次执行函数时都会执行。语句之一必须是 Return 语句，其形式如下：

Return value

## 6.2 编写你自己的函数

位于 `Return` 单词之后的值是将将发送给调用该函数的程序部分的值。这可以是任何值、变量或具有值的表达式（例如数学表达式）。返回的值必须与函数头中指定的数据类型相同。否则，将发生错误。

定义的最后一行（在函数体之后）是 `End Function`。这一行标记着函数定义的结束。

以下是一个用伪代码编写的函数示例：

```
Function Integer sum(Integer num1, Integer num2)
Declare Integer result
Set result = num1 + num2
Return result
End Function
```

图 6-7 展示了函数头的各个部分。注意该函数返回 `Integer`，函数名称为 `sum`，且函数有两个名为 `num1` 和 `num2` 的 `Integer` 类型参数。

![](img/c939132f78787c7f339c6977b3fc8c85_261_0.png)

该函数的目的是接受两个整数值作为参数并返回它们的和。让我们看看函数体来看看它是如何工作的。第一条语句变量声明了一个名为 `Result` 的本地 `Integer` 变量。下一条语句将 `num1 + num2` 的值赋值给 `result` 变量。接着执行 `Return` 语句，导致函数执行并将 `result` 变量中的值发送给调用该函数的程序部分。

程序 6-6 显示了一个使用该函数的完整伪代码程序。

![](img/c939132f78787c7f339c6977b3fc8c85_261_1.png)

```
1 Module main()
2 // Local variables
3 Declare Integer firstAge, secondAge, total
4 
5 // Get the user's age and the user's
6 // best friend's age.
7 Display "Enter your age."
8 Input firstAge
9 Display "Enter your best friend's age."
10 Input secondAge
11 // Get the sum of ages.
12 Set total = sum(firstAge,secondAge)
13 // Display the sum.
14 Display "Together you are , total, years old."
15 End Module
16 // The sum function accepts two Integer arguments and
17 returns the sum of those arguments as an Integer.
18 Function sum(Integer num1, Integer num2)
19 Declare Integer result
20 Set result = num1 + num2
21 Return result
22 End Function
```

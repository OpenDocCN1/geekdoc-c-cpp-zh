

# 附录 C 伪代码参考 595

Case value_2:
语句
语句
等等。如果 `testExpression` 等于 `value_2`，则执行这些语句。

根据需要插入尽可能多的 Case 部分

Case value_N:
语句
语句
等等。如果 `testExpression` 等于 `value_N`，则执行这些语句。

Default:
语句
语句
等等。如果 `testExpression` 不等于 Case 语句后列出的任何值，则执行这些语句。

End Select 这是该结构的结束。

结构的第一行以 `Select` 语句开始，后跟一个 `testExpression`。在结构内部有一个或多个语句块，它们以 `Case` 语句开头。注意 `Case` 关键字后面跟着一个值。

当 `Case` 语句执行时，它会将该值与每个 `Case` 语句后面的值（从上到下）进行比较。如果找到一个与 `testExpression` 的值匹配的值，程序将跳转到该 `Case` 语句。紧随 `Case` 语句的语句将被执行，然后程序跳出该结构。如果 `testExpression` 不匹配任何 `Case` 值，程序将跳转到 `Default` 语句并执行紧随其后的语句。这是一个示例：

```
Select month
Case 1:
Display "January"
Case 2:
Display "February"
Case 3:
Display "March"
Default:
Display "Error: Invalid month"
```

# While 循环

通用格式：

While 条件
语句
语句
等等。这些语句是循环的主体。当条件为真时重复执行。

End While

```
Select month
语句
语句
```

在通用格式中，条件是一个布尔表达式。`While` 和 `End While` 之间的语句是循环的主体。循环执行时，会测试条件。如果条件为真，则执行循环内的语句；如果条件为假，程序退出循环。以下是一个伪代码示例：

```
Set count = 0
While count < 10
    Display count
    Set count = count + 1
End While
```

# Do-While 循环

通用格式：

```
Do
语句
等等
Until 条件
```

这些语句是循环的主体。当条件为真时重复执行。

在通用格式中，`Do` 和 `Until` 之间的语句是循环的主体。循环执行后，会测试条件。如果条件为真，则重复执行；如果条件为假，程序退出循环。以下是一个示例：

```
Do
    Display count
    Set count = count - 1
Until count == 0
```

# Do-Until 循环

通用格式：

```
Do
语句
等等
While 条件
```

这些语句是循环的主体。当条件为真时重复执行。

在通用格式中，`Do` 和 `While` 之间的语句是循环的主体。循环执行后，会测试条件。如果条件为真，则重复执行；如果条件为假，程序退出循环。以下是一个示例：

```
Set count = 10
Do
    Display count
    Set count = count - 1
While count > 0
```

# For For

```
For 变量 = 起始值 To 结束值
    语句
    等等
```

在通用格式中，`For` 语句后面的语句是循环的主体。循环执行时，会测试变量。

```
For i = 1 To 10
    Display i
```

# For Each Loop

```
For Each 变量 In 集合
    语句
    等等
```

在通用格式中，`For Each` 语句后面的语句是循环的主体。循环执行时，处理集合中的每一个元素。以下是一个示例：

```
Set names = {"apple", "banana", "cherry"}
For Each name In names
    Display name
```

# 定义模块

```
Module 模块名
语句
等等
```

# 调用模块

```
Call 模块名
```

# 参数变量

```
Module 模块名(参数)
```

# 定义函数

```
Function 返回类型 函数名(参数列表)
语句
等等
Return 返回值
```

# 打开输出文件并写入数据

```
Declare 输出文件 文件名
Open 文件名 "文件名.dat"
Write 文件名 "内容"
Close 文件名
```

# 打开输入文件并读取数据

```
Declare 输入文件 文件名
Open 文件名 "文件名.dat"
Read 文件名 变量名
Close 文件名
```


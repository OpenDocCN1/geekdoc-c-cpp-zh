
| C++关键字（续） | | | | |
|---|---|---|---|---|
| continue | decltype | default | delete | do |
| double | dynamic_cast | else | enum | explicit |
| export | extern | false | final | float |
| for | friend | goto | if | import |
| inline | int | long | module | mutable |
| namespace | new | noexcept | not | not_eq |
| nullptr | operator | or | or_eq | override |
| private | protected | public | register | reinterpret_cast |
| return | short | signed | sizeof | static |
| static_assert | static_cast | struct | switch | template |
| this | thread_local | throw | true | try |
| typedef | typeid | typename | union | unsigned |
| using | void | volatile | virtual | wchar_t |
| while | xor | xor_eq | | |
| **C++20新增关键字** | | | | |
| char8_t | concept | consteval | constinit | co_await |
| co_return | co_yield | requires | | |

### 3.4.4 控制语句小结

C++只有三种控制结构，从本章开始，我们将其称为控制语句：

- 顺序，
- 选择（`if`、`if…else`和`switch`）以及
- 迭代（`while`、`do…while`、`for`和基于范围的`for`）。

你根据所实现算法的需要组合这些语句，从而构成每一个程序。我们可以将每个控制语句建模为活动图。每张图都包含初始状态和最终状态，分别表示控制语句的入口点和出口点。单入口/单出口控制语句使构建可读程序变得容易——我们只需使用控制语句堆叠，将一个控制语句的出口点连接到下一个控制语句的入口点。连接控制语句只有另一种方式——控制语句嵌套，即一个控制语句出现在另一个控制语句内部。因此，C++程序中的算法仅由三种控制语句以仅两种方式组合而成。这就是简单的本质。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_157_0.png)

### 检查点

- **1.（填空）** 伯姆和雅各皮尼的工作表明，所有程序都可以只用三种控制结构来编写——______、______和______结构。  
  **答案：** 顺序、选择、迭代。
- **2.（判断题）** while、for和do...while语句执行其操作（或一组操作）零次或多次。  
  **答案：** 错误。while和for语句执行其操作（或一组操作）零次或多次。do...while语句执行其操作（或一组操作）一次或多次。
- **3.（填空）** ________控制语句通过使用控制语句堆叠将一个控制语句的出口点连接到下一个控制语句的入口点，使构建可读程序变得容易。  
  **答案：** 单入口/单出口。

## 3.5 *if* 单选择语句

我们在2.7节简要介绍了`if`单选择语句。程序使用选择语句在备选行动方案中做出选择。例如，假设考试及格分数为60分。以下伪代码表示一个`if`语句，它测试条件“学生成绩大于或等于60”：

```text
if student's grade is greater than or equal to 60
    print "Passed"
```

如果该条件为真，该语句打印“Passed”——否则，`print`语句被忽略。缩进该选择语句的第二行是可选的，但为了清晰起见建议这样做——它强调`print`语句位于`if`语句的语句体中。

前面的伪代码可以用C++写成

```cpp
if (studentGrade >= 60) {
    cout << "Passed";
}
```

这段C++代码与伪代码非常对应。

### bool数据类型

在第2章中，你使用关系运算符或相等运算符创建了条件。实际上，任何求值为零或非零的表达式都可以用作条件。零被视为`false`，非零被视为`true`。C++还提供了数据类型`bool`，用于只能保存值`true`和`false`的布尔变量——这两个值都是C++关键字。编译器可以将`true`隐式转换为`1`，将`false`转换为`0`。

### if语句的UML活动图

以下UML活动图说明了单选择`if`语句。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_158_0.png)

该图包含活动图中最重要的符号——菱形，或称判定符号，它表示需要做出判定。工作流沿着由该符号关联的守卫条件所确定的路径继续，这些条件可以为真或为假。从UML判定符号引出的每条转换箭头都有一个守卫条件（在箭头旁的方括号中指定）。如果守卫条件为真，工作流进入该转换箭头所指向的动作状态。该图表明，如果成绩大于或等于60（即条件为真），程序打印“Passed”，然后转换到活动的最终状态。如果成绩小于60（即条件为假），程序立即转换到最终状态，不显示任何消息。if语句是单入口/单出口控制语句。

### 检查点

- **（伪代码）** 编写一个伪代码*if*语句，判断count是否大于10，如果是，则打印“Count is greater than 10.”
  
  **答案：**
  
  ```text
  if count is greater than 10
      print "Count is greater than 10."
  ```
- **（代码）** 编写一个实现上一练习题伪代码的if语句。假设int变量count已经存在。
  
  **答案：**
  
  ```cpp
  if (count > 10) {
      cout << "Count is greater than 10.";
  }
  ```
- **（填空）** 活动图中的菱形（或称判定符号）表示需要做出判定。工作流沿着由该符号关联的______所确定的路径继续。
  
  **答案：** 守卫条件。

## 3.6 if…else双选择语句

if-then选择语句仅在条件为真时执行指定的操作。if…else双选择语句允许你指定条件为真时要执行的一个操作，以及条件为假时要执行的另一个操作。例如，以下伪代码表示一个if…else语句：如果学生成绩大于或等于60，则打印“Passed”；如果小于60，则打印“Failed”：

```text
if student’s grade is greater than or equal to 60
    print “Passed”
else
    print “Failed”
```

无论哪种情况，在打印发生后，按顺序的下一条语句就会“执行”。前面的if…else伪代码语句可以用C++写成

```cpp
if (studentGrade >= 60) {
    cout << "Passed";
}
else {
    cout << "Failed";
}
```

if和else语句体都采用相同的缩进。无论你选择哪种缩进约定，都应在整个程序中一致应用。如果有多个缩进层级，每一层都应缩进相同的额外空格量。我们倾向于使用三个空格的缩进。IDE通常会为你自动缩进代码。

### if...else语句的UML活动图

下图说明了前面if...else语句中的控制流：

![](img/7b5e2088e71c7f78681d4ddbcf104c06_160_0.png)

### 3.6.1 嵌套if...else语句

程序可以通过将一个if...else语句放在另一个if...else语句内部来测试多种情况，从而创建嵌套if...else语句。例如，以下伪代码表示一个嵌套if...else语句：对于大于或等于90的考试成绩打印"A"，对于80到89的成绩打印"B"，对于70到79的成绩打印"C"，对于60到69的成绩打印"D"，对于所有其他成绩打印"F"。我们使用底纹来突出显示嵌套：

```text
if student’s grade is greater than or equal to 90
   print “A”
else
   if student’s grade is greater than or equal to 80
      print “B”
   else
      if student’s grade is greater than or equal to 70
         print “C”
      else
         if student’s grade is greater than or equal to 60
            print “D”
         else
            print “F”
```




对于输入无效成绩（即 E）的响应。第 12 行调用 GradeBook 成员函数 `displayGradeReport`（在图 5.10 的第 101–111 行定义），该函数根据输入的成绩输出报告（如图 5.11 中的输出所示）。

```cpp
// Fig. 5.11: fig05_11.cpp
// Creating a GradeBook object and calling its member functions.
#include "GradeBook.h" // include definition of class GradeBook

int main()
{
   // create GradeBook object
   GradeBook myGradeBook( "CS101 C++ Programming" );

   myGradeBook.displayMessage(); // display welcome message
   myGradeBook.inputGrades(); // read grades from user
   myGradeBook.displayGradeReport(); // display grade report based on grades
} // end main
```

```text
Welcome to the grade book for
CS101 C++ Programming!

Enter the letter grades.
Enter the EOF character to end input.
a
B
c
C
A
d
f
C
E
Incorrect letter grade entered. Enter a new grade.
D
A
b
^Z

Number of students who received each letter grade:
A: 3
B: 2
C: 3
D: 2
F: 1
```

**图 5.11** | 创建 GradeBook 对象并调用其成员函数。

## switch 语句的 UML 活动图

图 5.12 展示了通用 switch 多重选择语句的 UML 活动图。大多数 switch 语句在每个 case 中使用 break，在处理完该 case 后终止 switch 语句。图 5.12 通过在活动图中包含 break 语句来强调这一点。如果没有 break 语句，在一个 case 处理完后，控制不会转移到 switch 语句之后的第一条语句，而是会转移到下一个 case 的动作。

![](img/b42ba5cd262b1358d16610173f975e4d_212_0.png)

**图 5.12**  带 break 语句的 switch 多重选择语句 UML 活动图。

该图清楚地表明，case 末尾的 break 语句会使控制立即退出 switch 语句。再次注意，（除了初始状态、转移箭头、最终状态和若干注释外）图中还包含动作状态和判定。此外，该图使用合并符号将来自 break 语句的转移合并到最终状态。

使用 switch 语句时，请记住每个 case 只能用于测试一个整型常量表达式——即字符常量和整型常量的任意组合，该组合求值为一个常量整数值。字符常量用单引号中的特定字符表示，例如 'A'。整型常量就是一个整数值。此外，每个 case 标签只能指定一个整型常量表达式。

> **常见编程错误 5.8**
>
> 在 switch 的 case 标签中指定非常量的整型表达式是语法错误。

> **常见编程错误 5.9**
>
> 在 switch 语句中提供相同值的 case 标签是编译错误。

```cpp
// Fig. 5.13: fig05_13.cpp
// break statement exiting a for statement.
#include <iostream>
using namespace std;

int main()
{
    unsigned int count; // control variable also used after loop terminates

    for ( count = 1; count <= 10; ++count ) // loop 10 times
    {
        if ( count == 5 )
            break; // break loop only if count is 5

        cout << count << " ";
    } // end for

    cout << "\nBroke out of loop at count = " << count << endl;
} // end main
```

```text
1 2 3 4
Broke out of loop at count = 5
```

*图 5.13* | *break 语句退出 for 语句。*

控制变量 count 定义在 for 语句头之外，这样我们既可以在*循环体内*使用这个控制变量，也可以在*循环执行完成之后*使用它。

## continue 语句

*continue 语句*在 while、for 或 do...while 语句中执行时，会跳过该语句主体中剩余的语句，并继续循环的下一次迭代。在 while 和 do...while 语句中，循环继续测试在 continue 语句执行后立即求值。在 for 语句中，先执行增量表达式，然后对循环继续测试求值。

图 5.14 在 for 语句中使用 continue 语句（第 11 行），当嵌套的 if（第 10–11 行）确定 count 的值为 5 时，跳过输出语句（第 13 行）。当 continue 语句执行时，程序控制继续执行 for 头中的控制变量增量（第 8 行），再循环五次。

```cpp
// Fig. 5.14: fig05_14.cpp
// continue statement terminating an iteration of a for statement.
#include <iostream>
using namespace std;

int main()
{
    for ( unsigned int count = 1; count <= 10; ++count ) // loop 10 times
    {
        if ( count == 5 )  // if count is 5,
            continue;       // skip remaining code in loop

        cout << count << " ";
    } // end for

    cout << "\nUsed continue to skip printing 5" << endl;
} // end main
```

```text
1 2 3 4 6 7 8 9 10
Used continue to skip printing 5
```

*图 5.14* | continue 语句终止 for 语句的一次迭代。

在 5.3 节中，我们指出在大多数情况下可以使用 while 语句来表示 for 语句。唯一的例外是当 while 语句中的增量表达式在 continue 语句之后时。在这种情况下，增量不会在程序测试循环继续条件之前执行，while 语句也不会像 for 语句那样执行。

> **良好编程实践 5.5**
>
> 有些程序员认为 break 和 continue 违反了结构化编程。这些语句的效果可以通过我们很快将学习的结构化编程技术来实现，因此这些程序员不必使用 break 和 continue。大多数程序员认为在 switch 语句中使用 break 是可以接受的。

> **软件工程观察 5.1**
>
> 在实现高质量软件工程和实现最佳性能软件之间存在矛盾。通常，其中一个目标是以牺牲另一个目标为代价实现的。除了对性能要求最苛刻的情况外，请遵循以下准则：首先，让你的代码简单且正确；然后，只有在必要时才使其又快又小。

## 5.8 逻辑运算符

到目前为止，我们只研究了简单条件，例如 `counter <= 10`、`total > 1000` 和 `number != sentinelValue`。我们使用关系运算符 `>`、`<`、`>=` 和 `<=` 以及相等运算符 `==` 和 `!=` 来表达这些条件。每个判定恰好测试一个条件。为了在做出决策时测试多个条件，我们可以在单独的语句中或嵌套的 if 或 if...else 语句中执行这些测试。

C++ 提供了逻辑运算符，用于通过组合简单条件来形成更复杂的条件。这些逻辑运算符是 `&&`（逻辑与）、`||`（逻辑或）和 `!`（逻辑非，也称为逻辑否定）。

### 逻辑与（&&）运算符

假设我们希望确保两个条件都为真时才选择某条执行路径。在这种情况下，我们可以使用 `&&`（逻辑与）运算符，如下所示：

```cpp
if ( gender == FEMALE && age >= 65 )
   ++seniorFemales;
```

这个 if 语句包含两个简单条件。条件 `gender == FEMALE` 在此用于判断一个人是否为女性。条件 `age >= 65` 判断一个人是否为老年人。`&&` 运算符左侧的简单条件首先求值。如有必要，`&&` 运算符右侧的简单条件接着求值。正如我们稍后将讨论的，逻辑与表达式的右侧只有在左侧为真时才会求值。然后 if 语句会考虑组合条件

```cpp
gender == FEMALE && age >= 65
```

该条件当且仅当**两个**简单条件都为真时才为真。最后，如果这个组合条件确实为真，if 语句体中的语句会将 `seniorFemales` 的计数加 1。如果两个简单条件中的任何一个（或两个）为假，程序就会跳过递增操作，继续执行 if 之后的语句。通过在组合条件中添加冗余的括号，可以使其更具可读性：

```cpp
( gender == FEMALE ) && ( age >= 65 )
```

> **常见编程错误 5.10**
>
> 尽管 `3 < x && x < 7` 在数学上是正确的条件，但在 C++ 中其求值结果可能并非你所期望。请使用 `( 3 < x && x < 7 )` 在 C++ 中获得正确的求值。

图 5.15 总结了 `&&` 运算符。该表显示了 *expression1* 和 *expression2* 的假和真值的所有四种可能组合。这样的表通常称为**真值表**。C++ 会将所有包含关系运算符、相等运算符和/或逻辑运算符的表达式求值为假或真。

| 表达式1 | 表达式2 | 表达式1 && 表达式2 |
|---|---|---|
| 假 | 假 | 假 |
| 假 | 真 | 假 |
| 真 | 假 | 假 |
| 真 | 真 | 真 |

**图 5.15**  `&&`（逻辑与）运算符真值表。

### 逻辑或（||）运算符

现在让我们考虑 `||`（逻辑或）运算符。假设我们希望确保两个条件中的一个或两个为真时才选择某条执行路径。在这种情况下，我们使用 `||` 运算符，如下面的程序片段所示：

```cpp
if ( ( semesterAverage >= 90 ) || ( finalExam >= 90 ) )
    cout << "Student grade is A" << endl;
```

前面的条件包含两个简单条件。简单条件 `semesterAverage >= 90` 用于判断学生是否因为整个学期的扎实表现而应获得课程“A”等成绩。简单条件


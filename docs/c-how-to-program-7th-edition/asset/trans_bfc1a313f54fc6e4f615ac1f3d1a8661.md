
![](img/023f159fdd47d944d48e08843cea732d_156_0.png)

> **性能提示 4.2**
>
> *在嵌套的 if...else 语句中，将更可能为真的条件放在嵌套语句的开头进行测试。与先测试频繁出现的情况相比，这会使嵌套的 if...else 语句更早退出，从而运行得更快。*

## 悬空 else 问题

C++ 编译器总是将 else 与紧邻其前的 if 关联，除非通过花括号（{ 和 }）的位置另有指示。这种行为可能导致所谓的悬空 else 问题。例如，

```cpp
if ( x > 5 )
    if ( y > 5 )
        cout << "x and y are > 5";
    else
        cout << "x is <= 5";
```

看起来表示如果 x 大于 5，则嵌套的 if 语句决定 y 是否也大于 5。如果是，则输出 "x and y are > 5"。否则，看起来如果 x 不大于 5，则 if...else 的 else 部分输出 "x is <= 5"。

注意！这个嵌套的 if...else 语句并不像看起来那样执行。编译器实际上将该语句解释为

```cpp
if ( x > 5 )
    if ( y > 5 )
        cout << "x and y are > 5";
    else
        cout << "x is <= 5";
```

其中第一个 if 的主体是一个嵌套的 if...else。外层 if 语句测试 x 是否大于 5。如果是，则继续测试 y 是否也大于 5。如果第二个条件为真，则显示正确的字符串——"x and y are > 5"。然而，如果第二个条件为假，则显示字符串 "x is <= 5"，即使我们知道 x 大于 5。

要强制嵌套的 if...else 语句按原本意图执行，我们可以将其写为如下形式：

```cpp
if ( x > 5 )
{
    if ( y > 5 )
        cout << "x and y are > 5";
}
else
    cout << "x is <= 5";
```

花括号（{}）向编译器指示第二个 if 语句位于第一个 if 的主体中，并且 else 与第一个 if 关联。练习 4.23–4.24 进一步探讨悬空 else 问题。

## 块

if 选择语句的主体中只期望有一条语句。类似地，if...else 语句的 if 和 else 部分各期望只有一条主体语句。要包含多个

从该点开始。此外，每个从判定符号指出的转换箭头旁边都有一个守卫条件。合并符号有两条或更多转换箭头指向菱形，且只有一条转换箭头从菱形指出，表示多个活动流合并以继续活动。与判定符号不同，合并符号在 C++ 代码中没有对应物。

![](img/023f159fdd47d944d48e08843cea732d_159_0.png)

**图 4.6** | *while 重复语句的 UML 活动图。*

图 4.6 的图清晰地展示了本节前面讨论的 while 语句的重复。从动作状态引出的转换箭头指向合并，合并再转换回每次循环中都要测试的判定，直到守卫条件 product > 100 变为真。然后 while 语句退出（到达其最终状态），控制按程序中的顺序传递给下一条语句。

想象一个很深的箱子，里面装满了空的 UML 重复语句活动图——数量多到你可能需要将它们与其他控制语句的活动图堆叠和嵌套，以形成算法的结构化实现。你用适合该算法的动作表达式和守卫条件填充动作状态和判定符号。

> **性能提示 4.3**
>
> *本文提到的许多性能提示只能带来很小的改进，因此你可能会想忽略它们。然而，对于在循环中执行很多次的代码，小的性能改进可以带来显著的整体性能提升。*

## 4.8 算法制定：计数器控制的重复

为了说明程序员如何开发算法，本节和 4.9 节解决班级平均分问题的两个变体。考虑以下问题陈述：

> *一个班有十名学生参加了一次测验。这次测验的成绩（0 到 100 范围内的整数）已提供给你。计算并显示所有学生成绩的总分以及该测验的班级平均分。*

班级平均分等于成绩总和除以学生人数。在计算机上解决这个问题的算法必须输入每个成绩，计算平均分并打印结果。

### 使用计数器控制重复的伪代码算法

让我们使用伪代码列出要执行的动作，并指定这些动作应发生的顺序。我们使用计数器控制的重复来一次输入一个成绩。这种技术使用一个称为计数器的变量来控制一组语句将执行的次数（也称为循环的迭代次数）。

计数器控制的重复通常称为确定性重复，因为重复次数在循环开始执行之前就已知。在此示例中，当计数器超过 10 时重复终止。本节展示一个完整开发的伪代码算法（图 4.7）以及一个在 C++ 中实现该算法的 GradeBook 类版本（图 4.8–图 4.9）。成员函数 getAverage，当与一个演示该算法实际运行的应用（图 4.10）一起呈现时。在 4.9 节中，我们演示如何使用伪代码从头开发这样的算法。

> **软件工程观察 4.3**
>
> *经验表明，在计算机上解决问题最困难的部分是开发解决方案的算法。从算法生成可工作的 C++ 程序的过程通常是直接的。*

![](img/023f159fdd47d944d48e08843cea732d_160_0.png)

```text
1  Set total to zero
2  Set grade counter to one
3
4  While grade counter is less than or equal to ten
5      Prompt the user to enter the next grade
6      Input the next grade
7      Add the grade into the total
8      Add one to the grade counter
9
10 Set the class average to the total divided by ten
11 Print the total of the grades for all students in the class
12 Print the class average
```

**图 4.7**  使用计数器控制重复解决班级平均分问题的伪代码。

注意图 4.7 的伪代码算法中对 total 和 counter 的引用。total 是用于累加多个值之和的变量。counter 是用于计数的变量——在此情况下，grade counter 指示用户即将输入 10 个成绩中的哪一个。用于存储 total 的变量在程序中使用前通常初始化为零；否则，总和将包括存储在 total 内存位置中的先前值。

### 增强 GradeBook 验证

让我们考虑对 GradeBook 类所做的一项增强。在图 3.16 中，我们的 setCourseName 成员函数使用 if 语句测试课程名称的长度是否小于或等于 25 个字符，以此验证课程名称。如果为真，则设置课程名称。此代码之后是一个 if 语句，测试课程名称的长度是否大于 25 个字符（在这种情况下，课程名称将被缩短）。第二个 if 语句的条件与第一个 if 语句的条件完全相反。如果一个条件求值为真，另一个必定求值为假。这种情况非常适合 if...else 语句，因此我们修改了代码，用一条 if...else 语句替换两条 if 语句（图 4.9 的第 18–25 行）。

### 在 GradeBook 类中实现计数器控制的重复

GradeBook 类（图 4.8–图 4.9）包含一个构造函数（在图 4.8 的第 11 行声明，并在图 4.9 的第 9–12 行定义），它为该类的数据成员 courseName（在图 4.8 的第 17 行声明）赋值。图 4.9 的第 16–26 行、29–32 行和 35–39 行分别定义了成员函数 setCourseName、getCourseName 和 displayMessage。第 42–68 行定义了成员函数 determineClassAverage，它实现图 4.7 中伪代码所描述的班级平均分算法。

```cpp
1  // Fig. 4.8: GradeBook.h
2  // Definition of class GradeBook that determines a class average.
3  // Member functions are defined in GradeBook.cpp
4  #include <string> // program uses C++ standard string class
5  using namespace std;
6
7  // GradeBook class definition
8  class GradeBook
9  {
10 public:
11    GradeBook( string ); // constructor initializes course name
12    void setCourseName( string ); // function to set the course name
13    string getCourseName(); // function to retrieve the course name
14    void displayMessage(); // display a welcome message
15    void determineClassAverage(); // averages grades entered by the user
16 private:
17    string courseName; // course name for this GradeBook
18 }; // end class GradeBook
```

**图 4.8** | 使用计数器控制重复的班级平均分问题：GradeBook 头文件。

```cpp
1  // Fig. 4.9: GradeBook.cpp
2  // Member-function definitions for class GradeBook that solves the
3  // class average program with counter-controlled repetition.
4  #include <iostream>
5  #include "GradeBook.h" // include definition of class GradeBook
6  using namespace std;
7
8  // constructor initializes courseName with string supplied as argument
9  GradeBook::GradeBook( string name )
10 {
```

**图 4.9** | 使用计数器控制重复的班级平均分问题：GradeBook 源代码文件。（第 1 部分，共 3 部分。）


## 伪代码语句

```
Display a summary of the exam results and decide whether a bonus should be paid
```

可以细化如下：

```
Display the number of passes
Display the number of failures
If more than eight students passed
    Display “Bonus to instructor”
```

完整的第二次细化如图4.15所示。空行将While结构分隔开，以提高可读性。该伪代码现在已足够细化，可转换为C++。

```
1  Initialize passes to zero
2  Initialize failures to zero
3  Initialize student counter to one

5  While student counter is less than or equal to 10
6      Prompt the user to enter the next exam result
7      Input the next exam result

9      If the student passed
10         Add one to passes
11     Else
12         Add one to failures

14     Add one to student counter

16 Display the number of passes
17 Display the number of failures

19 If more than eight students passed
20     Display “Bonus to instructor”
```

**图 4.15** | 考试结果问题的伪代码。

## 转换为类分析

实现该伪代码算法的程序如图4.16所示。此示例不包含类——它只包含一个源代码文件，其中函数main执行应用程序的所有工作。在本章和第3章中，你已看到由一个类（包括该类的头文件和源代码文件）以及另一个测试该类的源代码文件组成的示例。该源代码文件包含函数main，它创建该类的一个对象并调用其成员函数。偶尔，当试图创建一个可复用类来演示某个概念并不合理时，我们会使用一个完全包含在单个源代码文件的main函数中的示例。

```
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed 9
Failed 1
Bonus to instructor!
```

**图 4.16** | 考试结果问题：嵌套控制语句。（第2部分，共2部分。）

第9–12行声明用于处理考试结果的变量。我们利用了C++的一项特性，该特性允许将变量初始化并入声明中（passes初始化为0，failures初始化为0，studentCounter初始化为1）。循环程序可能需要在每次重复开始时进行初始化；此类重新初始化通常由赋值语句完成，而不是在声明中完成，也不是通过把声明移到循环体内部来完成。

while语句（第15–29行）循环10次。每次迭代输入并处理一个考试结果。用于处理每个结果的if...else语句（第22–25行）嵌套在while语句中。如果结果为1，if...else语句递增passes；否则，它假定结果为2并递增failures。第28行在第15行再次测试循环条件之前递增studentCounter。输入10个值后，循环终止，第32行显示通过人数和未通过人数。第35–36行的if语句判断是否有超过八名学生通过考试，如果是，则输出消息"Bonus to instructor!"。

图4.16显示了该程序两次示例执行的输入和输出。第二次示例执行结束时，第35行的条件为真——超过八名学生通过了考试，因此程序输出一条消息，表明教师应获得奖金。

## 4.11 赋值运算符

C++提供了若干赋值运算符来缩写赋值表达式。例如，语句

```
c = c + 3;
```

可以用加法赋值运算符+=缩写为

```
c += 3;
```

它将运算符右侧表达式的值加到运算符左侧变量的值上，并将结果存储在左侧变量中。任何如下形式的语句

```
variable = variable operator expression;
```

其中同一变量出现在赋值运算符两侧，且该运算符是二元运算符+、-、*、/或%之一（文中稍后还会讨论另外几个运算符），都可以写成如下形式

```
variable operator= expression;
```

因此赋值c += 3将3加到c上。图4.17展示了算术赋值运算符、使用这些运算符的示例表达式以及说明。

*假设：int c = 3, d = 5, e = 4, f = 6, g = 12;*

| 赋值运算符 | 示例表达式 | 说明 | 赋值结果 |
|---|---|---|---|
| += | c += 7 | c = c + 7 | 将10赋给c |
| -= | d -= 4 | d = d - 4 | 将1赋给d |
| *= | e *= 5 | e = e * 5 | 将20赋给e |
| /= | f /= 2 | f = f / 2 | 将2赋给f |
| %= | g %= 9 | g = g % 9 | 将3赋给g |

**图 4.17**  |  算术赋值运算符。

## 4.12 递增和递减运算符

除了算术赋值运算符外，C++还提供两个一元运算符，用于将数值变量的值加1或减1。它们是一元递增运算符++和一元递减运算符--，总结于图4.18。程序可以使用递增运算符++将名为c的变量的值加1，而不是使用表达式c = c + 1或c += 1。放在变量前面（置于变量*之前*）的递增或递减运算符分别称为**前置递增**或**前置递减**运算符。放在变量后面（置于变量*之后*）的递增或递减运算符分别称为**后置递增**或**后置递减**运算符。

| 运算符 | 名称 | 示例表达式 | 说明 |
|---|---|---|---|
| ++ | 前置递增 | ++a | 将a递增1，然后在包含a的表达式中使用a的新值。 |
| ++ | 后置递增 | a++ | 在包含a的表达式中使用a的当前值，然后将a递增1。 |
| -- | 前置递减 | --b | 将b递减1，然后在包含b的表达式中使用b的新值。 |
| -- | 后置递减 | b-- | 在包含b的表达式中使用b的当前值，然后将b递减1。 |

**图 4.18**  |  递增和递减运算符。

使用前置递增（或递减）运算符将变量加（或减）1，称为对该变量进行前置递增（或前置递减）。前置递增（或前置递减）使变量递增（递减）1，然后在变量所在的表达式中使用该变量的新值。使用后置递增（或递减）运算符将变量加（或减）1，称为**后置递增**（或**后置递减**）。后置递增（或后置递减）使变量的*当前*值用于其所在的表达式中，然后将变量的值递增（递减）1。

![](img/bfd978e7e9b192bab46ec2a89e481263_169_0.png)

### 良好编程实践 4.5

与二元运算符不同，一元递增和递减运算符应紧挨其操作数放置，中间不留空格。

图4.19演示了++递增运算符的前置递增版本和后置递增版本之间的区别。递减运算符（--）的工作方式类似。

```cpp
// Fig. 4.19: fig04_19.cpp
// Preincrementing and postincrementing.
#include <iostream>
using namespace std;

int main()
{
    int c;

    // demonstrate postincrement
    c = 5; // assign 5 to c
    cout << c << endl; // print 5
    cout << c++ << endl; // print 5 then postincrement
    cout << c << endl; // print 6

    cout << endl; // skip a line

    // demonstrate preincrement
    c = 5; // assign 5 to c
    cout << c << endl; // print 5
    cout << ++c << endl; // preincrement then print 6
    cout << c << endl; // print 6
} // end main
```

```text
5
5
6

5
6
6
```

**图 4.19** | 前置递增和后置递增。

第11行将c初始化为5，第12行输出c的初始值。第13行输出表达式c++的值。这会后置递增变量c，因此输出c的原始值（5），然后将c的值递增。因此，第13行再次输出c的初始值（5）。第14行输出c的新值（6），以证明该变量的值在第13行已递增。第19行将c的值重置为5，第20行输出该值。第21行输出表达式++c的值。该表达式前置递增c，因此其值先递增，然后

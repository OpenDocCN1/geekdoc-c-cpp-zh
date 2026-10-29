

# 选择

![](img/202cface8244f523c2641baa2e00d7dd_169_0.png)

**图 4.3** 单向 if 语句

这种修改形式的 if 语句称为 **单向 if 语句**。程序 4.3 使用此语句检查汽车的里程，并在行驶里程超过 3000.0 英里的汽车上仅显示一条消息。

# 程序 4.3

```
```cpp
#include <iostream>
using namespace std;

int main()
{

    const double LIMIT = 3000.0;
    int idNum;
    double miles;

    cout << "Please type in car number and mileage: ";
    cin  >> idNum >> miles;
```

```
if(miles > LIMIT)
    cout << " Car " << idNum << " is over the limit." << endl;

    cout << "End of program output." << endl;

    return 0;
}
```

为展示单向选择条件的作用，程序 4.3 运行了两次，每次使用不同的输入数据。只有第一次运行的输入数据会导致消息 Car 256 is over the limit 被显示。

```
Please type in car number and mileage: 256 3562.8
Car 256 is over the limit.
End of program output.
```

and

```
Please type in car number and mileage: 23 2562.3
End of program output.
```

# 与 if-else 语句相关的问题

在使用 C++ 的 if-else 语句时遇到的两个最常见问题如下：

- 对表达式的全部含义理解不足
- 使用赋值运算符 = 代替关系运算符 ==

请记住，表达式是任何产生结果的操作数和运算符的组合。此定义比乍看之下要广泛得多。例如，以下所有内容都是有效的 C++ 表达式：

```
age + 5
age = 30
age == 40
```

假设变量声明正确，每个表达式都会产生一个结果。以下示例使用 cout 对象在 age 最初被赋值为 18 时显示这些表达式的值：

```
age = 18;
cout << "The value of the first expression is " << (age + 5) << endl;
cout << "The value of the second expression is " << (age = 30) << endl;
cout << "The value of the third expression is " << (age == 40) << endl;
```

# 信息点

# 布尔数据类型

在当前的 ANSI/ISO C++ 标准之前，C++ 没有内置的布尔数据类型及其两个布尔值 true 和 false。因为该数据类型最初不是语言的一部分，所以经过测试的表达式不能求值为布尔值。因此，语法

```
if (Boolean expression is true)
    execute this statement;
```

也没有内置到 C 或 C++ 中。相反，C++ 使用更全面的语法，

```
if (expression)
    execute this statement;
```

其中 expression 是求值为数值表达式的任何表达式。如果测试表达式的值是非零值，则被视为 true，而只有零值被视为 false。

正如 ANSI/ISO C++ 标准所规定，C++ 具有包含值 true 和 false 的内置布尔数据类型。布尔变量使用 bool 关键字声明。如当前实现，布尔值 true 和 false 代表的实际值是整数值 1 和 0。例如，检查以下声明两个布尔变量的程序：

```
#include <iostream>
using namespace std;
int main()
{
    bool t1, t2;

    t1 = true;
    t2 = false;
    cout << "The value of t1 is " << t1
         << "\nand the value of t2 is " << t2 << endl;

    return 0;
}
```

此程序产生以下输出：

```
The value of t1 is 1
and the value of t2 is 0
```

# 信息点

# 布尔数据类型（续）

如该输出所示，布尔值 true 和 false 由整数值 1 和 0 表示，并具有以下关系：

```
!true = is false
!false = is true
```

此外，对类型为 bool 的变量应用后缀或前缀 ++ 运算符会将布尔值设置为 true。不能对布尔变量应用后缀和前缀 -- 运算符。

布尔值也可以进行比较，如以下代码所示：

```
if (t1 == t2)
    cout << "The values are equal" << endl;
else
    cout << "The values are not equal" << endl;
```

最后，将任何非零值赋给布尔变量会使变量设置为 true（值为 1），而将零值赋给布尔变量会使变量设置为 false（值为 0）。

# 练习 4.2

- 1. （练习）为以下条件编写合适的 if 语句：

- a. 如果角度等于 90 度，打印消息“角度为直角。”；否则，打印消息“角度不是直角。”

- b. 如果温度高于 100 度，显示消息“高于水的沸点”；否则，显示消息“低于水的沸点。”

- c. 如果数字为正，将数字加到变量 positivesum；否则，将数字加到变量 negativesum。

- d. 如果斜率小于 0.5，将变量 flag 设置为 0；否则，将 flag 设置为 1。

- e. 如果 slope1 和 slope2 之间的差小于 0.001，将变量 approx 设置为 0；否则，将 approx 计算为 (slope1 - slope2) / 2.0。

- f. 如果频率高于 60，显示消息“频率过高。”

- g. 如果 temp1 和 temp2 之间的差超过 2.3，将变量 error 计算为 (temp1 - temp2) * factor。

- h. 如果 x 大于 y 且 z 小于 20，提示用户输入变量 p 的值。

- i. 如果 distance 大于 20 且小于 35，提示用户输入变量 time 的值。

# 第 4 章

2. （练习）编写与以下流程图所示条件相对应的 if 语句：

![](img/202cface8244f523c2641baa2e00d7dd_174_0.png)

![](img/202cface8244f523c2641baa2e00d7dd_174_1.png)

![](img/202cface8244f523c2641baa2e00d7dd_174_2.png)

![](img/202cface8244f523c2641baa2e00d7dd_174_3.png)

# 选择

- 3. **（练习）** 编写一个 C++ 程序，要求用户输入两个数字。如果输入的第一个数字大于第二个数字，程序应打印消息“第一个数字更大。”；否则，应打印消息“第一个数字更小。”通过输入数字 5 和 8 然后使用数字 11 和 2 测试你的程序。如果输入的两个数字相等，你认为你的程序会显示什么？测试此情况。

- 4. **（程序）**
  - a. 在及格/不及格课程中，如果成绩大于或等于 70，则学生通过；如果成绩低于 70，则不及格。编写一个 C++ 程序接受成绩并打印消息“A passing grade”或“A failing grade”，视情况而定。
  - b. 为了验证练习 4a 编写的程序是否正常运行，你应该进行多少次运行？每次程序运行应输入什么数据？

- 5. **（程序）**
  - a. 如果某笔钱在银行存放超过 5 年，银行按 4.5% 的利率支付利息；否则，利率为 3.0%。编写一个 C++ 程序，使用 cin 对象接受变量 numYears 中的年数，并根据输入到 numYears 的值显示正确的利率。
  - b. 为了验证练习 5a 编写的程序是否正常运行，你应该进行多少次运行？每次程序运行应输入什么数据？

- 6. **（练习）**
  - a. 编写一个 C++ 程序，根据输入显示消息“PROCEED WITH TAKEOFF”或“ABORT TAKEOFF”。如果变量 code 中输入字符 g，则应显示第一条消息；否则应显示第二条消息。
  - b. 为了验证练习 6a 编写的程序是否正常运行，你应该进行多少次运行？每次程序运行应输入什么数据？

- 7. **（程序）** 编写、编译并运行一个 C++ 程序，接受用户输入的整数并判断其为偶数还是奇数。输出应显示消息“The entered number is even.”或“The entered number is odd.”，对应用户输入的数字。*（提示：偶数除以 2 的余数为 0。）*

- 8. **（程序）** 编写、编译并运行一个 C++ 程序，接受用户输入的数字并计算平方根和倒数。在计算平方根之前，验证该数字不为负；在计算倒数之前，检查该数字不为零。如果出现任一条件，显示一条消息说明该运算无法计算。

- 9. **（程序）** 能被 400 整除的年份或能被 4 整除但不能被 100 整除的年份为闰年。例如，由于 1600 能被 400 整除，1600 年是闰年。同样，由于 1988 能被 4 整除但不能被 100 整除，它也是闰年。利用此信息，编写一个 C++ 程序接受年份作为用户输入，判断该年份是否为闰年，并显示一条消息告知用户输入的年份是否为闰年。

- 10. **（程序）**
  - a. 编写、编译并运行一个 C++ 程序来计算并显示一个人的周薪，条件如下：如果工作时间小于或等于 40 小时，个人每小时获得 $12.00；否则，个人获得 $480.00 加上


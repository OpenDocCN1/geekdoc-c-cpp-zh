

# 算术运算符

程序随后将用户输入的选课学生人数赋值给 `added`。此后，程序使用加法运算符将两个操作数 `total` 和 `added` 相加。得到的和被赋值给 `total`，它现在反映了课程中所有学生的数量，包括预注册和后续选课的学生。然后将其输出。

```cpp
#include <iostream>
using namespace std;
int main() {
    int total, added;
    cout << "Enter number of pre-registered students: ";
    cin >> total;
    cout << "Enter number of students adding the course: ";
    cin >> added;
    total = total + added;
    cout << "Total number of students: " << total;
    return 0;
}
```

该程序的输入和输出可以是：
Enter number of registered students: 30
Enter number of students adding the course: 3
Total number of students: 33

## 复合赋值与算术运算符

新程序员会对像 `total = total + added` 这样的语句感到困惑，因为在数学中，一个变量不能等于加号另一个变量。然而，这种语句并不是在数学中，而是在 C++ 编程中， `=` 运算符不是用于相等，而是用于赋值。

尽管如此，还有另一种方式可以表示 `total = total + added`：
`total += added;`

对于编译器来说，使用 `total = total + added` 还是 `total += added` 没有区别。然而，许多程序员更倾向于使用 `total += added`，因为它看起来更优雅，另人认为它可读性更高，而且出于实用考虑，它需要的字符更少。

这种算术运算符和赋值运算符的紧凑结合不仅限于加法运算符。如表 4-2 所示，它也可以与其他算术运算符一起。这里假设 `a` 是之前声明的整型变量。

## 表 4-2：算术运算符与赋值运算符的结合

| 语句 | 结合运算符 |
| --- | --- |
| a = a + 2; | a += 2; |
| a = a - 2; | a -= 2; |
| a = a * 2; | a *= 2; |
| a = a / 2; | a /= 2; |
| a = a % 2; | a %= 2; |

# 算术赋值运算符之间的优先级

语句 `total = total + added` 使用了两个运算符：赋值和算术。算术运算的优先级高于赋值运算。这意味着加法在赋值之前执行。直观来说这比另一种顺序更有意义。然而，正如我将在本中详细解释的，当一个语句中使用多个运算符时，也会出现优先级，那里正确的顺序并不那么直观。

# 溢出与下溢

溢出和下溢适用于加法的结果。在我的编译器和操作系统上，`int` 数据类型的范围是 -2,147,483,648 到 2,147,483,647。以下是我从一个巨大的预注册人数 2,147,483,647 开始，然后增加一个学生的结果：

- Enter number of prereistered students: 2147483647
- Enter number of students adding the course: 1
- Total number of students: -2147483648

虽然负数输入在这个程序中没有意义，因为你不能有负数的学生选课或增加一个课程，但其他程序可能会使用负数，例如零度以下的温度。因此，以下输入使用负数来说明使用加法运算符的下溢。

- Enter number of prereistered students: -2147483648
- Enter number of students adding the course: -1
- Total number of students: 2147483647

# 字符串相加

当我们考虑相加数值操作数时，加法运算符也可以用于字符串操作数。以下代码的输出是："Your name is JeffKent."。

```cpp
#include <iostream>
#include <string>
using namespace std;
int main(void)
{
    string firstName = "Jeff";
    string lastName = "Kent";
    cout << "Your name is " << firstName + lastName;
    return 0;
}
```

相两个字符串的效果是将第二个字符串操作数附加到第一个字符串操作数之后。加意味着将第二个字符串的内容添加到第一个字符串的末尾。

虽然你可以将数字加数字，或者将字符串加字符串，但尝试将数字和字符串相加会导致编译器错误。加法运算符可以对两个数值操作数执行算术运算，或对两个字符串操作数执行追加操作，但它不知道如何将一个数值操作数和一个字符串操作数相加。

# 减法运算符

在我教学的社区学院，学生离开课程的同时也在加入。一些预注册的学生从未出现过。其他后来出现的学生决定退课。

以下程序在我们使用的加法运算符程序的基础上增加了一个整型变量 `dropped`，用于那些我因为从未出现而删除的学生，或者自己退课的学生。`dropped` 变量由用户赋值。程序使用减法运算符更新 `total`。

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    int total, dropped, added;
    cout << "Enter number of pre-registered students: ";
    cin >> total;
    cout << "Enter number of students adding the course: ";
    cin >> added;
    total = total + added;
    cout << "How many students dropped? ";
    cin >> dropped;
    total -= dropped;
    cout << "Total number of students: " << total;
    return 0;
}
```
*(注：原文示例代码中 `added` 变量未定义，此处为翻译逻辑保持一致，但在实际代码中需定义)*

该程序的输入输出可以是：
Enter number of registered students: 30
Enter number of students adding the course: 3
How many students dropped? 5
Total number of students: 28

# 乘法运算符

回到我的社区学院例子，所有入学的学生都欠 72 元学费，即使他们从未出现或后来退课。

以下程序在我们使用的加法运算符程序的基础上添加了以下内容：

```cpp
cout << "Total tuition owed: $" << (total + dropped) * 72;
```

程序现在是：

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    int total, added, dropped;
    cout << "Enter number of pre-registered students: ";
    cin >> total;
    cout << "Enter number of students adding the course: ";
    cin >> added;
    total = total + added;
    cout << "How many students dropped? ";
    cin >> dropped;
    total -= dropped;
    cout << "Total number of students: " << total << endl;
    cout << "Total tuition owed: $" << (total + dropped) * 72 << endl;
    return 0;
}
```

该程序的输入和输出可以是
Enter number of prereistered students: 30
Enter number of students adding the course: 3
How many students dropped? 5
Total number of students: 28
Total tuition owed: $2376

# 算术运算符之间的优先级

语句我们使用了两个算术运算符：加法和乘法。两个算术运算的执行顺序会有区别。如果先执行加法，28+5，然后将和 3 乘以 72，结果是 2376。然而，如果先执行乘法，5*72，然后将积 30 加到 28，结果将是 388。

C++ 有规则，称为优先级，用来决定哪个操作先执行。优先级在本章之前的加法运算符高于赋值运算符的部分中讨论过。然而，现在的问题是算术运算符之间的优先级。

表 4-3 列出了算术运算符之间的优先级。

| 优先级 | 运算符 |
|---|---|
| 最高 | - (一元取反) |
| 中间 | * / % |
| 最低 | + |

当表 4-3 中同一行有多个运算符时，这些运算符具有相同的优先级




## 自测练习

21. 编写一个 if-else 语句，如果变量 score 的值大于 100 则输出单词 High，如果 score 的值最多为 100 则输出 Low。变量 score 的类型为 int。

22. 假设 savings 和 expenses 是类型为 double 的变量，并且已赋予值。编写一个 if-else 语句，如果 savings 至少与 expenses 一样大，则输出单词 Solvent，减少 savings 的值使其减去 expenses 的值，并将 expenses 的值设为 0。否则，如果 savings 小于 expenses，则 if-else 语句仅输出单词 Bankrupt，并且不改变任何变量的值。

23. 编写一个 if-else 语句，如果变量 exam 的值大于或等于 60 且变量 programs_done 的值大于或等于 10，则输出单词 Passed。否则，if-else 语句输出单词 Failed。变量 exam 和 programs_done 均为类型 int。

24. 编写一个 if-else 语句，如果变量 temperature 的值大于或等于 100，或者变量 pressure 的值大于或等于 200，或者两者都满足，则输出单词 Warning。否则，if-else 语句输出单词 OK。变量 temperature 和 pressure 均为类型 int。

25. 考虑一个二次表达式，例如

x² - x - 2

描述该二次式为正（即大于 0）涉及描述一个数集，该数集要么小于较小的根（为 -1），要么大于较大的根（为 +2）。编写一个 C++ 布尔表达式，当该公式具有正值时为真。

26. 考虑二次表达式

x² - 4x + 3

描述该二次式为负涉及描述一个数集，该数集同时大于较小的根（+1）且小于较大的根（+3）。编写一个 C++ 布尔表达式，当该二次式的值为负时为真。

27. 以下嵌入在这些 if-else 语句中的 cout 语句的输出是什么？你应假设这些语句嵌入在一个完整正确的程序中。解释你的答案。

## DISPLAY 2.12 一个 while 循环

```
1  #include <iostream>
2  using namespace std;
3  int main()
4  {
5      int countDown;
6      cout << "How many greetings do you want? ";
7      cin >> countDown;
8      while (countDown > 0)
9      {
10         cout << "Hello ";
11         countDown = countDown - 1;
12     }
13     cout << endl;
14     cout << "That's all!\n";
15     return 0;
16 }
```

### Sample Dialogue 1

How many greetings do you want? 3
Hello Hello Hello
That's all!

### Sample Dialogue 2

How many greetings do you want? 1
Hello
That's all!

### Sample Dialogue 3

How many greetings do you want? 0
That's all!

循环体被执行零次。

```
cout << "Hello ";
countDown = countDown - 1;
```

因此，每次重复循环体时，都会输出 "Hello "，并且变量 countDown 的值会减少一。在计算机重复循环体三次后，countDown 的值减少到 0，并且 Display 2.12 中的程序和括号中的布尔表达式

## DISPLAY 2.13 while 语句的语法

### 包含多个语句的循环体：

```
1   while ( Boolean_Expression )
2   {
3       Statement_1
4       Statement_2
5       ...
6       Statement_Last
7   }
```

此处不要放置分号。

body

### 包含单个语句的循环体：

```
8   while ( Boolean_Expression )
9       Statement
```

body

不再满足。因此，此 while 语句在重复循环体三次后结束。

while 语句的语法在 Display 2.13 中给出。允许的 Boolean_Expressions 与 if-else 语句中允许的布尔表达式完全相同。就像在 if-else 语句中一样，while 语句中的布尔表达式必须用括号括起来。在 Display 2.13 中，我们给出了两种情况的语法模板：循环体中有多个语句的情况和循环体中只有一个语句的情况。请注意，当循环体中只有一个语句时，你无需包含大括号 { 和 }。

让我们更详细地回顾 while 语句执行的操作。当 while 语句被执行时，首先发生的事情是检查 while 之后跟随的布尔表达式。它为真或为假。例如，比较

```
countDown > 0
```

如果 countDown 的值为正，则为真。如果为假，则不采取任何操作，程序继续执行 while 语句之后的下一条语句。如果比较为真，则执行整个循环体。循环体中至少有一个被比较的表达式通常包含可能被循环体改变的内容，例如 Display 2.12 中 while 语句中的 countDown 的值。在执行完循环体后，会再次检查比较。此过程只要比较继续为真就会一遍又一遍地重复。在每次循环体迭代后，会再次检查比较，如果为真，则整个循环体再次执行。当比较不再为真时，while 语句结束。

## DISPLAY 2.15 一个 do-while 循环

```
#include <iostream>
using namespace std;
int main()
{
    char ans;
    do
    {
        cout << "Hello\n";
        cout << "Do you want another greeting?\n" << "Press y for yes, n for no,\n" << "and then press return: ";
        cin >> ans;
    } while (ans == 'y' || ans == 'Y');
    cout << "Good-Bye\n";
    return 0;
}
```

### Sample Dialogue

```
Hello
Do you want another greeting?
Press y for yes, n for no, and then press return: y
Hello
Do you want another greeting?
Press y for yes, n for no, and then press return: Y
Hello
Do you want another greeting?
Press y for yes, n for no, and then press return: n
Good-Bye
```

一元运算符，++ 和 --。++ 运算符称为增量运算符，-- 运算符称为减量运算符。它们通常与类型为 int 的变量一起使用。如果 n 是类型为 int 的变量，则 n++ 将 n 的值增加一，n-- 将 n 的值减少一。因此 n++ 和 n--（后跟分号）是可执行语句。例如，语句

```
int n = 1, m = 7;
n++;
cout << "The value of n is changed to " << n << endl;
m--;
cout << "The value of m is changed to " << m << endl;
```

产生以下输出：

```
The value of n is changed to 2
The value of m is changed to 6
```

现在你知道了名称 “C++” 中的 “++” 从何而来。

增量和减量语句经常在循环中使用。例如，我们在 Display 2.12 的 while 循环中使用了以下语句：

```
countDown = countDown - 1;
```

然而，大多数经验丰富的 C++ 程序员会使用减量运算符而不是赋值语句，因此整个 while 循环将如下所示：

```
while (countDown > 0)
{
    cout << "Hello ";
    countDown--;
}
```

## PROGRAMMING EXAMPLE 信用卡余额

假设你有一张银行信用卡，欠款余额为 $50，并且假设银行每月向你收取 2% 的利息。你可以在不付款的情况下让多少个月过去，你的欠款余额才会超过 $100？解决这个问题的一种方法是简单地阅读每月的对账单并计算余额达到 $100 或更多之前经过的月份数。更好的是，你可以用程序计算月度余额，而不是等待对账单到达。这样你就可以在不必等待太久的情况下得到答案（并且不会危及你的信用评级）。

一个月后，余额将为 $50 加上 $50 的 2%，即 $51。两个月后，余额将为 $51 加上 $51 的 2%，即 $52.02。三个月后，余额将为 $52.02 加上 $52.02 的 2%，依此类推。一般来说，每个月都会使余额增加 2%。程序可以通过将余额存储在名为 balance 的变量中来跟踪余额。余额在一个月内的变化可以按如下方式计算：

```
balance = balance + 0.02 * balance ;
```

如果我们重复此操作直到 balance 的值达到（或超过）100.00 并且我们计算重复次数，那么我们将知道余额达到 100.00 需要多少个月。为此，我们需要另一个变量来计算余额被更改的次数。让我们将这个新变量称为 count。我们的 while 循环的最终体将因此包含以下语句：


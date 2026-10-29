

## 程序 3.3

```
#include <iostream>
using namespace std;

int main()
{
    int sum;

    sum = 0;
    cout << "The value of sum is initially set to " << sum << endl;
    sum = sum + 96;
    cout << " sum is now " << sum << endl;
    sum = sum + 70;
    cout << " sum is now " << sum << endl;
    sum = sum + 85;
    cout << " sum is now " << sum << endl;
    sum = sum + 60;
    cout << " The final sum is " << sum << endl;

    return 0;
}
```

程序 3.3 显示以下输出：

```
The value of sum is initially set to 0
sum is now 96
sum is now 166
sum is now 251
The final sum is 311
```

尽管程序 3.3 并不是一个实用的程序（因为手工加数更容易），但它确实说明了重复使用具有以下形式的语句的累加效果：

```
variable = variable + newValue;
```

这种类型的语句称为累加语句。当你变得更加熟悉第 5 章中介绍的重复语句时，你会发现累加语句有许多用途。

## 计数

**计数语句**，它是一种与累加语句类似的赋值语句，具有以下形式：

```
variable = variable + fixedNumber;
```

计数语句的示例如下：

```
i = i + 1;
n = n + 1;
count = count + 1;
j = j + 2;
m = m + 2;
kk = kk + 3;
```

在这些示例中，相同的变量同时出现在等号的两侧。执行语句后，变量的值会增加一个固定量。在前三个示例中，变量 i、n 和 count 各自增加了 1。在接下来的两个示例中，变量增加了 2，而在最后一个示例中，变量 kk 增加了 3。

对于仅增加或减少 1 的变量，C++ 提供了两个一元运算符：增量和减量运算符。使用**增量运算符** ++，表达式 `variable = variable + 1` 可以替换为表达式 `variable++` 或表达式 `++variable`。以下是增量运算符的示例：

| Expression | Alternative |
|---|---|
| `i = i + 1` | `i++` or `++i` |
| `n = n + 1` | `n++` or `++n` |
| `count = count + 1` | `count++` or `++count` |

程序 3.4 说明了增量运算符的使用。它显示以下输出：

```
The initial value of count is 0
    count is now 1
    count is now 2
    count is now 3
    count is now 4
```

## 程序 3.4

```
```cpp
#include <iostream>
using namespace std;

int main()
{
    int count;

    count = 0;
    cout << "The initial value of count is " << count << endl;
    count++;
    cout << "    count is now " << count << endl;
    count++;
    cout << "    count is now " << count << endl;
    count++;
    cout << "    count is now " << count << endl;
    count++;
    cout << "    count is now " << count << endl;

    return 0;
}
```
```

当 ++ 运算符出现在变量之前时，它称为**前缀增量运算符**；当它出现在变量之后时，它称为**后缀增量运算符**。前缀增量运算符和后缀增量运算符之间的区别很重要，当被递增的变量在赋值表达式中使用时。例如，`k = ++n`，它使用前缀增量运算符，在一个表达式中做了两件事：`n` 的值增加 1，然后 `n` 的新值被赋给变量 `k`。因此，语句 `k = ++n;` 等价于以下两个语句：

```
```cpp
n = n + 1;    // increment n first
k = n;        // assign n's value to k
```
```

使用后缀增量运算符的赋值表达式 `k = n++` 则反转了此过程。后缀增量运算符在赋值完成后起作用。因此，语句 `k = n++;` 首先将 `n` 的当前值赋给 `k`，然后将 `n` 的值增加 1。此过程等价于以下两个语句：

```
```cpp
k = n;        // assign n's value to k
n = n + 1;    // and then increment n
```
```

C++ 还提供了减量运算符 --，具有前缀和后缀变体。正如你可能预期的那样，表达式 variable-- 和 --variable 都等价于表达式 variable = variable - 1。以下是减量运算符的示例：

| Expression | Alternative |
|---|---|
| i = i - 1 | i-- or --i |
| n = n - 1 | n-- or --n |
| count = count - 1 | count-- or --count |

当 -- 运算符出现在变量之前时，它称为前缀减量运算符。当此运算符出现在变量之后时，它称为后缀减量运算符。例如，表达式 n-- 和 --n 都将 n 的值减少 1，并且等价于更长的表达式 n = n - 1。

与增量运算符一样，前缀和后缀减量运算符在使用在赋值表达式中时产生不同的结果。例如，表达式 k = --n 首先将 n 的值减少 1，然后将 n 的值赋给 k，而表达式 k = n-- 首先将 n 的当前值赋给 k，然后将 n 的值减少 1。

## 练习 3.1

- 1. （练习）编写一个赋值语句来计算半径为 3.5 英寸的圆的周长。确定圆的周长 c 的公式为 c = 2πr，其中 r 为半径，π 等于 3.1416。
- 2. （练习）编写一个赋值语句来计算圆的面积。确定圆的面积 a 的公式为 a = πr²，其中 r 为半径且 π = 3.1416。
- 3. （练习）编写一个赋值语句将华氏温度转换为摄氏温度。此转换的公式为 摄氏 = 5.0 / 9.0 (华氏 - 32)。
- 4. （练习）编写一个赋值语句来计算单程 s 英里旅程的往返距离 d，单位为英尺。
- 5. （练习）编写一个赋值语句来计算完成一次旅程所需的时间，单位为分钟。计算经过时间的公式为 经过时间 = 总距离 / 平均速度。假设距离以英里为单位，平均速度以英里每小时（mph）为单位。
- 6. （练习）编写一个赋值语句来计算等差数列中第 n 项的值 v。计算此值的公式如下：
  
  v = a + (n - 1)d
  
  a 是数列中的第一个数。
  d 是数列中任意两个数之间的差。

## 第 3 章

## 赋值运算符

7. （练习）编写一个赋值语句来确定梁的最大弯矩 *M*，给定此公式：

*M = X W (L − X) / L*

*X* 是放置重量 *W* 的位置距梁端的距离。
*L* 是梁的长度。

8. （调试）确定并纠正以下程序中的错误。

```
a. #include <iostream>
   using namespace std;
   int main()
   {
       width = 15
       area = length * width;
       cout << "The area is " << area
   }
```

```
b. #include <iostream>
   using namespace std;
   int main()
   {
       int length, width, area;
       area = length * width;
       length = 20;
       width = 15;
       cout << "The area is " << area;

       return 0;
   }
```

```
c. #include <iostream>

   int main()
   {
       int length = 20; width = 15, area;
       length * width = area;
       cout << "The area is " , area;

       return 0;
   }
```

9. （调试）由于错误，学生将程序 3.3 中的语句重新排序如下：

```
#include <iostream>
using namespace std;

int main()
{
    int sum;
    sum = 0;
    sum = sum + 96;
    sum = sum + 70;
    sum = sum + 85;
    sum = sum + 60;
    cout << "The value of sum is initially set to "
         << sum << endl;
    cout << "   sum is now " << sum << endl;
    cout << "   sum is now " << sum << endl;
    cout << "   sum is now " << sum << endl;
    cout << "   The final sum is " << sum << endl;
    return 0;
}
```

确定此程序产生的输出。

10. （练习）使用程序 3.1，通过确定具有以下长度和宽度的矩形的面积来完成下表：

| Length (in.) | Width (in.) | Area |
|---|---|---|
| 1.62 | 6.23 | |
| 2.86 | 7.52 | |
| 4.26 | 8.95 | |
| 8.52 | 10.86 | |
| 12.29 | 15.35 | |

11. （程序）椭圆的面积（见图 3.4）由以下公式给出：

Area = π a b

使用此公式，编写一个 C++ 程序来计算具有短轴 a 为 2.5 英寸和长轴 b 为 6.4 英寸的椭圆的面积。

![](img/e9bf940282dfb289356f077151cc69dd_111_0.png)

# 图 3.4 椭圆的短轴 a 和长轴 b

12. （程序）a. 编写一个 C++ 程序来计算存钱罐中的美元金额。银行目前包含 12 个半美元、20 个四分之一美元、32 个十分之一美元、45 个镍币和 27 个便士。

b. 在计算机上运行为练习 12a 编写的程序。


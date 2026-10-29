
将 result 的值设为 4。然而，下面的表达式赋给 result 的值是不可预测的，因为它并不保证表达式按顺序求值：

result = (first = 2, second = first + 1, third = second + 1);

例如，third = second + 1 可能会在 second = first + 1 之前被求值。

## Display 2.6 The Increment Operator in an Expression

```
1 #include <iostream>
2 using namespace std;

3 int main( )
4 {
5     int numberOfItems, count,
6         caloriesForItem, totalCalories;

7     cout << "How many items did you eat today? ";
8     cin >> numberOfItems;
9     totalCalories = 0;
10    count = 1;
11    cout << "Enter the number of calories in each of the\n"
12        << numberOfItems << " items eaten:\n";

13    while (count++ <= numberOfItems)
14    {
15        cin >> caloriesForItem;
16        totalCalories = totalCalories
17                    + caloriesForItem;
18    }

19    cout << "Total calories eaten today = "
20        << totalCalories << endl;
21    return 0;
22 }
```

## Sample Dialogue

```
How many items did you eat today? 7
Enter the number of calories in each of the
7 items eaten:
300 60 1200 600 150 1 120
Total calories eaten today = 2431
```

> 1 C++ 标准确实规定用逗号连接的表达式应从左到右求值。然而，我们的经验是，并非所有编译器都符合这一标准。

## The for Statement

C++ 中第三个也是最后一个循环语句是 **for statement**。for 语句最常用于以等增量遍历某个整型变量。正如我们在第 5 章中将会看到的，for 语句经常用于遍历数组。然而，for 语句是一个完全通用的循环机制，可以做 while 循环能做的任何事情。

例如，下面的 for 语句对 1 到 10 的整数求和：

```
sum = 0;
int n;
for (n = 1; n <= 10; n++)
    sum = sum + n;
```

for 语句以关键字 for 开始，后面跟着三个用括号括起来的部分，告诉计算机如何处理控制变量。for 语句的开头看起来如下：

```
for (Initialization_Action; Boolean_Expression; Update_Action)
```

第一个表达式说明变量、变量组或其他事物如何初始化；第二个给出一个布尔表达式，用于检查循环何时结束；最后一个表达式说明循环体每次迭代后循环控制变量如何更新。

for 语句开头处的三个表达式由两个——也仅有两个——分号分隔。不要受诱惑在第三个表达式后放置分号。技术上的解释是，这三件事是表达式，而不是语句，因此不需要在末尾加分号。

for 语句通常使用单个 int 变量来控制循环迭代和循环结束。然而，for 语句开头处的三个表达式可以是任意 C++ 表达式；因此，它们可能涉及多于（甚至少于）一个变量，且变量可以是任何类型。

使用逗号运算符，你可以将多个操作添加到三个括号内项目中的第一个或最后一个（但通常不是第二个）。例如，你可以将变量 sum 的初始化移入 for 循环内部，得到以下与我们之前展示的 for 语句代码等价的内容：

```
for (sum = 0, n = 1; n <= 10; n++)
    sum = sum + n;
```

尽管我们不建议这样做，因为可读性不佳，但你可以将 for 循环的整个主体移入括号内的第三个项目中。之前的 for 语句等价于以下内容：

```
for (sum = 0, n = 1; n <= 10; sum = sum + n, n++);
```

## Display 2.7 for Statement

## for Statement Syntax

```
for (Initialization_Action; Boolean_Expression; Update_Action)
Body_Statement
```

## EXAMPLE

```
for (number = 100; number >= 0; number--)
    cout << number
        << " bottles of beer on the shelf.\n";
```

## EQUIVALENT while LOOP SYNTAX

```
Initialization_Action;
while (Boolean_Expression)
{
    Body_Statement
    Update_Action;
}
```

## EQUIVALENT EXAMPLE

```
number = 100;
while (number >= 0)
{
    cout << number
        << " bottles of beer on the shelf.\n";
    number--;
}
```

## Sample Dialogue

```
100 bottles of beer on the shelf.
99 bottles of beer on the shelf.
.
.
0 bottles of beer on the shelf.
```

Display 2.7 显示了 for 语句的语法，并通过展示其如何转换为等价的 while 语句来描述 for 语句的动作。请注意，在 for 语句中，如同对应的 while 语句中一样，停止条件是在第一次循环迭代之前进行测试。因此，可能存在一个 for 循环，其主体被执行零次。

## PITFALL: Extra Semicolon in a for Statement

你通常不会在 for 循环开始处的括号后放置分号。来看会发生什么，考虑下面的 for 循环：

```
for (int count = 1; count <= 10; count++);
cout << "Hello\n";
```

如果你没有注意到额外的分号，你可能会期望这个 for 循环十次向屏幕写入 Hello。如果你注意到了分号，你可能会期望编译器发出错误信息。两者都不会发生。如果你将这个 for 循环嵌入到一个完整的程序中，编译器不会抱怨。如果你运行程序，只有一次 Hello 会被输出，而不是十次。发生了什么？要回答这个问题，我们需要一些背景知识。

在 C++ 中创建一个语句的一种方法是给某物后面加上分号。如果你给 x++ 后面加上分号，你就把表达式

```
x++
```

改成了语句

```
x++;
```

如果你在空无一物后面放置分号，你仍然创建了一个语句。因此，分号本身就是一个语句，被称为空语句或 null 语句。空语句不执行任何操作，但它仍然是一个语句。因此，以下是一个完整且合法的 for 循环，其主体是空语句：

```
for (int count = 1; count <= 10; count++);
```

这个 for 循环确实迭代了十次，但由于主体是空语句，主体迭代时什么也不会发生。这个循环什么也不做，而且做了十次！

这种问题也可能出现在 while 循环中。注意不要在 while 循环开始处括住布尔表达式的右括号后放置分号。do-while 循环则恰好相反。你必须始终记住用分号结束 do-while 循环。

## PITFALL: Infinite Loops

只要控制布尔表达式为真，while 循环、do-while 循环或 for 循环就不会终止。这个布尔表达式通常包含一个变量，该变量会被循环体改变，并且通常这个变量的值会以最终使布尔表达式变为假从而终止循环的方式改变。然而，如果你犯了错误，写出程序使得布尔表达式始终为真，那么循环将永远运行。永远运行的循环称为无限循环。

infinite loop

不幸的是，无限循环的例子并不难找到。首先让我们描述一个会终止的循环。下面的 C++ 代码会写出小于 12 的正偶数。也就是说，它会逐行输出数字 2、4、6、8 和 10，然后循环结束。

```
x = 2;
while (x != 12)
{
    cout << x << endl;
    x = x + 2;
}
```

x 的值在每次循环迭代中增加 2，直到达到 12。此时，while 关键字后的布尔表达式不再为真，所以循环结束。

现在假设你想写出小于 12 的奇数，而不是偶数。你可能会错误地认为你只需要把初始化语句改为

```
x = 1;
```

但这个错误会创建一个无限循环。因为 x 的值从 11 变到 13，x 的值永远不会等于 12；因此，循环永远不会终止。

当循环通过使用 == 或 != 检查数值来终止时，这种问题很常见。处理数字时，始终更安全地测试是否越过某个值。例如，以下内容作为我们的 while 循环的第一行会很好地工作：

```
while (x < 12)
```

有了这个改动，x 可以初始化为任意数字，循环仍然会终止。

一个处于无限循环中的程序将永远运行，除非有外部力量停止它。由于你现在可以编写包含无限循环的程序，了解如何强制程序终止是个好主意。强制程序停止的方法因系统而异。Control-C 键可以在许多系统上终止程序。按下 Control-C 的方法是按住 Control 键的同时按下 C 键。

在简单程序中，无限循环几乎总是错误。然而，有些程序是有意编写成原则上永远运行的，例如航空公司预订程序中的主外层循环，它只是不断询问更多预订，直到你关闭计算机（或以非典型方式终止程序）。

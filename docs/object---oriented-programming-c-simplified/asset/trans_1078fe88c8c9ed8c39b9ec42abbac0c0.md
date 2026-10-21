

```
for(initialization; condition; increment/decrement)
{
    Statements;
}
```

## for 循环的嵌套

for 循环的嵌套在许多编程场景中使用得最为频繁，也是显示各种图案时最重要的用途之一，我们将在接下来的程序中看到这些图案。

for 循环嵌套的语法如下：

```
for(initialization; condition; increment/decrement)
{
    for(initialization; condition; increment/decrement)
    {
        Statements;
    }
    Statements;
}
```

对于第一个 for 循环（外层 for 循环）的每次迭代，内层 for 循环都会执行，因为它是外层 for 循环循环体的一部分。内层 for 循环拥有自己的一组语句，这些语句会一直执行，直到内层 for 循环的条件为真。请看下面给出的几个程序：

```
/* PROG 3.51 TO PRINT THE FOLLOWING PATTERN, INPUT IS NUMBER OF LINES

1
2 2
3 3 3
4 4 4 4
5 5 5 5 5
*/

#include <iostream.h>
void main()
{
    int line, row, col;
    cout << "Enter the number of lines" << endl;
    cin >> line;
    cout << "The pattern is" << endl;
    for(row = 1; row <= line; row++)
    {
        for(col = 1; col <= row; col++)
            cout << " " << row;
        cout << "\n";
    }
}
```

**输出：**

```
Enter the number of lines
4
The pattern is
1
2 2
3 3 3
4 4 4 4
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_125_0.png)

图 3.52. 程序输出界面。

我们在程序中使用了两个 for 循环。一个用于控制行数，另一个用于控制列数。初始时假设 line = 4，那么外层 for 循环会执行四次。第一次执行时 row = 1，内层循环只执行一次。打印换行的语句位于第二个 for 循环之后，因此在打印 1 之后会输出一个换行。当控制流第二次进入外层 for 循环时，row 的值为 2；内层循环通过将 col 的值设为 1 重新开始；这一次内层循环执行两次，即打印 row 的值（当前为 2）两次。此过程一直持续到 row <= 4 为止。

```
/* PROG 3.52 TO PRINT THE FOLLOWING PATTERN, INPUT IS NUMBER OF LINES

1
0 1
1 0 1
0 1 0 1
1 0 1 0 1
*/

#include <iostream.h>
void main()
{
    int line, row, col;
    cout << "Enter the number of lines" << endl;
    cin >> line;
    cout << "The pattern is" << endl;
    for(row = 1; row <= line; row++)
    {
        for(col = 1; col <= row; col++)
        {
            if(row % 2 == 0)
                cout << !(col % 2);
            else
                cout << (col % 2);
        }
        cout << "\n";
    }
}
```

**输出：**

```
Enter the number of lines
4
The pattern is
1
01
101
0101
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_126_0.png)

图 3.53. 程序输出界面。

**解释：**

仔细观察该图案。偶数行是一种图案，奇数行是另一种图案。在偶数行，即 row = 2, 4, 6, ...... 时，如果打印 col % 2 的补值，就能得到所需的图案。在 row = 1, 3, 5, ...... 时，直接打印 col % 2 即可。

## 3.7.3 do-while 循环

最后一种循环是 do-while 循环。其语法如下：

```
do
{
    Statements;
    Statements;
    Statements;
    ...........;
    ...........;
} while (condition);
```

它与 while 循环类似，区别在于条件是在末尾检查，而不是在开头检查。

```
/* PROG 3.53 DEMO OF DO-WHILE LOOP*/

#include <iostream.h>
void main()
{
    int t = 1;
    do
    {
        cout << t << endl;
        t++;
    } while(t <= 15);
}
```

**输出：**

```
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_128_0.png)

图 3.54. 程序输出界面。

**解释：** do-while 循环与 while 循环类似，区别在于条件是在末尾检查的。循环以 `do` 开头，后跟循环体，在循环体末尾使用 `while` 来书写条件。`while` 是 do-while 循环的一部分，并且必须以分号结尾。初始时 t 的值为 1，程序打印该值；然后 t 变为 2。在循环体末尾条件为真，因此控制流返回到 do 循环体，过程继续。

### 关于 do-while 循环的一些要点

-   它也被称为底部测试循环或出口控制循环，因为条件位于循环的底部。
-   无论循环体末尾给定的条件如何，该循环至少会执行一次。
-   do-while 循环主要用于编写菜单驱动程序。

```
/* PROG 3.54 TO FIND NUMBER OF DIGITS IN A GIVEN NUMBER TILL SINGLE DIGIT*/

#include <iostream.h>
void main()
{
    int num, r;
    int sum = 0, save;
    num = 0;
    cout << "Enter the number\n";
    cin >> num;
    do
    {
        sum = 0;
        while(num != 0)
        {
            r = num % 10;
            sum = sum + r;
            num = num / 10;
        }
        if(sum > 9)
            num = sum;
    } while(num > 9);
    cout << "Sum of digits up to single digit"
         << " is := " << sum << endl;
}
```

**输出：**

```
Enter the number

4275

Sum of digits up to single digit is := 9
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_129_0.png)

图 3.55. 程序输出界面。

**解释：** 例如，如果数字是 4275，那么各位数字之和为 4 + 2 + 7 + 5 = 18。由于 18 大于 9，我们重复该过程，得到结果 1 + 8 = 9。这一次结果是一个个位数，因此我们停止该过程。在求各位数字之和的程序中，我们使用了 while 循环；但在求逐位相加直到个位数的数字和时，我们使用了 do-while 循环。当 sum > 9 时，将 sum 赋给 num，然后使用 do-while 循环求出该 num 的各位数字之和。

## 3.8 思考要点

-   赋值运算符 (=)，其两侧各有一个操作数。右侧操作数的值被赋给左侧的操作数。
-   算术赋值运算符 +=、-=、*=、/= 和 %=，它们是由算术运算符与赋值运算符组合而成的。
-   一元负号运算符 (−)，它返回数值的相反数。
-   自增运算符 ++ 的两种版本。你知道，在 ++x 中，++ 运算符称为前置自增运算符；而在 x++ 中，++ 称为后置自增运算符。
-   自减运算符 -- 的两种版本。你已经学过，例如在 --x 中，-- 运算符是前置自减运算符；而在 x-- 中，-- 称为后置自减运算符。
-   C 中的六个关系运算符：==（等于）、!=（不等于）、>（大于）、<（小于）、>=（大于或等于）和 <=（小于或等于）。
-   如何通过在数据前加上强制类型转换运算符来改变数据的类型。
-   sizeof 运算符返回指定数据类型所占的字节数。你可以使用该运算符来测量数据类型在机器上的大小。
-   逻辑与运算符 (&&) 仅在其两个操作数（即表达式）都为 TRUE 时返回 1，否则返回 0。
-   逻辑或运算符 (||) 仅在其两个操作数都为 FALSE 时返回 0，否则返回 1。
-   逻辑非运算符 (!) 将操作数的逻辑值取反。
-   共有六种位操作运算符：按位与运算符 (&)、按位或运算符 (|)、按位异或运算符 (^)、按位取反运算符 (~)、右移运算符 (>>) 和左移运算符 (<<)。
-   条件运算符 (?:) 是 C++ 中唯一可以接受三个操作数的运算符。
-   程序的一项重要任务是让计算机根据指定的分支条件跳转到代码的不同部分。
-   if 语句是 C++ 中用于条件分支的非常重要的语句。
-   if 语句可以嵌套使用，以便在程序中做出一系列决策。
-   if-else 语句是 if 语句的扩展。
-   当代码中需要做出的决策不止几个时，switch 语句可以帮助你保持程序的可读性。
-   case 和 default 关键字后跟冒号 (:) 和一个整数值，在 switch 语句中用作标签。
-   break 语句可用于退出 switch 结构或循环（通常是无限循环）。
-   continue 语句用于让你在跳过某些语句的同时保持在循环内。
-   goto 语句使计算机能够跳转到程序中的其他位置。不建议使用该语句，因为它可能导致程序不可靠且难以调试。
-   循环可用于反复执行同一组语句，直到满足指定条件。
-   循环使程序更加简洁。
-   C++ 中有三种用于循环的语句：for、while 和 do-while。
-   for 语句中有三个表达式字段。第二个字段包含用作指定条件的表达式。
-   for 语句不以分号结尾。
-   空的 for(; ;) 语句可用于构成无限循环。


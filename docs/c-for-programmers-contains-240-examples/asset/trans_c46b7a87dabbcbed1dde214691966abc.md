

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_177_0.png)

图 5.4 | 图 5.2 中 for 语句的 UML 活动图。

+   a) 将控制变量从 1 变到 100，每次递增 1。
+   
+       for ( int i = 1; i <= 100; i++ )

+   b) 将控制变量从 100 变到 1，每次递增 -1（即每次递减 1）。
+   
+       for ( int i = 100; i >= 1; i-- )

+   c) 将控制变量从 7 变到 77，步长为 7。
+   
+       for ( int i = 7; i <= 77; i += 7 )

+   d) 将控制变量从 20 变到 2，步长为 -2。
+   
+       for ( int i = 20; i >= 2; i -= 2 )

+   e) 将控制变量按以下值序列变化：2, 5, 8, 11, 14, 17, 20。
+   
+       for ( int i = 2; i <= 20; i += 3 )

+   f) 将控制变量按以下值序列变化：99, 88, 77, 66, 55, 44, 33, 22, 11, 0。
+   
+       for ( int i = 99; i >= 0; i -= 11 )

## 常见编程错误 5.6

> 在向下计数的循环的循环继续条件中使用不正确的关系运算符（例如在向下计数到 1 的循环中错误地使用 `i <= 1` 而不是 `i >= 1`）通常是逻辑错误，会导致程序运行时产生不正确的结果。

## 应用：对从 2 到 20 的偶数求和

接下来的两个示例提供了 for 语句的简单应用。图 5.5 中的程序使用 for 语句将从 2 到 20 的偶数相加。循环的每次迭代（第 12–13 行）将控制变量 number 的当前值加到变量 total 上。

请注意，图 5.5 中 for 语句的循环体实际上可以通过逗号运算符合并到 for 头的增量部分中，如下所示：

```
for ( int number = 2; // initialization
      number <= 20; // loop continuation condition
      total += number, number += 2 ) // total and increment
; // empty body
```

## 良好编程实践 5.2

> 虽然 for 之前的语句和 for 循环体中的语句通常可以合并到 for 头中，但这样做可能会使程序更难阅读、维护、修改和调试。

## 良好编程实践 5.3

> 尽可能将控制语句头限制为一行。

```
1  // Fig. 5.5: fig05_05.cpp
2  // Summing integers with the for statement.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  int main()
8  {
9      int total = 0; // initialize total
10
11     // total even integers from 2 through 20
12     for ( int number = 2; number <= 20; number += 2 )
13         total += number;
14
15     cout << "Sum is " << total << endl; // display results
16     return 0; // successful termination
17  } // end main
```

```
Sum is 110
```

图 5.5 | 使用 for 语句对整数求和。

## 应用：复利计算

下一个示例使用 for 语句计算复利。请考虑以下问题陈述：

某人将 1000.00 美元存入一个年利率为 5% 的储蓄账户。假设所有利息都留在账户中，计算并打印 10 年中每年年底账户中的金额。使用以下公式确定这些金额：

\[a = p(1+r)^n\]

其中

- \(p\) 是原始投资金额（即本金），
- \(r\) 是年利率，
- \(n\) 是年数，
- \(a\) 是第 n 年年底的存款金额。

这个问题涉及一个循环，该循环在资金存续的 10 年中每年执行一次指定的计算。解决方案如图 5.6 所示。

```
// Fig. 5.6: fig05_06.cpp
// Compound interest calculations with for.
#include <iostream>
using std::cout;
using std::endl;
using std::fixed;

#include <iomanip>
using std::setw; // enables program to set a field width
using std::setprecision;

#include <cmath> // standard C++ math library
using std::pow; // enables program to use function pow

int main()
{
   double amount;   // amount on deposit at end of each year
   double principal = 1000.0; // initial amount before interest
   double rate = .05; // interest rate

   // display headers
   cout << "Year" << setw( 21 ) << "Amount on deposit" << endl;

   // set floating-point number format
   cout << fixed << setprecision( 2 );

   // calculate amount on deposit for each of ten years
   for ( int year = 1; year <= 10; year++ )
   {
      // calculate new amount for specified year
      amount = principal * pow( 1.0 + rate, year );

      // display the year and the amount
      cout << setw( 4 ) << year << setw( 21 ) << amount << endl;
   } // end for

   return 0; // indicate successful termination
} // end main
```

**图 5.6** | 使用 for 进行复利计算。（第 1 部分，共 2 部分。）

| 年份 | 存款金额 |
|------|-------------------|
| 1 | 1050.00 |
| 2 | 1102.50 |
| 3 | 1157.63 |
| 4 | 1215.51 |
| 5 | 1276.28 |
| 6 | 1340.10 |
| 7 | 1407.10 |
| 8 | 1477.46 |
| 9 | 1551.33 |
| 10 | 1628.89 |

图 5.6 | 使用 for 进行复利计算。（第 2 部分，共 2 部分。）

for 语句（第 28–35 行）执行其循环体 10 次，将控制变量从 1 变到 10，每次递增 1。C++ 没有指数运算符，因此我们使用标准库函数 pow（第 31 行）来实现此目的。函数 pow( x, y ) 计算 x 的 y 次幂的值。在此示例中，代数表达式 ( 1 + r )n 被写为 pow( 1.0 + rate, year )，其中变量 rate 表示 r，变量 year 表示 n。函数 pow 接受两个 double 类型的参数，并返回一个 double 值。

如果不包含头文件 <cmath>（第 12 行），此程序将无法编译。函数 pow 需要两个 double 参数。请注意，year 是一个整数。头文件 <cmath> 包含的信息告诉编译器在调用函数之前将 year 的值转换为临时的 double 表示形式。此信息包含在 pow 的函数原型中。第 6 章总结了其他数学库函数。

## 常见编程错误 5.7

> 一般来说，使用标准库函数时忘记包含相应的头文件（例如，在使用了数学库函数的程序中忘记包含 <cmath>）是一个编译错误。

## 关于使用 float 或 double 类型表示货币金额的告诫

请注意，第 17–19 行声明了 double 变量 amount、principal 和 rate。我们这样做是为了简单起见，因为我们处理的是美元的小数部分，并且需要一种允许其值包含小数点的类型。不幸的是，这可能会带来麻烦。下面简要解释使用 float 或 double 表示美元金额时可能出现的问题（假设使用 setprecision(2) 在打印时指定两位精度）：机器中存储的两个美元金额可能是 14.234（打印为 14.23）和 18.673（打印为 18.67）。当这些金额相加时，内部和为 32.907，打印为 32.91。因此，你的打印输出可能如下所示：

```
14.23
+ 18.67
------
32.91
```

但是，人们将打印出的各个数字相加时会期望得到 32.90！你已经受到警告了！

## 良好编程实践 5.4

> 不要使用 float 或 double 类型的变量进行货币计算。浮点数的不精确性会导致错误，从而产生不正确的货币值。[注意：一些第三方供应商销售可执行精确货币计算的 C++ 类库。]

## 使用流操纵符格式化数值输出

for 循环之前的第 25 行输出语句和 for 循环中的第 34 行输出语句联合起来，按照参数化流操纵符 setprecision 和 setw 以及非参数化流操纵符 fixed 指定的格式打印变量 year 和 amount 的值。流操纵符 setw( 4 ) 指定下一个输出值应出现在宽度为 4 的字段中——即 cout 打印该值时至少占 4 个字符位置。如果要输出的值宽度小于 4 个字符位置，则默认情况下该值在字段中右对齐。如果要输出的值宽度大于 4 个字符位置，字段宽度会扩展以容纳整个值。若要指示值应左对齐输出，只需输出非参数化流操纵符 left（位于头文件 <iostream> 中）。输出非参数化流操纵符 right 可恢复右对齐。

输出语句中的其他格式设置表示变量 amount 以带小数点的定点值形式打印（在第 25 行使用流操纵符 fixed 指定），在 21 个字符位置的字段中右对齐（在第 34 行使用 setw( 21 ) 指定），小数点右侧有两位精度（在第 25 行使用操纵符 setprecision( 2 ) 指定）。我们在 for 循环之前将流操纵符 fixed 和 setprecision 应用于输出流（即 cout），因为这些格式设置在被更改之前一直有效——此类设置称为粘性设置（sticky settings），无需在每次循环迭代时都应用。但是，使用 setw 指定的字段宽度仅适用于下一个输出值。我们将在第 15 章“流输入/输出”中讨论 C++ 强大的输入/输出格式化功能。

请注意，作为 pow 函数参数出现的计算 1.0 + rate 位于 for 语句的循环体内。实际上，这个计算在每次循环迭代中都会产生相同的结果，因此重复执行它是浪费的——它应该在循环之前执行一次。

## 性能提示 5.1

> 避免将值不变的表达式放在循环内——不过，即使你放了，当今许多复杂的优化编译器也会在生成的机器语言代码中自动将这些表达式移到循环外。

## 性能提示 5.2

> 许多编译器包含可提高你编写的代码性能的优化功能，但最好还是一开始就编写良好的代码。

## 5.5 do...while 重复语句

do...while 重复语句与 while 语句类似。在 while 语句中，循环继续条件的测试发生在循环体执行之前的循环开头。do...while 语句在循环体执行之后测试循环继续条件；因此，循环体至少执行一次。当 do...while 终止时，执行将继续执行 while 后面的语句。


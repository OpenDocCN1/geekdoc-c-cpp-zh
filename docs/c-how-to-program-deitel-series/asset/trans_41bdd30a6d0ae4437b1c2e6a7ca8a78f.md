
```cpp
using namespace std;

unsigned long fibonacci( unsigned long ); // function prototype

int main()
{
   // calculate the fibonacci values of 0 through 10
   for ( unsigned int counter = 0; counter <= 10; ++counter )
      cout << "fibonacci( " << counter << " ) = "
         << fibonacci( counter ) << endl;

   // display higher fibonacci values
   cout << "\nfibonacci( 20 ) = " << fibonacci( 20 ) << endl;
   cout << "fibonacci( 30 ) = " << fibonacci( 30 ) << endl;
   cout << "fibonacci( 35 ) = " << fibonacci( 35 ) << endl;
} // end main

// recursive function fibonacci
unsigned long fibonacci( unsigned long number )
{
   if ( ( 0 == number ) || ( 1 == number ) ) // base cases
      return number;
   else // recursive step
      return fibonacci( number - 1 ) + fibonacci( number - 2 );
} // end function fibonacci
```

```text
fibonacci( 0 ) = 0
fibonacci( 1 ) = 1
fibonacci( 2 ) = 1
fibonacci( 3 ) = 2
fibonacci( 4 ) = 3
fibonacci( 5 ) = 5
fibonacci( 6 ) = 8
fibonacci( 7 ) = 13
fibonacci( 8 ) = 21
fibonacci( 9 ) = 34
fibonacci( 10 ) = 55

fibonacci( 20 ) = 6765
fibonacci( 30 ) = 832040
fibonacci( 35 ) = 9227465
```

**图 6.29** | 递归函数 fibonacci。（第 2 部分，共 2 部分）

### *评估 fibonacci(3)*

图 6.30 展示了函数 fibonacci 将如何计算 fibonacci(3)。此图提出了关于 C++ 编译器对运算符操作数的计算顺序的一些有趣问题。这与运算符应用于其操作数的顺序（即由运算符优先级和结合性规则所决定的顺序）是一个不同的问题。图 6.30 显示，计算 fibonacci(3) 会导致两次递归调用，即 fibonacci(2) 和 fibonacci(1)。这些调用按什么顺序进行？

![](img/b42ba5cd262b1358d16610173f975e4d_289_0.png)

**图 6.30** 函数 `fibonacci` 的递归调用集合。

### *操作数的计算顺序*

大多数程序员只是简单地认为操作数是从左到右计算的。C++ 并没有指定大多数运算符（包括 `+`）的操作数的计算顺序。因此，你不能对这些调用的执行顺序做任何假设。这些调用实际上可以先执行 `fibonacci(2)`，然后执行 `fibonacci(1)`，也可以按相反顺序执行：先执行 `fibonacci(1)`，再执行 `fibonacci(2)`。在这个程序以及大多数其他程序中，最终结果是一样的。然而，在某些程序中，操作数的计算可能会产生*副作用*（数据值的变化），这可能影响表达式的最终结果。

C++ 只规定了四个运算符的操作数计算顺序——`&&`、`||`、逗号 `(,)` 和 `?:`。前三个是二元运算符，它们的两个操作数保证按从左到右的顺序计算。最后一个运算符是 C++ 唯一的三元运算符——它最左边的操作数总是首先求值；如果结果为 `true`，则接下来求值中间的操作数，并忽略最后一个操作数；如果最左边的操作数结果为 `false`，则接下来求值第三个操作数，并忽略中间的操作数。

**可移植性提示 6.2**

依赖于 `&&`、`||`、`?:` 和逗号 `(,)` 运算符之外的操作数计算顺序的程序，在不同编译器下可能表现不同，并可能导致逻辑错误。

**常见编程错误 6.13**

编写依赖于 `&&`、`||`、`?:` 和逗号 `(,)` 运算符之外的操作数计算顺序的程序，可能导致逻辑错误。

**错误预防提示 6.9**

不要依赖操作数的求值顺序。为了确保副作用按正确顺序生效，应将复杂表达式拆分成单独的语句。

![](img/b42ba5cd262b1358d16610173f975e4d_290_0.png)

**常见编程错误 6.14**

请记住，`&&` 和 `||` 运算符使用短路求值。如果将带有副作用的表达式放在 `&&` 或 `||` 运算符的右侧，而该表达式本应总是被求值，则会造成逻辑错误。

### 指数复杂度

关于像我们这里用来生成斐波那契数的递归程序，有必要提出一个警告。函数 `fibonacci` 中的每一层递归都会对函数调用的数量产生*加倍*的影响；也就是说，计算第 *n* 个斐波那契数所需的递归调用数量级为 2ⁿ。这会迅速失控。仅计算第 20 个斐波那契数就需要的调用数量级为 2²⁰，即大约一百万次调用；计算第 30 个斐波那契数需要的调用数量级为 2³⁰，即大约十亿次调用，以此类推。计算机科学家将这种现象称为**指数复杂度**。这类问题即使是世界上最强大的计算机也会感到无能为力！一般的复杂度问题，尤其是指数复杂度，会在通常称为“算法”的高年级计算机科学课程中详细讨论。

![](img/b42ba5cd262b1358d16610173f975e4d_290_1.png)

**性能提示 6.8**

避免使用会导致调用次数呈指数“爆炸”的斐波那契式递归程序。

## 6.22 递归与迭代

在前两节中，我们研究了两个也可以用简单的迭代程序实现的递归函数。本节比较这两种方法，并讨论在特定情况下为什么你可能选择其中一种而不是另一种。

-   迭代和递归都*基于控制语句*：迭代使用*重复结构*；递归使用*选择结构*。
-   迭代和递归都涉及*重复*：迭代显式使用*重复结构*；递归通过*重复的函数调用*实现重复。
-   迭代和递归都涉及*终止测试*：迭代在*循环继续条件不满足*时终止；递归在识别到*基本情况*时终止。
-   计数器控制重复的迭代和递归都逐渐接近终止：迭代*修改计数器*，直到计数器达到使循环继续条件不满足的值；递归产生*原问题的更简单版本*，直到达到基本情况。
-   迭代和递归*都可能无限进行*：如果循环继续测试永远不会变为 false，则迭代发生无限循环；如果递归步骤在每次递归调用中不能以一种收敛于基本情况的方式减小问题，则发生*无限递归*。

### 迭代阶乘实现

为了说明迭代和递归之间的区别，让我们考察阶乘问题的一个迭代解决方案（图 6.31）。其中使用了重复语句（图 6.31 第 23...24 行），而不是递归解决方案中的选择语句（图 6.28 第 20–23 行）。两种解决方案都使用终止测试。在递归解决方案中，第 20 行（图 6.28）测试基本情况。在迭代解决方案中，第 23 行（图 6.31）测试循环继续条件——如果测试失败，循环终止。最后，迭代解决方案不是产生原问题的更简单版本，而是使用一个计数器，并修改它直到循环继续条件变为 false。

```cpp
// Fig. 6.31: fig06_31.cpp
// Iterative version of factorial.
#include <iostream>
#include <iomanip>
using namespace std;

unsigned long factorial( unsigned int ); // function prototype

int main()
{
   // calculate the factorials of 0 through 10
   for ( unsigned int counter = 0; counter <= 10; ++counter )
      cout << setw( 2 ) << counter << "! = " << factorial( counter )
           << endl;
} // end main

// iterative function factorial
unsigned long factorial( unsigned int number )
{
   unsigned long result = 1;

   // iterative factorial calculation
   for ( unsigned int i = number; i >= 1; --i )
      result *= i;

   return result;
} // end function factorial
```

```text
0! = 1
1! = 1
2! = 2
3! = 6
4! = 24
5! = 120
6! = 720
7! = 5040
8! = 40320
9! = 362880
10! = 3628800
```

**图 6.31** | *迭代函数 factorial。*

### 递归的缺点

递归有缺点。它会重复调用函数机制，因此产生*函数调用的开销*。这在处理器时间和内存空间方面都可能代价高昂。每次递归调用都会创建*函数变量的另一个副本*；这会消耗大量的内存。

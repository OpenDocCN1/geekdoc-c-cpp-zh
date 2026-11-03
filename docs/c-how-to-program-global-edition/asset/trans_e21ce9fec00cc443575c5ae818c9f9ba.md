
// Fig. 5.18: fig05_18.c
// Recursive factorial function.
#include <stdio.h>

unsigned long long int factorial(unsigned int number);

int main(void)
{
    // during each iteration, calculate
    // factorial(i) and display result
    for (unsigned int i = 0; i <= 21; ++i) {
        printf("%u! = %llu\n", i, factorial(i));
    }
}

// recursive definition of function factorial
unsigned long long int factorial(unsigned int number)
{
    // base case
    if (number <= 1) {
        return 1;
    }
    else { // recursive step
        return (number * factorial(number - 1));
    }
}

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
11! = 39916800
12! = 479001600
13! = 6227020800
14! = 87178291200
15! = 1307674368000
16! = 20922789888000
17! = 355687428096000
18! = 6402373705728000
19! = 121645100408832000
20! = 2432902008176640000
21! = 14197454024290336768

递归阶乘函数首先测试终止条件是否成立，即 number 是否小于或等于 1。如果 number 确实小于或等于 1，factorial 返回 1，不再需要进一步递归，程序终止。如果 number 大于 1，则语句

```
return number * factorial(number - 1);
```

表达了将问题表示为 number 与对 factorial 的递归调用的乘积，该递归调用计算 number - 1 的阶乘。调用 factorial(number - 1) 比原始计算 factorial(number) 稍微简单一些。

函数 factorial（第 17-26 行）接收一个 unsigned int 并返回类型为 unsigned long long int 的结果。C 标准规定类型为 unsigned long long int 的变量可以保存至少为 18,446,744,073,709,551,615 的值。如 Fig. 5.18 所示，阶乘值增长很快。我们选择数据类型 unsigned long long int，以便程序可以计算更大的阶乘值。转换说明符 %llu 用于打印 unsigned long long int 值。不幸的是，阶乘函数产生的数值增长如此之快，以至于即使使用 unsigned long long int，在 unsigned long long int 变量的最大值被超过之前，我们也无法打印很多阶乘值。

即使使用 unsigned long long int，我们仍然无法计算超过 21! 的阶乘。这指出了 C（以及大多数其他过程式编程语言）的一个弱点——即该语言不易扩展以处理各种应用的独特需求。正如我们在书中后面会看到的，C++ 是一种可扩展的语言，通过“类”，我们可以创建新的数据类型，包括如果我们愿意可以容纳任意大整数的类型。

## 常见编程错误 5.9

在需要时忘记从递归函数返回一个值。

## 常见编程错误 5.10

省略基本情况，或错误地编写递归步骤使其无法收敛到基本情况，将导致无限递归，最终耗尽内存。这类似于迭代（非递归）解决方案中无限循环的问题。

## 5.15 使用递归的示例：斐波那契数列

斐波那契数列
0, 1, 1, 2, 3, 5, 8, 13, 21, ...

以 0 和 1 开头，并且具有每个后续斐波那契数都是前两个斐波那契数之和的性质。

斐波那契数列可以递归定义如下：

fibonacci(0) = 0
fibonacci(1) = 1
fibonacci(n) = fibonacci(n - 1) + fibonacci(n - 2)

图 5.19 使用函数 fibonacci 递归计算第 n 个斐波那契数。请注意，斐波那契数往往增长很快。因此，我们在函数 fibonacci 中为参数类型选择了数据类型 unsigned int，为返回类型选择了数据类型 unsigned long long int。在图 5.19 中，每一对输出行显示程序的一次单独运行。

```
1 // Fig. 5.19: fig05_19.c
2 // Recursive fibonacci function
3 #include <stdio.h>
4 
5 unsigned long long int fibonacci(unsigned int n); // function prototype
6 
7 int main(void)
8 {
9     unsigned int number; // number input by user
10 
11     // obtain integer from user
12     printf("%s", "Enter an integer: ");
13     scanf("%u", &number);
14 
15     // calculate fibonacci value for number input by user
16     unsigned long long int result = fibonacci(number);
17 
18     // display result
19     printf("Fibonacci(%u) = %llu\n", number, result);
20 }
21 
22 // Recursive definition of function fibonacci
23 unsigned long long int fibonacci(unsigned int n)
24 {
25     // base case
26     if (0 == n || 1 == n) {
27         return n;
28     }
29     else { // recursive step
30         return fibonacci(n - 1) + fibonacci(n - 2);
31     }
32 }
```

Enter an integer: 0
Fibonacci(0) = 0

Enter an integer: 1
Fibonacci(1) = 1

## 图 5.19 | 递归斐波那契函数。（第 1 部分，共 2 部分。）

Enter an integer: 2
Fibonacci(2) = 1

Enter an integer: 3
Fibonacci(3) = 2

Enter an integer: 10
Fibonacci(10) = 55

Enter an integer: 20
Fibonacci(20) = 6765

Enter an integer: 30
Fibonacci(30) = 832040

Enter an integer: 40
Fibonacci(40) = 102334155

## 图 5.19 | 递归斐波那契函数。（第 2 部分，共 2 部分。）

从 main 对 fibonacci 的调用不是递归调用（第 16 行），但所有后续对 fibonacci 的调用都是递归的（第 30 行）。每次调用 fibonacci 时，它立即测试基本情况——n 等于 0 或 1。如果为真，则返回 n。有趣的是，如果 n 大于 1，递归步骤会生成两个递归调用，每个调用都是比原始调用 fibonacci 稍微简单的问题。图 5.20 显示了函数 fibonacci 如何计算 fibonacci(3)。

![](img/bf54db922e6fa8319cba11069e785521_218_0.png)

## 图 5.20 | fibonacci(3) 的递归调用集合。

## 操作数的求值顺序

该图提出了关于 C 编译器将如何求值运算符操作数的顺序的一些有趣问题。这与运算符对其操作数的应用顺序不同，后者由运算符优先级和结合性规则决定。图 5.20 显示，在计算 fibonacci(3) 时，将进行两次递归调用，即 fibonacci(2) 和 fibonacci(1)。但这些调用的顺序是什么？你可能会简单地假设操作数将从左到右求值。出于优化原因，C 未指定大多数运算符（包括 +）的操作数求值顺序。因此，你不应假设这些调用的执行顺序。调用可能先执行 fibonacci(2) 然后执行 fibonacci(1)，或者调用可能按相反顺序执行，先执行 fibonacci(1) 再执行 fibonacci(2)。在此和其他大多数程序中，最终结果将相同。但在某些程序中，操作数的求值可能会产生副作用，从而影响表达式的最终结果。

C 仅指定了四个运算符的操作数求值顺序——&&、||、逗号（,）运算符和 ?:。其中前三个是二进制运算符，其操作数保证从左到右求值。[注意：用于分隔函数调用中参数的逗号不是逗号运算符。]最后一个运算符是 C 的唯一三元运算符。其最左操作数始终首先求值；如果最左操作数求值为非零（真），则下一个求值中间操作数，最后一个操作数被忽略；如果最左操作数求值为零（假），则下一个求值第三个操作数，中间操作数被忽略。

## 常见编程错误 5.11

编写依赖于除 &&、||、?: 和逗号（,）运算符之外的运算符操作数求值顺序的程序可能会导致错误，因为编译器不一定按你期望的顺序求值操作数。

## 可移植性提示 5.2

依赖于除 &&、||、?: 和逗号（,）运算符之外的运算符操作数求值顺序的程序在不同编译器上可能功能不同。

## 指数复杂度

关于我们在此用于生成斐波那契数的递归程序，需要谨慎。fibonacci 函数中的每个递归层级对调用次数都有加倍效应——计算第 n 个斐波那契数将执行的递归调用次数的数量级为 2^n。这很快就会失控。仅计算第 20 个斐波那契数就需要数量级为 2^20 或约一百万次调用，计算第 30 个斐波那契数就需要数量级为 2^30 或约十亿次调用，等等。计算机科学家将此称为指数复杂度。此类问题甚至让世界上最强大的计算机也感到谦卑！一般复杂性问题，特别是指数复杂性，在通常称为“算法”的高级计算机科学课程中进行了详细讨论。

本节中我们展示的示例使用了直观上吸引人的方法来计算斐波那契数，但有更好的方法。练习 5.48 要求你更深入地研究递归，并提出实现递归斐波那契算法的替代方法。

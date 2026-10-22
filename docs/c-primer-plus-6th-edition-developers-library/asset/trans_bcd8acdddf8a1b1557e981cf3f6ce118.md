

例如，我们可以这样做：

```
double power(double n, int p)  // returns a double
{
    double pow = 1;
    int i;

    for (i = 1; i <= p; i++)
        pow *= n;

    return pow;            // return the value of pow
}
```

要声明函数类型，只需在函数名前面加上类型，就像声明变量时所做的那样。关键字 return 使函数向调用函数返回以下值。这里函数返回一个变量的值，但它也可以返回表达式的值。例如，下面是一个有效的语句：

```
return 2 * x + b;
```

该函数将计算表达式的值并返回它。在调用函数中，返回值可以赋给另一个变量，可以用作表达式中的值，可以用作另一个函数的参数——例如 printf(" %f", power(6.28, 3))——也可以被忽略。

现在让我们在程序中使用该函数。为了测试函数，能够向函数提供多个值以查看其反应会很方便。这提示我们设置一个输入循环。自然的选择是 while 循环。你可以使用 scanf() 一次读取两个值。如果成功读取两个值，scanf() 返回值 2，因此你可以通过将 scanf() 的返回值与 2 进行比较来控制循环。还有一点：要在程序中使用 power() 函数，你需要声明它，就像声明程序使用的变量一样。清单 6.20 显示了该程序。

## Listing 6.20 The power.c Program

```
// power.c -- raises numbers to integer powers
#include <stdio.h>
double power(double n, int p); // ANSI prototype
int main(void)
{
    double x, xpow;
    int exp;

    printf("Enter a number and the positive integer power");
    printf(" to which\nthe number will be raised. Enter q");
    printf(" to quit.\n");
    while (scanf("%lf%d", &x, &exp) == 2)
    {
```
```
xpow = power(x,exp);  // function call
printf("%.3g to the power %d is %.5g\n", x, exp, xpow);
printf("Enter next pair of numbers or q to quit.\n");
}
printf("Hope you enjoyed this power trip -- bye!\n");

return 0;
}

double power(double n, int p)  // function definition
{
    double pow = 1;
    int i;

    for (i = 1; i <= p; i++)
        pow *= n;

    return pow;            // return the value of pow
}
```

以下是示例运行：

```
Enter a number and the positive integer power to which
the number will be raised. Enter q to quit.
1.2 12
1.2 to the power 12 is 8.9161
Enter next pair of numbers or q to quit.
2
16
2 to the power 16 is 65536
Enter next pair of numbers or q to quit.
q
Hope you enjoyed this power trip -- bye!
```

## Program Discussion

main() 程序是驱动程序的一个例子，一个专门用于测试函数的短程序。

while 循环是我们之前使用过的形式的概括。输入 1.2 12 会导致 scanf() 成功读取两个值并返回 2，循环继续。因为 scanf() 会跳过空白，所以输入可以分布在多行上，如示例输出所示，但输入 q 会产生返回值 0，因为 q 不能使用 %lf 说明符读取。这会导致 scanf() 返回 0，从而终止循环。同样，输入 2.8 q 会产生 scanf() 返回值 1；这也会终止循环。

现在让我们来看一下与函数相关的问题。power() 函数在该程序中出现了三次。第一次出现是：

```
double power(double n, int p); // ANSI prototype
```

该语句宣布，或声明，程序将使用一个名为 power() 的函数。初始关键字 double 表示 power() 函数返回类型为 double 的值。编译器需要知道 power() 返回什么类型的值，以便知道期望多少字节的数据以及如何解释它们；这就是为什么你必须声明函数的原因。括号内的 double n, int p 表示 power() 接受两个参数。第一个应为类型 double 的值，第二个应为类型 int。

第二次出现是：

```
xpow = power(x,exp);        // function call
```

这里程序调用函数，并向其传递两个值。函数计算 x 的 exp 次幂并将结果返回给调用程序，其中返回值被赋给变量 xpow。

第三次出现是在函数定义的头部：

```
double power(double n, int p)  // function definition
```

这里 power() 接受两个参数，一个 double 和一个 int，由变量 n 和 p 表示。请注意，power() 在函数定义中出现时后面不跟分号，但在函数声明中出现时后面跟分号。函数头之后是指定 power() 执行什么操作的代码。

请回忆函数使用 for 循环计算 n 的 p 次幂的值并将其赋给 pow。下面的行使 pow 的值成为函数返回值：

```
return pow;                // return the value of pow
```

## Using Functions with Return Values

声明函数、调用函数、定义函数、使用 return 关键字——这些是定义和使用带返回值的函数的基本要素。

到目前为止，你可能有一些疑问。例如，如果你应该在你使用其返回值之前声明函数，为什么你在使用 scanf() 的返回值时没有声明 scanf()？为什么你必须单独声明 power()，而你的定义已经说明它是 double 类型？

让我们先回答第二个问题。编译器在程序中第一次遇到 power() 时需要知道 power() 的类型。此时，编译器尚未遇到 power() 的定义，因此它不知道定义说明返回类型是 double。为了帮助编译器，你通过使用前向声明来预览即将发生的事情。该声明告知编译器 power() 在其他地方定义，并且它将返回类型 double。如果你在文件中将 power() 函数定义放在 main() 之前，你可以省略前向声明，因为编译器在到达 main() 之前已经了解了 power() 的所有信息。然而，这不是标准的 C 风格。因为 main() 通常为程序提供整体框架，所以最好先显示 main()。此外，函数通常保存在单独的文件中，因此前向声明是必不可少的。

接下来，为什么你没有声明 scanf()？好吧，你声明了。stdio.h 头文件为 scanf()、printf() 和其他几个 I/O 函数提供了函数声明。scanf() 声明指出它返回类型 int。

## Key Concepts

循环是一个强大的编程工具。在设置循环时，你应特别注意三个方面：

- 清楚地定义导致循环终止的条件
- 确保循环测试中使用的值在第一次使用之前已初始化
- 确保循环在每个周期做一些事情来更新测试

C 通过数值评估来处理测试条件。结果为 0 表示假，任何其他值表示真。使用关系运算符的表达式通常用作测试，它们更具体一些。关系表达式在为真时求值为 1，在为假时求值为 0，这与新的 _Bool 类型允许的值一致。

数组由相同类型的相邻内存位置组成。你需要记住，数组元素编号从 0 开始，因此最后一个元素的下标始终比元素数量少一。C 不会检查你是否使用有效的下标值，因此责任在你。

使用函数涉及三个独立步骤：

- 1. 使用函数原型声明函数。
- 2. 从程序内部使用函数调用来使用函数。
- 3. 定义函数。

原型允许编译器查看你是否正确使用了函数，而定义则规定了函数的工作方式。原型和定义是当代编程实践中将程序元素分离为接口和实现的一个例子。接口描述了功能的使用方式，这就是原型所做的，而实现则规定了采取的具体操作，这就是定义所做的。


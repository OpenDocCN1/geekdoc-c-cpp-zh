
`printf("\nEnter Second Number : ");`

`scanf("%d", &num2);`

`printf("\nvalue of num1 before function invocation: %d", num1);`

`printf("\nvalue of num2 before function invocation: %d", num2);`

`swap(&num1,&num2);`

`printf("\nvalue of num1 after function invocation: %d", num1);`

`printf("\nvalue of num2 after function invocation: %d", num2);`

```
```

```c
printf("\n value of num2 after function invocation: %d", num2 );
getch();
```
Output:
Enter First Number : 10
Second Number : 20
value of num1 before function invocation: 10
value of num2 before function invocation: 20
value of num1 after function invocation: 20
value of num2 after function invocation: 10

`swap()` 函数在列表 5 中创建，该方法的参数是通过引用传递（call by reference）方法传递的。你会注意到，函数内部对形式参数的修改也会反映在 `main()` 中。

- 1. 请结合合适的例子解释“值传递”和“引用传递”的区别。`VTU, 2004`年2月
- 2. 描述向函数传递参数的两种方法。在什么情况下你倾向于使用每一种？请举例。`VTU, 2006`年7/8月

除了将单个值或单个引用作为函数参数外，你还可以像下一节讨论的那样，将数组作为函数参数传递。

## 14 在函数中传递数组

数组元素可以通过值传递或引用传递传递给函数。在值传递中，我们将数组元素的值传递给函数。相反，在引用传递中，我们将数组名（不带任何下标）以及数组元素的大小传递给函数。列表 6 显示了使用值传递方法向方法传递数组的示例：

### 列表 6：使用值传递方法在函数中传递数组

```c
#include <stdio.h>
#include <conio.h>
void display(int m)
{
    printf("%d \n", m);
}
void main()
{
    int i;
    clrscr();
    static int num [ ] = {50, 55, 60, 65, 60};
    for (i=0; i<4; i++)
    display(num[i]);
    getch();
}
```

Output:
50
55
60
65
60

### 列表 7：使用引用传递方法在函数中传递数组

```c
#include <stdio.h>
#include <conio.h>
float largest(float arr[], int n) {
    int i; float max;
    max=arr[0];
    for(i=1; i<n; i++)
        if(max<arr[i])
            max=arr[i];
    }
    return max;
}
void main() {
    static float value[4] = {2.5, -4.75, 1.2, 3.67};
    clrscr();
    printf("%f \n", largest(value, 4));
    getch();
}
```

Output:
3.670000

在列表 7 中，创建了 `largest()` 函数并使用引用传递方法将 `value` 数组传递给该函数。在讨论向函数传递数组之后，让我们在下一节讨论可以调用自身的特定类型函数。

## 14.5 递归函数

递归函数是在其执行过程中会调用自身，直到某些条件不再满足的函数。这种过程用于重复计算，其中每个动作都是根据上一个的结果描述的。例如，如果你正在计算一个数的阶乘，那么你该将该数乘以 -1。你继续这样做直到达到 1，以得到该数的阶乘。换句话说，如果你被要求获取五的阶乘，你执行以下乘法：

```
5*4*3*2*1
```

在这个示例中，乘法重复执行，直到数字达到 1。此示例中计算的因子可以使用递归函数计算，如列表 8 所示：

### 列表 8：使用递归函数

```c
#include<stdio.h>
#include<conio.h>
```
Output:
Enter a number = 5
Fact=120

在列表 8 中，创建了 `factorial(long)` 函数使用递归函数计算数的阶乘。

递归解决问题必须满足以下两个条件：

- 问题必须以递归的形式编写。
- 问题陈述必须包含停止条件。

列表 9 显示了另一个递归函数的示例：

## 列表 9：使用递归函数获取斐波那契数列第 n 项

```c
#include <stdio.h>
#include <conio.h>
int fibo(m) {
  if(m == 1 || m == 2)
    return(1);
  else
    return(fibo(m-1)+fibo(m-2));
}
void main() {
  int n;
  clrscr();
  printf("\nEnter term number\n");
  scanf("%d", &n);
  i=fibo(n);
  printf("\n%d Fibonacci number is %d\n",n,i);
  getch();
}
```

Output:
Enter term number 12
The 12 Fibonacci number is 144

列表 9 中创建的 `fibo()` 函数是一个计算斐波那契数列第 n 项的递归函数。程序中使用的变量根据类型和作用域表现不同。让我们在下一节讨论变量与函数的行为。

## 14.6 函数与变量

不同类型的变量用于 C 程序，它们具有相应的作用域或可见性。在函数或代码块内部定义的变量称为局部变量。它们仅在声明它们的函数或代码块内可见。然而，在函数外部定义的变量称为全局变量，在程序的所有代码块中均可见。此外，使用 `static` 和 `register` 关键字定义的变量分别称为静态变量和寄存器变量。让我们在以下标题下讨论这些变量的行为：

- 局部变量与全局变量
- 静态变量与寄存器变量

程序中的函数（包括 `main()` 函数定义的变量存储临时值。这些变量是局部的，仅在定义的函数内访问。如果在函数外部尝试访问变量，会导致编译错误。列表 10 显示了在函数外部访问局部变量的示例：

### 列表 10：在函数外部使用局部变量

```c
#include <stdio.h>
#include <conio.h>
void function() {
    printf("%d", n);
}
void main() {
    int n;
    clrscr();
    printf("enter the number");
    scanf("%d",&n);
    printf("the number entered is %d",n);
    function();
```

当你尝试编译列表 10 中的程序时，会产生编译错误：

```
undefined symbol 'n'
```

产生编译错误是因为 `main()` 函数内部定义的变量 `n` 在 `function()` 中被访问。列表 11 修改后的代码没有引起任何编译错误并成功执行：

### 列表 11：在函数内部使用局部变量

```c
#include <stdio.h>
#include <conio.h>
void function1() {
    int n=10;
    printf("\n%d", n);
}
void main() {
  int n;
  clrscr();
  printf("\nEnter the number\n");
  scanf("%d",&n);
  printf("The number entered is %d\n",n);
  function1();
  getch();
}
```

Output:
Enter the number 25
The number entered is 25
10

变量 `n` 在 `main()` 函数和 `function1()` 中均定义并在两个函数中被访问。全局变量的情况可以成功编译并执行。列表 12 显示了 C 程序中使用全局变量的示例。

### 列表 12：使用全局变量

```c
#include <stdio.h>
#include <conio.h>
int n;
void function1() {
  printf("\nInside Function %d\n", n);
}
void main() {
  clrscr();
  printf("\enter the number\n");
  scanf("%d",&n);
  printf("The number you entered is %d\n",n);
  function1();
  getch();
}
```

Output:
Enter the number 25
The number you entered is 25
Inside Function 25

变量 `n` 在列表 12 中被为全局变量，可以从程序的所有函数访问。

- 1. 在函数中定义的变量被称为........
   A. 实际变量 B. 形式变量 C. 局部变量 D. 全局变量
   `VTU, 2009`年1/2月
- 2. 解释局部变量和全局变量。`VTU, 2003`年7/8月

![](img/65598774ce63b10f1a1b26f2c84e0_383_0.png)

## 静态变量与寄存器变量

使用 `static` 关键字定义的变量称为静态变量。这些变量可以在函数或代码块内局部定义，也可以在程序中全局定义。当静态变量在函数内部定义时，它在函数内部可见并在程序执行期间保持其值。这些静态变量称为内部静态变量。然而，在程序全局定义的变量可以在程序的所有函数访问并在整个执行过程中保持其值，被称为外部静态变量。

程序的变量存储在随机访问存储 `RAM` 中。然而，某些程序变量也存储在中央处理器 `CPU` 寄存器中以加快程序的执行。需要存储在 CPU 寄存器的变量用 `register` 关键字定义。寄存器变量是局部变量。

> 使用 `register` 关键字声明变量不能保证程序的速度。只有当 CPU 寄存器时，寄存器变量才能确保程序的快速执行。

列表 13 显示了使用内部静态变量的示例：

### 列表 13：使用内部静态变量

```c
#include <stdio.h>
#include <conio.h>
void function() {
    static int result=1;
    printf("%d \n", result);
}
void main() {
    int i;
    clrscr();
    for(i=1;i<5;i++) {
        function();
    }
    getch();
}
```

Output:
2
4
8
16

列表 13 中的 `result` 变量在函数内部声明为内部静态变量，用于计算到 4 的数字积。列表 14 显示了外部静态变量的使用。

### 列表 14：使用外部静态变量

```c
#include <stdio.h>
#include <conio.h>
static int result=5;
```

## 第14 章

```c
void function1() {
    result=result*2;
    printf("%d \n", result);
}
void main() {
    int i;
    clrscr();
    for(i=1;i<5;i++) {
        function1();
    }
    getch();
}
```

输出：

10
20
40
80

列表 14 中的 `result` 变量被声明为外部静态变量，用于计算数字的乘积。

- 定义 `auto`、`global`、`static` 和 `register` 变量，并给出它们的示例。`VTU, 2005`年7/8月

在讨论了各种类型的变量及其与函数的交互后，我们本完了本章。现在，让我们总结一下你在本章中学习到的内容。

## 总结

在本章中，你学习了函数的基本概念及其实现。讨论从 C 程序中函数的概述开始。接下来，本章讨论了如何在 C 程序中定义和调用函数。在本章中，你还学习了 C 程序中使用的函数类型。本章详细讨论了两种参数传递的方法及其实现和后果。此外，你学习了如何在 C 程序中向函数传递数组。本章通过示例详细讨论了递归函数。在本章的末尾，你学习了 C 程序中不同类型的变量与函数的交互行为。

## 快速复习

- Q1. 什么是函数？
答. 函数是程序中的一个子图或语句块，用于执行特定的任务。在 C 程序中使用函数可以缩短程序的长度并增加程序的模块化程度。此外，在程序中使用函数还易于错误的检测和纠正。

## 函数操作

Q2. 解释 C 程序中使用的函数类型：
答. C 程序中使用的两种函数：通过包含定义特定函数的库来使用。这些是已经创建的函数，存放在 C 库中，可以在任何 C 程序中使用。

- 用户定义函数：由用户和程序员创建。用户定义函数必须在程序中使用之前进行定义。

Q3. 解释 `main()` 函数。
答. `main` 函数定义在 `stdio.h` 中。所有 C 程序都必须使用它，因为它是程序执行从这里开始的。然而，函数定义中使用的参数是形式参数。

Q4. 实际参数和形式参数之间的区别是什么？
答. 在调用函数期间传递的参数称为实际参数，函数定义中使用的参数称为形式参数。

Q5. 什么是递归函数？
答. 递归函数是一个不断调用它自身的函数，直到满足指定的条件。

Q6. 写一个程序使用函数计算到 50 为内偶数的之和。

```c
#include<stdio.h>
#include<conio.h>
int sum() {
 int i, sum=0;
for(i=2;i<=50;i+=i) {
 if(i%2!=0) 
 sum+=i;
 }
 return sum;
}
 void main() {
 clrscr();
 result=sum();
 printf("\nThe sum of even numbers up to 50 is %d\n", result);
 getch();
}
```

输出：
The sum of even numbers up to 50 is 650

Q7. 写一个程序使用函数找到到 50 为内奇数的之和。
答。

```c
#include<stdio.h>
#include<conio.h>
int odd() {
 int i, sum=0;
for(i=2;i<=50;i++) {
 if(i%2!=0)
 sum+=i;
 }
 return sum;
}
void main() {
    int result, n;
    clrscr();
    result=odd(n);
    printf("\nThe sum of odd numbers up to 50 is %d", result);
    getch();
}
```

输出：
The sum of odd numbers up to 50 is 624

Q8. 写一个 C 程序使用递归函数计算给定数字各位数字之和。答。

```c
#include<stdio.h>
#include<conio.h>
int sumofdigits(int n) {
    int num, sum=0;
    while(n!=0) {
        num=n%10;
        sum=sum+num;
        n=n/10;
    }
    return sum;
}
void main() {
    int n, result;
    clrscr();
    printf("\nEnter a number = ");
    scanf("%d", &n);
    result=sumofdigits(n);
    printf("\nSum of digits of the given number = %d", result);
    getch();
}
```

输出：
Enter a number = 545
Sum of digits of the given number = 14

Q9. 写一个 C 程序接受两个正整数并使用递归函数计算它们的最大公约数 `GCD`。答。

```c
#include<stdio.h>
#include<conio.h>
int GCD(int num1, int num2) {
    int num;
    if(num2==0)
    return (num1);
    else {
    num=num1%num2;
    return GCD(num2, num);
    }
}
void main() {
    int n1, n2, result;
    printf
```

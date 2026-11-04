
```c
    test(&i);
    printf("%d\n", i);
    return 0;
}

void test(int *p)
{
    *p = 20;
}
```

由于 & 运算符产生 i 的地址，&i 是指向 i 的指针，调用与声明匹配。当 test() 被调用时，我们有 p = &i。由于 p 指向 i，test() 可以改变 i 的值。因此，*p 是 i 的别名，语句 *p = 20 将 i 从 10 改为 20。因此，程序输出 20。

> 由于函数不能返回多个值，我们可以传递参数的地址并改变它们的值。

值得注意的是，传递参数的地址通常被称为另一种类型的调用，名为按引用调用。然而，它与按值调用并无不同，因为函数仍然无法改变传递参数的值。例如，考虑以下程序：

```c
#include <stdio.h>

void test(int *p);

int main(void)
{
    int *ptr, i;

    ptr = &i;
    printf("%p\n", ptr);

    test(ptr);
    printf("%p\n", ptr);
    return 0;
}

void test(int *p)
{
    int j;
    p = &j;
}
```

你认为调用 test() 后 ptr 的值是否发生了变化？答案是否定的。虽然 p 的值发生了变化并指向 j，但 ptr 保持不变，因为传递的是值；p 是 ptr 的拷贝。在第 18 章，我们将看到 C++ 提供了另一种在不传递指针的情况下修改参数的方法。特别是，我们将讨论引用和按引用调用。区分按值调用和按引用调用的人可能想说指针像引用一样可用于改变参数的值。然而，引用是 C++ 的概念，而不是 C 的。

当函数被调用时，允许混合使用指针和平常值。例如：

```c
#include <stdio.h>

void test(int *p, int a);

int main(void)
{
    int i = 100, j = 200;

    test(&i, j);
    printf("%d %d\n", i, j);
    return 0;
}

void test(int *p, int a)
{
    *p = 300;
    a = 400;
}
```

当 test() 被调用时，我们有 p = &i，且 test() 将 i 从 100 改为 300，而 j 的值没有改变。因此，程序输出 300 200。

这里有一个更困难的例子。函数如何改变指针的值？我们只需向函数传递一个指向指针的指针类型的参数。例如：

```c
#include <stdio.h>

void test(int **arg);

int var = 100;

int main(void)
{
    int *ptr, i = 30;

    ptr = &i;
    test(&ptr); /* The value of &ptr is the memory address of ptr, which points to the address of i. So, the type of the argument is a pointer to a pointer to an integer and matches the function declaration. */

    printf("%d\n", *ptr);
    return 0;
}

void test(int** arg)
{
    *arg = &var;
}
```

由于 ptr 的内存地址被传递给 test()，test() 可以改变其值。当 test() 被调用时，我们有 arg = &ptr，所以 *arg = ptr。因此，语句 *arg = &var; 等价于 ptr = &var; 这意味着 ptr 的值发生了变化并指向 var 的地址。因此，程序显示 100。我们稍后会讨论 var 的作用域。我们理解你可能会觉得这个例子有点困难。然而，因为你很可能需要阅读或编写改变指针值的代码，我们在这里添加了它，以便于查找和查阅。理论就到此为止，让我们进入练习。

## 练习

### C.11.1

在下面的程序中，scanf() 和 printf() 哪个函数可能会改变 a 的值？

```c
#include <stdio.h>
int main(void)
{
    int a;

    scanf("%d", &a);
    printf("Value: %d\n", a);
    return 0;
}
```

答案：scanf() 可能会改变 a 的值，因为传递的参数是其地址。另一方面，printf() 不能改变 a，因为传递的参数是其值。

### C.11.2

编写两个函数，分别接收一个整数参数并返回该数的平方和立方。编写一个程序读取一个整数并使用这些函数显示该数平方与立方的和。

```c
#include <stdio.h>

int square(int a);
int cube(int a);

int main(void)
{
    int i, j, k;

    printf("Enter number: ");
    scanf("%d", &i);

    j = square(i);
    k = cube(i);
    printf("sum = %d\n", j+k);  /* Without declaring the j and k variables, we could write printf("sum = %d\n", square(i)+cube(i)); */
    return 0;
}

int square(int a)
{
    return a*a;
}

int cube(int a)
{
    return a*a*a;
}
```

### C.11.3

编写一个函数，接收三个值作为参数并返回其中的最小值。编写一个程序读取三名学生的成绩并使用该函数显示最小值。

```c
#include <stdio.h>

float min(float a, float b, float c);

int main(void)
{
    float i, j, k;
    printf("Enter grades: ");
    scanf("%f%f%f", &i, &j, &k);

    printf("Min grade = %f\n", min(i, j, k));
    return 0;
}

float min(float a, float b, float c)
{
    if(a <= b && a <= c)
        return a;
    else if(b < a && b < c)
        return b;
    else
        return c;
}
```

### C.11.4

编写一个函数，接收一个整数和一个字符作为参数，并按整数的值重复显示该字符。编写一个程序读取一个整数和一个字符并使用该函数显示字符。

```c
#include <stdio.h>

void show_char(int num, char ch);

int main(void)
{
    char ch;
    int i;

    printf("Enter character: ");
    scanf("%c", &ch);

    printf("Enter number: ");
    scanf("%d", &i);

    show_char(i, ch);
    return 0;
}

void show_char(int num, char ch)
{
    int i;

    for(i = 0; i < num; i++)
        printf("%c", ch);
}
```

注释：show_char() 的返回类型声明为 void，因为它不返回任何值。

### C.11.5

下面程序的输出是什么？

```c
#include <stdio.h>

int f(int a);

int main(void)
{
    int i = 10;

    printf("%d\n", f(f(f(i))));
    return 0;
}

int f(int a)
{
    return a+1;
}
```

答案：每次调用 f() 时，它返回其参数加一后的值。调用按从内到外的顺序执行。因此，第一次调用返回 11，成为第二次调用的参数。第二次调用返回 12，成为第三次调用的参数。因此，程序显示 13。

### C.11.6

编写一个函数，接收一个字符作为参数，使用 switch 语句判断：如果字符是 'a'、'b' 或 'c' 则返回相同字符，否则返回字符 'z'。编写一个程序读取一个字符，调用该函数并显示返回值。

```c
#include <stdio.h>

char check(char ch);

int main(void)
{
    char ch;
    printf("Enter character: ");
    scanf("%c", &ch);

    printf("%c\n", check(ch));
    return 0;
}

char check(char ch)
{
    switch(ch)
    {
        case 'a':
        case 'b':
        case 'c':
        return ch;

        default:
        return 'z';
    }
}
```

### C.11.7

编写一个函数，接收三个浮点数作为参数并返回其中落在 [1, 2] 范围内的数的平均值。编写一个程序读取三个浮点数，调用该函数并显示返回值。

```c
#include <stdio.h>

double avg(double a, double b, double c);

int main(void)
{
    double i, j, k, ret;

    printf("Enter prices: ");
    scanf("%lf%lf%lf", &i, &j, &k);

    ret = avg(i, j, k);
    if(ret == -1)
        printf("No value in [1, 2]\n");
    else
        printf("Avg = %f\n", ret);
    return 0;
}

double avg(double a, double b, double c)
{
    int k = 0;
    double sum = 0;

    if(a >= 1 && a <= 2)
    {
        sum += a;
        k++;
    }
    if(b >= 1 && b <= 2)
    {
        sum += b;
        k++;
    }
    if(c >= 1 && c <= 2)
    {
        sum += c;
        k++;
    }
    if(k != 0)
        return sum/k;
    else
        return -1;
}
```

### C.11.8

下面程序的输出是什么？

```c
#include <stdio.h>

void test(int *ptr1, int *ptr2);

int main(void)
{
    int i = 10, j = 20;
    test(&i, &j);
    printf("%d %d\n", i, j);
    return 0;
}

void test(int *ptr1, int *ptr2)
{
    int m, *tmp;
    tmp = ptr1;
    ptr1 = &m;
    *ptr1 = 100;
    *ptr2 += m;
    ptr2 = tmp;
    *ptr2 = 100;
}
```

答案：调用 test() 时，我们有 ptr1 = &i 且 ptr2 = &j。语句 ptr1 = &m; 和 *ptr1 = 100; 使 m 等于 100。由于 ptr2 指向 j 的地址，*ptr2 为 20。因此，语句 *ptr2 += m; 使 j 等于 20+100 = 120。由于 tmp 指向 i 的地址，语句 ptr2 = tmp; 等价于 ptr2 = &i。因此，语句 *ptr2 = 100; 将 i 的值改为 100。结果，程序输出：100 120

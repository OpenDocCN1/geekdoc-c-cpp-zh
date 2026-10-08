

## 5.3 计算函数 299

> 编程警告：如果参数以指针的形式传递给函数参数，函数对这些指针的任何更改将反映在调用函数的参数中。

按值传递与按指针传递：了解何时按值传递以及何时按指针传递非常重要。函数通常设计用于执行特定任务并向调用程序返回单个值。对于那些在计算中使用参数且不改变其值的函数——最好始终使用按值调用。通过 `return` 语句返回单个值的函数可以用以下方式使用：

- 作为赋值语句右侧的表达式，以保存返回的值以供程序后续使用。

```c
int sum;
sum = func(arg1, arg2, arg3);
```

- 作为算术表达式中的表达式。

```c
a = b * c - func(arg1, arg2, arg3) * m / n;
```

- 作为待求值并打印的表达式。

```c
printf("Value returned = %d\n", func(arg1, arg2, arg3));
```

- 作为另一个函数调用的参数，如下所示：

```c
value = funcx(func(arg1, arg2, arg3));
```

在这种情况下，`funcx()` 的参数是调用函数 `func(arg1, arg2, arg3)` 后返回的值。换句话说，在任何可以使用相同类型表达式的地方，都可以使用简单的调用。

函数可能需要返回多个值。这只能通过使用指针变量作为参数来实现。函数可以部分参数按值传递，部分按指针传递。像 PI 等常量以及 1.75 和 'A' 等字面量只能按值传递。对于有意更改的参数，使用按指针传递是非常重要的。

---

### 5.3.3 复习题

- 1. 判断下列陈述对错。

- a. 当按值传递变量时，必须在参数列表中指定变量名。

- b. 当按指针传递变量时，必须在参数列表中指定变量名的地址。

- c. 通过按值向函数传递参数可以防止函数更改参数的值。

- d. 参数是具有其独立存储区域的局部变量。

- e. 在函数中，当按指针传递时，调用函数中的持久性参数是可以被更改的。

- f. 按指针传递参数是传递了指定变量的地址。

- g. 当指针传递给函数时，如果函数更改了参数的值，那么它就指向了不同的内容。

- h. 如果函数被写为从参数计算单个值，那么始终按值传递参数更好。

- 2. 为以下代码段中的每个非库函数编写函数声明。

- a. int main()

```c
{
int x, y, z, sum;
sum = func(x, y, z);
printf("sum = %d\n", sum);

  return 0;
}
```

```c
int func(int a, int b, int c)
{
  return a + b + c; // 根据上下文推断的逻辑
}
```

b. int main()
```c
{
float x, y, z, sum;
sum = func(&x, &y, &z);
printf("sum = %f\n", sum);

  return 0;
}
```

```c
float func(float *a, float *b, float *c)
{
  float sum1;
  sum1 = *a + *b + *c;
  return sum1;
}
```

- 3. 为以下代码中的每个非库函数编写函数声明和定义：

- a. int main()
```c
{
    int num1, num2, num3, largest_num;

    largest_num = largest(num1, num2, num3);
    printf("The largest number is %d\n", largest_num);

    return 0;
}
```

- b. int main()
```c
{
    int num1, num2, num3, smallest_num;

    smallest(&num1, &num2, &num3, &smallest_num);
    printf("The smallest number is %d\n", smallest_num);

    return 0;
}
```

---

## 5.4 输入输出函数

第 3 章中讨论的输入输出函数处理的是数据进入和输出程序。现在，我们将探索如何使用指针允许函数修改调用程序中的变量。

函数通常只能返回一个值。然而，如果我们需要返回多个值，可以传递变量的指针。这允许函数访问并修改作为参数传递的变量的实际内存位置。

下面的示例展示了如何使用指针计算两个数字的和和积。

```c
#include <stdio.h>

void calculate(int a, int b, int *sum, int *prod) {
    *sum = a + b;
    *prod = a * b;
}

int main() {
    int x, y, s, p;
    printf("Enter two numbers: ");
    scanf("%d %d", &x, &y);
    calculate(x, y, &s, &p);
    printf("Sum: %d, Product: %d\n", s, p);
    return 0;
}
```

在这个示例中，变量 `s` 和 `p` 通过地址传递给 `calculate` 函数。该函数使用解引用运算符 `*` 更新存储在这些地址的值。


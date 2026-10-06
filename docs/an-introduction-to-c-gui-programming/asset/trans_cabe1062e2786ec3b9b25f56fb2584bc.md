
## 调用函数

以下是需要翻译的

[content]
## 参数 (ARGUMENTS)

函数可以有任意数量的参数，从零到数百个。如果你不需要返回值，可以将返回类型设置为 `void`。

## 看看函数

我们向函数提供的参数在圆括号内，且与函数定义的顺序相同；所以在这种情况下，a 是 5，b 是 y 的值。

你能从一个函数返回多个结果吗？但是，你也可以使用指针将多个数据项传回调用函数。考虑这个示例：

```c
#include <stdio.h>

int sum_and_diff (int a, int b, int *res)
{
  int sum;
  sum = a + b;
  *res = a - b;
  return sum;
}

void main (void)
{
    int b = 2;
    int diff;

    printf("The sum of 5 and %d is %d\n", b,
    sum_and_diff(5, b, &diff));
    printf("The difference of 5 and %d is %d\n", b, diff);
}
```

我们修改了 `sum` 函数，以计算参数的和和差值。和之前之前返回一个整数，但我们还通过指针传回了差值。记住，函数的参数是局部变量，即使你在函数内部修改了其中一个，对调用函数传递的值也没有影响。这就是为什么指针很有用的原因：通过传递指针，函数不会更改指针本身的值，而是更改它所指向的值。

## 变量作用域 (VARIABLE SCOPE)

![](img/6a7eee5b2241c3d49170130a2016f2_36_0.png)

![](img/6a7eee5b2241c3d49170130a2016f2_36_1.png)

## 调用函数

让我们看看 main 中是如何调用函数的

```
int z = sum (5, y);
```

`sum` 函数返回一个整数，因此我们将其赋值给整数变量。我们提供的函数参数在圆括号内，与定义相同；所以在这种情况下，a 是 5，b 是 y 的值。


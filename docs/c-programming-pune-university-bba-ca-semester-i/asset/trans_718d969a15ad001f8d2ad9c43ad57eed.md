
```c
void intro()
{
    printf("Hi\n");
    printf("My name is Kiran Gurbani\n");
    printf("How are you?");
    /* there is no return statement inside this function, since its
     * return type is void */
}
```

**输出：**

Hi  
My name is Kiran Gurbani  
How are you?

**函数定义访问函数调用并将值返回主函数的图示表示。**

![](img/35ea447eca4d04af54f37bf3d3ca337d_149_0.png)

## 6.2 函数类型

函数可以带参数或不带参数定义，函数也可以返回值或不返回值。这完全取决于用户需求。

在C编程中，根据我们的需求，可以通过多种方式定义用户定义函数。以下是C语言中可用的函数类型：

- 1. 无参数且无返回值的函数
- 2. 无参数且有返回值的函数
- 3. 有参数且无返回值的函数
- 4. 有参数且有返回值的函数

### 1. 无参数且无返回值的函数

在此方法中，在定义、声明或调用函数时，我们不会向函数传递任何参数。这种类型的C函数在当我们从……调用函数时不会返回任何值

## 示例：

在这个程序中，我们将使用不带参数和 `return` 关键字的用户定义函数来计算2个整数值的乘积。

```c
#include<stdio.h>
int Multiplication();
int main()
{
    int Multi;
    Multi = Multiplication();
    printf("\n Multiplication of a and b is = %d \n", Multi);
    return 0;
}
int Multiplication()
{
    int Multi, a = 20, b = 40;
    Multi = a * b;
    return Multi;
}
```

如果你观察 `main()` 函数，我们声明了整型变量 `Multi`，并将其赋值为 `Multiplication()` 函数的返回值，因为该用户定义函数也只返回整数值。

```c
Multi = Multiplication();
```

我们没有向 `Multiplication()` 函数传递任何参数。

在下一行，使用 `printf` 语句打印输出。

```c
printf("\n Multiplication of a and b is = %d \n", Multi);
```

每当我们调用 `Multiplication()` 函数时，它都会打印上述语句。

在 `Multiplication()` 函数内部，我们声明了整型变量 `Multi`、`a` 和 `b`，并将20赋给 `a`，将40赋给 `b`。

在下一行，我们使用算术运算符（`*`）将 `a` 和 `b` 相乘。

```text
Multi = a * b
     = 20 * 40
     = 800
```

每当我们调用 `Multiplication()` 函数时，它都会打印相同的输出，因为 `a` 和 `b` 的值在函数内部是固定的。

### 3. 有参数且无返回值的函数

如果你观察上述2种方法，无论执行多少次，它们都会给出相同的输出。我们对变量 `a` 和 `b` 的值没有任何控制权，因为它们是固定值。

在实际应用中，我们大多处理动态数据，这意味着我们必须允许用户输入自己的值，而不是固定值。

此方法允许我们在调用函数时向函数传递参数。但是，当我们从 `main()` 或任何子函数调用该函数时，这种类型的函数不会返回任何值。

如果我们希望允许用户将自己的数据传递给函数参数，但不期望任何返回值，那么这种类型的函数非常有用。

## 示例：

该程序允许用户输入2个整数值，然后我们将这些值传递给用户定义函数来计算和。

```c
#include<stdio.h>
void Addition(int, int);
void main()
{
    int a, b;
    printf("\n Please Enter two integer values \n");
    scanf("%d %d", &a, &b);
    // Calling the function with dynamic values
    Addition(a, b);
}
void Addition(int a, int b)
{
    int Sum;
    Sum = a + b;
    printf("\n Addition of %d and %d is = %d \n", a, b, Sum);
}
```

如果你观察 `main()` 函数，我们声明了整型变量 `a` 和 `b`。

该程序允许用户输入2个整数值作为 `a` 和 `b`。

```c
printf("\n Please Enter two integer values \n");
scanf("%d %d", &a, &b);
```

在下一行，我们使用用户输入的值调用了 `Addition(int a, int b)` 函数。

```c
Addition(a, b);
```

在 `Addition(int a, int b)` 函数内部，我们声明了整型变量 `Sum`，并且函数中还有整型（`a`、`b`）参数。这意味着该函数将允许用户传递2个整数值。

在下一行，我们使用算术运算符（`+`）将 `a` 和 `b` 相加。

在下一行，使用 `printf` 语句打印输出。

```c
printf("\n Addition of %d and %d is = %d \n", a, b, Sum);
```

## 4. 有参数且有返回值的函数

此方法允许我们在调用函数时向函数传递参数。当我们从 `main()` 或任何子函数调用该函数时，这种类型的函数会返回某个值。返回值的数据类型将取决于函数声明的返回类型。例如，如果返回类型是 `int`，那么返回值将是 `int`。

这种类型的用户定义函数称为全动态函数，因为它为最终用户提供了最大的控制权。

**示例：**

该程序允许用户输入2个整数值，然后我们将这些值传递给用户定义函数，以将这些值相乘，并使用 `return` 关键字返回该值。

```c
#include<stdio.h>
int Multiplication(int, int);
int main()
{
    int a, b, Multi;
    printf("\n Please Enter two integer values \n");
    scanf("%d %d", &a, &b);
    // Calling the function with dynamic values
    Multi = Multiplication(a, b);
    printf("\n Multiplication of %d and %d is = %d \n", a, b, Multi);
    return 0;
}
```

```c
int Multiplication(int a, int b)
{
    int Multi;
    Multi = a * b;
    return Multi;
}
```

如果你观察 `main()` 函数，我们声明了整型变量 `Multi`、`a` 和 `b`。

该程序允许用户输入2个整数值作为 `a` 和 `b`。

```c
printf("\n Please Enter two integer values \n");
scanf("%d %d", &a, &b);
```

在下一行，我们将 `Multiplication(int a, int b)` 函数的返回值赋给 `Multi` 整数，因为该用户定义函数也只返回整数值。

```c
Multi = Multiplication(a, b);
```

我们将用户输入作为参数传递给函数 `Multiplication(int a, int b)`。

在下一行，使用 `printf` 语句打印输出。

```c
printf("\n Multiplication of a and b is = %d \n", Multi);
```

在 `Multiplication()` 函数内部，我们声明了整型变量 `Multi`，并且函数中还有两个整型（`a`、`b`）参数。这意味着该函数将允许用户传递2个整数值。

在下一行，我们使用算术运算符（`*`）将 `a` 和 `b` 相乘。

## 全局变量与局部变量

局部变量在函数内部声明。全局变量在所有函数外部声明。局部变量只能在其声明的函数中使用。全局变量可以在所有函数中使用。

```c
#include<stdio.h>
// Global variables
int x;
int y;
int add()
{
        return x + y;
}
int main()
{
        int answer; // Local variable
        x = 2;
        y = 5;
        answer = add();
        printf("%d\n", answer);
        return 0;
}
```

在示例中，声明了全局变量 `x` 和 `y`。这些变量可以在 `main()` 和 `add()` 中使用。局部变量 `answer` 只能在 `main()` 中使用。

## 6.3 按值调用与按引用调用

在C编程语言中，按值调用和按引用调用也称为传值调用和传引用调用。这些方法是将（或调用）数据传递给函数的不同方式。

在按值调用时。

在按引用调用时。

按值调用和按引用调用的函数参数可以通过两种方式传递：

- 1. 按值调用（在函数调用中，我们传递变量的值）
- 2. 按引用调用（在函数调用中，我们传递变量的引用或地址）

## 按值调用

如果数据按值传递，则数据会从例如 `main()` 中使用的变量复制到函数使用的变量。因此，如果传递的数据（即存储在函数变量中的数据）在函数内部被修改，则值只会在函数内部使用的变量中改变。让我们看一个按值调用的示例：

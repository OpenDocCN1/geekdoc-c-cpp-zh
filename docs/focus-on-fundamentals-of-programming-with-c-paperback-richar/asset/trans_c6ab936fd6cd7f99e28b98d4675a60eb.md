

- 此函数现在可以由另一个如下所示的函数调用：

```
// power2.c

#include <stdio.h>

long power(int base, unsigned exponent);

int main(void) {
    long result = power(3, 4);
    printf("%ld\n", result);
    return 0;
}

long power(int base, unsigned exponent) {
    int i;
    long num = 1;

    for(i = 0; i < exponent; ++i) {
        num *= base;
    }
    return num;
}
```

main() 中的一个语句现在调用函数 power() 并将返回值赋给变量 result，然后输出该变量。

## 示例 3：改进的 Power 函数

我们可以进一步改进 power() 函数，允许 base 为 float，允许 exponent 为正或负的 int（或零），并允许函数返回 float。

下面的程序：

```
// power3.c

#include <stdio.h>
#include <stdlib.h>

float power(float base, int exponent);

int main(void) {
    float result = power(3.5, -6);
    printf("%f\n", result);
    return 0;
}

float power(float base, int exponent) {
    int i;
    float num = 1.0;
    if (exponent == 0) {
        return 1.0;
    }
    for (i = 0; i < abs(exponent); ++i) {
        num *= base;
        if (exponent > 0) {
            return num;
        }
        else {
            return 1/num;
        }
    }
}
```

产生以下输出：

```
0.000544
```

请注意，for 循环中使用了返回 exponent 绝对值的 abs() 函数。abs() 函数是内置的 C 数学函数，使用它需要包含相应的头文件：

```
#include <stdlib.h>
```

## 再论函数原型

一般来说，C 语言不关心你在程序中放置函数的顺序，只要函数名在被调用之前已知于编译器即可。这通过使用 *函数原型* 来保证。函数原型在函数实际声明 *事先*，向程序的其余部分声明函数名、其参数及其返回类型。

函数原型放置在程序开头，在第一个函数声明之前，通常是 `main()`，由函数头加上右花括号后的分号组成。下面是一个示例：

```
// prototype.c

#include <stdio.h>

int main(void);
int add(int a, int b);
int mult(int a, int b);

int main(void) {
    int num1, num2;

    printf("Enter two integers: ");
    scanf("%d%d", &num1, &num2);
    printf("The sum of the two numbers is %d\n", add(num1, num2));
    printf("The product of the two numbers is %d\n", mult(num1, num2));

    return 0;
}

int add(int a, int b) {
    return a + b;
}

int mult(int a, int b) {
    return a * b;
}
```

程序的输出如下：

```
Enter two integers: 4 5
The sum of the two numbers is 9
The product of the two numbers is 20
```

请注意，我们甚至为 `main()` 提供了函数原型。

你是否注意到 scanf() 函数中 num1 和 num2 前面的 &？使用 scanf() 读取 int、char 或 float 时，必须向 scanf() 提供变量在内存中的地址，而不是变量名。& 在 C 中被称为地址运算符，当放置在变量前面时，返回该变量的地址。

## 关于 main() 和函数原型位置的说明...

从技术上讲，main() 可以放在程序中的任何位置。但是，它通常被放置为程序中的第一个函数。如你所见，我们通常不会在 main() 中放置太多详细代码。使用得当时，它为程序的其余部分提供了抽象，并且作为程序中第一个函数的可见性很有用。

但这不仅仅是风格问题。认为将 main() 放置为程序中的最后一个函数就可以消除对函数原型的需求是不正确的。假设你的代码设置如下：

```
void foo1() {
...
}

void foo2() {
...
}

int main() {
...
}
```

如果 main() 调用 foo1() 或 foo2() 没有问题。如果 foo2() 调用 foo1() 没有问题。但是如果 foo1() 调用 foo2() 会发生什么？编译器会报错，因为它尚未看到 foo2() 的声明。这是什么类型的函数？它有多少个参数？参数的数据类型是什么？有返回值吗？如果编译器无法回答所有这些问题，它如何对对 foo2() 的函数调用进行错误检查？使用函数原型可以让编译器在查看任何代码之前看到函数声明，从而可以正确地进行错误检查。

当然，你可能希望在程序中交换 `foo1()` 和 `foo2()` 的顺序，一切都会正常。但是，在拥有几十个函数的大型程序中，可能不容易正确地排序函数。使用函数原型，我们永远不必担心函数的顺序。

使用函数原型的最后一个原因涉及构建更大的程序和链接源代码。这将在以后讨论。

## 函数返回值

请注意，即使函数返回一个值，程序也不必使用它：

```
// return1.c

while (...) {
    :
    getchar();    // get a character and do nothing with it
    c = getchar(); // get another character and assign to c
    :
}
```

### void 返回值和 void 参数列表

如果函数不返回任何值，其返回类型应指定为 `void`。`void` 说明符告知编译器函数不返回值。从某种意义上说，`void` 数据类型实际上定义了数据类型的缺失，声明为 `void` 类型的函数没有返回值，不能像有返回值一样在表达式中使用。

```
// return2.c

void printHeader(void) {
    printf("Program Number 1\n");
    printf("by Richard Stegman\n");
    printf("Version 1.0, released 2/12/14\n");
}
```

如你所见，此函数不返回值。你可以使用以下语句调用它：

```
printHeader();
```

请注意，调用中必须包含 ()。如果不包含，函数不会被调用，即使在许多系统上它可以正确编译。

如果函数不传递任何参数（即，没有声明形式参数），则应在函数名后的括号内的参数列表中指定 void。下面是一个不接受任何值并生成并返回 0 到 255 之间随机数的函数：

```
// parameter1.c

int getRandomNumber(void) {
    return (rand() % 255);
}
```

函数头：

```
int getRandomNumber()
```

向程序的其余部分声明函数：

```
getRandomNumber()
```

并指定该函数不接受任何参数，并将返回 int 结果。

## 函数参数

传递给函数的值称为参数或实际参数。出现在函数头中的参数称为形式参数。我们说实际参数被传递给形式参数。

在 C 中，函数参数始终按值传递。每个参数都会被求值，其值在函数头中局部用于替代形式参数。因此，如果将参数传递给函数，该参数的存储值在调用环境中不会被更改。例如：

```
// parameter2.c

#include <stdio.h>

int main(void);
void foo(int num);

int main(void) {
    int num = 5;
    printf("%d\n", num);
    foo(num);
    printf("%d\n", num);
    return 0;
}

int foo(int num) {
    printf("%d\n", num);
    num = num + 1;
    printf("%d\n", num);
}
```

产生以下输出：

```
5
5
6
5
```

如果我们想按引用传递参数（即，在函数中更改参数的值，并使该新值反映回调用函数），我们必须将参数的地址传递给函数，而不是参数本身。一旦函数有权访问用于存储实际参数的内存位置，它就可以修改其内容，从而修改实际参数。

例如：

```
// parameter3.c

#include <stdio.h>

int main(void);
void foo(int *num);

int main(void) {
    int num = 5;
    printf("%d\n", num);
    foo(&num);
    printf("%d\n", num);
    return 0;
}

void foo(int *num) {
    printf("%d\n", *num);
    *num = *num + 1;
    printf("%d\n", *num);
}
```

产生以下输出：

```
5
5
6
6
```

请注意，实际参数的值已通过对 foo() 的调用而更改。

为了按引用传递，我们必须首先将实际参数的地址传递给函数。这是通过使用地址运算符 (&) 来完成的。当 & 放置在变量前面时，它返回该变量的地址。


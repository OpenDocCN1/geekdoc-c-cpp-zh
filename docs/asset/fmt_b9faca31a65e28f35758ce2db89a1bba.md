
该程序的输出为：

```
p: (10, 20)
q[0]: (1, 2)
q[4]: (9, 10)
```

在此示例中，`new`运算符用于为单个`Point`对象和一个`Point`对象数组动态分配内存。`delete`运算符用于在不再需要时释放内存。成员访问运算符`->`和`[]`用于访问对象的数据成员。

请注意，如果`new`运算符无法分配请求的内存，它会抛出`std::bad_alloc`异常，因此它通常在`try-catch`块中使用来处理异常。最好一致地使用`new`和`delete`运算符，因为将它们与C标准库中的`malloc()`和`free()`函数混合使用可能导致未定义行为。

### 按位取反运算符：`~`

在C++中，`~`运算符是按位取反运算符，用于对整数值执行按位NOT操作。它是一个一元运算符，接受一个整数操作数并返回一个整数值，该值是按位NOT操作的结果。

按位取反运算符`~`通过翻转其操作数的所有位来否定操作数的值。如果操作数是一个n位整数，`~`运算符返回一个n位整数，其所有位都被翻转。例如，`0000 1100`（十进制12）的按位取反是`1111 0011`（十进制243）。

以下是如何在C++中使用按位取反运算符的示例：

```cpp
#include <iostream>

int main() {

    int x = 12;

    int y = ~x;

    std::cout << "x: " << x << std::endl;

    std::cout << "y: " << y << std::endl;

    return 0;

}
```

该程序的输出为：

```
x: 12
y: -13
```

在此示例中，按位取反运算符`~`用于否定`x`变量的值。`~`操作的结果存储在`y`变量中并打印到控制台。

请注意，按位取反运算符的优先级高于按位与、或和异或运算符`&`、`|`和`^`，因此它通常在这些运算符之前求值。例如，表达式`~x & y`等价于`(~x) & y`，而表达式`x | ~y`等价于`x | (~y)`。

### 指向成员的运算符：`.*`和`->*`

在C++中，`.*`运算符和`->*`运算符用于通过指向对象的指针访问类或结构体的成员。

`.*`运算符用于对象本身是指针时，而`->*`运算符用于对象是实际对象且你想通过指向对象的指针访问成员时。

以下是这些运算符如何使用的示例：

```cpp
#include <iostream>

struct S

{

    int x;

    double y;

};

int main()

{

    S s{10, 3.14};

    S* p = &s;

    int S::*px = &S::x;

    double S::*py = &S::y;

    std::cout << "s.x = " << s.x << std::endl;

    std::cout << "s.y = " << s.y << std::endl;

    std::cout << "(p->*px) = " << (p->*px) << std::endl;

    std::cout << "(p->*py) = " << (p->*py) << std::endl;

    std::cout << "(s.*px) = " << (s.*px) << std::endl;

    std::cout << "(s.*py) = " << (s.*py) << std::endl;

    return 0;

}
```

该程序的输出将为：

```
s.x = 10
s.y = 3.14
(p->*px) = 10
(p->*py) = 3.14
(s.*px) = 10
(s.*py) = 3.14
```

在此示例中，我们有一个结构体`s`包含两个成员：`x`和`y`。我们创建了一个类型为`s`的对象`s`和指向`s`的指针`p`。我们还定义了`s`的两个指向成员的指针`px`和`py`，它们分别指向成员`x`和`y`。

我们可以使用点运算符`.`直接访问`s`的成员`x`和`y`，也可以使用`->*`运算符通过指针`p`访问它们。我们还可以使用`.*`运算符通过指向对象本身的指针访问`s`的成员`x`和`y`。

### 后缀增量和减量运算符：`++`和`--`

在C++中，后缀增量运算符`++`和后缀减量运算符`--`用于将变量的值增加或减少1。这些运算符称为“后缀”，因为它们出现在操作数之后（即其值被增量或减量的变量之后）。

以下是这些运算符如何使用的示例：

```cpp
#include <iostream>

int main()

{

    int x = 10;

    int y = 10;

    std::cout << "x = " << x << std::endl;

    std::cout << "y = " << y << std::endl;

    std::cout << "x++ = " << x++ << std::endl;

    std::cout << "y-- = " << y-- << std::endl;

    std::cout << "x = " << x << std::endl;

    std::cout << "y = " << y << std::endl;

    return 0;

}
```

该程序的输出将为：

```
x = 10
y = 10
x++ = 10
y-- = 10
x = 11
y = 9
```

在此示例中，我们有两个变量`x`和`y`，均初始化为10。我们使用后缀增量运算符`x++`将`x`的值增加1，并使用后缀减量运算符`y--`将`y`的值减少1。

后缀增量和减量运算符返回操作数在被增量或减量之前的值。这就是为什么`x++`和`y--`的输出为10，即使`x`和`y`的值分别被增量和减量。

需要注意的是，后缀增量和减量运算符的优先级低于大多数其他运算符，因此它们通常与其他运算符组合使用。例如：

```cpp
int a = 10;

int b = 20;

int c = a++ + b;  // c = 30, a = 11

int d = a-- - b;  // d = -1, a = 10
```

在此示例中，`c`的值计算为`10 + 20 = 30`，并在计算完成后将`a`的值递增到11。同样，`d`的值计算为`11 - 20 = -1`，并在计算完成后将`a`的值递减到10。

### 前缀增量和减量运算符：`++`和`--`

在C++中，前缀增量运算符`++`和前缀减量运算符`--`用于将变量的值增加或减少1。这些运算符称为“前缀”，因为它们出现在操作数之前（即其值被增量或减量的变量之前）。

以下是这些运算符如何使用的示例：

```cpp
#include <iostream>

int main()

{

    int x = 10;

    int y = 10;

    std::cout << "x = " << x << std::endl;

    std::cout << "y = " << y << std::endl;

    std::cout << "++x = " << ++x << std::endl;

    std::cout << "--y = " << --y << std::endl;

    std::cout << "x = " << x << std::endl;

    std::cout << "y = " << y << std::endl;

    return 0;

}
```

该程序的输出将为：

```
x = 10
y = 10
++x = 11
--y = 9
x = 11
y = 9
```

在此示例中，我们有两个变量`x`和`y`，均初始化为10。我们使用前缀增量运算符`++x`将`x`的值增加1，并使用前缀减量运算符`--y`将`y`的值减少1。
前缀增量和减量运算符返回操作数在被增量或减量之后的值。这就是为什么`++x`和`--y`的输出分别为11和9，即使`x`和`y`的值在输出产生之前就已被增量和减量。

需要注意的是，前缀增量和减量运算符的优先级高于大多数其他运算符，因此它们通常与其他运算符组合使用。例如：

```cpp
int a = 10;

int b = 20;

int c = ++a + b;  // c = 31, a = 11

int d = --a - b;  // d = -9, a = 10
```

在此示例中，`a`的值在`c`的值被计算之前被递增到11

calculated as 11 + 20 = 31 . Similarly, the value of a is decremented to 10 before the value of d is calculated as 10 - 20 = -10 .

### Relational operators: `<`, `>`, `<=`, and `>=`

In C++, the relational operators `<` , `>` , `<=` , and `>=` are used to compare the values of two operands. These operators return a boolean value indicating whether the comparison is true or false.

Here is an example of how these operators can be used:

```cpp
#include <iostream>

int main()

{

    int x = 10;

    int y = 20;

    int z = 10;

    std::cout << "(x < y) = " << (x < y) << std::endl;

    std::cout << "(x > y) = " << (x > y) << std::endl;

    std::cout << "(x <= y) = " << (x <= y) << std::endl;

    std::cout << "(x >= y) = " << (x >= y) << std::endl;

    std::cout << "(x == z) = " << (x == z) << std::endl;

    std::cout << "(x != z) = " << (x != z) << std::endl;

    return 0;

}
```

The output of this program would be:

```
(x < y) = 1

(x > y) = 0

(x <= y) = 1

(x >= y) = 0

(x == z) = 1

(x != z) = 0
```

In this example, we have three variables: `x` , `y` , and `z` . We use the relational operators to compare the values of `x` and `y` , as well as the values of `x` and `z` .

The relational operator `<` returns true if the value of the left operand is less than the value of the right operand, and false otherwise. The relational operator `>` returns true if the value of the left operand is greater than the value of the right operand, and false otherwise.

The relational operator `<=` returns true if the value of the left operand is less than or equal to the value of the right operand, and false otherwise. The relational operator `>=` returns true if the value of the left operand is greater than or equal to the value of the right operand, and false otherwise.

The relational operator `==` returns true if the value of the left operand is equal to the value of the right operand, and false otherwise. The relational operator `!=` returns true if the value of the left operand is not equal to the value of the right operand, and false otherwise.

It's important to note that the relational operators have a lower precedence than most other operators, so they are often used in combination with other operators. For example:

```cpp
int a = 10;

int b = 20;
```

```cpp
if (a < b && b > a)

{

    std::cout << "a is less than b and b is greater than a" << std::endl;

}
```

```cpp
if (a == b || a != b)

{

    std::cout << "a is either equal to b or not equal to b" << std::endl;

}
```

In this example, the first `if` statement will be true because both conditions

### Scope resolution operator: `::`

In C++, the scope resolution operator `::` is used to specify the scope in which a name is defined. It is used to qualify the name of a class, function, or variable, and is often used to access a name that is defined in a different scope.

Here is an example of how the scope resolution operator can be used:

```cpp
#include <iostream>

int x = 10;

int main()

{

    int x = 20;

    std::cout << "x = " << x << std::endl;

    std::cout << "::x = " << ::x << std::endl;

    return 0;

}
```

The output of this program would be:

```
x = 20
::x = 10
```

In this example, we have a global variable `x` and a local variable `x` in the `main` function. The local variable `x` is defined within the scope of the `main` function, while the global variable `x` is defined outside of any function and is therefore in the global scope.

We use the scope resolution operator `::` to specify the global scope when accessing the global variable `x`. Without the scope resolution operator, the local variable `x` would be accessed instead.

The scope resolution operator can also be used to access a name that is defined in a different namespace:

```cpp
#include <iostream>

namespace NS1

{

    int x = 10;

}

namespace NS2

{

    int x = 20;

    int main()

    {

        std::cout << "x = " << x << std::endl;

        std::cout << "NS1::x = " << NS1::x << std::endl;

        std::cout << "NS2::x = " << NS2::x << std::endl;

        return 0;

    }

}
```

The output of this program would be:

```
x = 20

NS1::x = 10

NS2::x = 20
```


```cpp
void doubleFirst(int one, int two)                         //Line 26
{
    cout << "Line 28: Inside doubleFirst:  one = "       //Line 27
         << one << ", two = " << two << endl;            //Line 28

    one = one * 2;                                         //Line 29

    cout << "Line 30: Inside doubleFirst:  one = "
         << one << ", two = " << two << endl;            //Line 30

    two = two + 2;                                         //Line 31

    cout << "Line 32: Inside doubleFirst:  one = "
         << one << ", two = " << two << endl;            //Line 32
}                                                          //Line 33

void squareFirst(int& ref, int val)                        //Line 34
{                                                          //Line 35
    cout << "Line 36: Inside squareFirst: ref = "
         << ref << ", val = " << val << endl;             //Line 36

    ref = ref * ref;                                        //Line 37

    cout << "Line 38: Inside squareFirst: ref = "
         << ref << ", val = " << val << endl;             //Line 38

    val = val + 2;                                         //Line 39

    cout << "Line 40: Inside squareFirst: ref = "
         << ref << ", val = " << val << endl;             //Line 40
}                                                          //Line 41
```

### 示例运行：

```text
Line 9: Inside main:  num = 5
Line 20: Inside addFirst:  first = 5, second = 5
Line 22: Inside addFirst:  first = 7, second = 7
Line 24: Inside addFirst:  first = 14, second = 14
Line 11: Inside main after addFirst: num = 14
Line 28: Inside doubleFirst:  one = 14, two = 14
Line 30: Inside doubleFirst:  one = 28, two = 14
Line 32: Inside doubleFirst:  one = 28, two = 16
Line 13: Inside main after doubleFirst: num = 14
Line 36: Inside squareFirst: ref = 14, val = 14
Line 38: Inside squareFirst: ref = 196, val = 14
Line 40: Inside squareFirst: ref = 196, val = 16
Line 15: Inside main after squareFirst: num = 196
```

函数 `addFirst` 的两个参数都是引用参数，而函数 `doubleFirst` 的两个参数都是值参数。语句：

```cpp
addFirst(num, num);
```

在函数 `main` 中（第 10 行）将 `num` 的引用传递给函数 `addFirst` 的两个形参 `first` 和 `second`，因为这两个形参对应的实参相同。也就是说，变量 `first` 和 `second` 指向同一个内存位置，即 `num`。图 6-14 说明了这种情况。

![](img/b217c421655b51e7494cf3b89bb5432d_447_0.png)

**图 6-14** 函数 `addFirst` 的参数

`first` 对其值所做的任何修改都会立即改变 `second` 和 `num` 的值。同样，`second` 对其值所做的任何修改都会立即改变 `first` 和 `num`，因为这三个变量都指向同一个内存位置。（注意，`num` 被初始化为 5。）

函数 `doubleFirst` 的形参是值参数。因此，语句：

```cpp
doubleFirst(num, num);
```

在函数 `main` 中（第 12 行）将 `num` 的值复制到 one 和 two，因为这两个形参对应的实参相同。图 6-15 说明了这种情况。

![](img/b217c421655b51e7494cf3b89bb5432d_447_1.png)

**图 6-15** 函数 `doubleFirst` 的参数

因为 `one` 和 `two` 都是值参数，所以 one 对其值所做的任何修改都不会影响 `two` 和 `num` 的值。同样，`two` 对其值所做的任何修改也不会影响 `one` 和 `num`。（注意，在函数 `doubleFirst` 执行之前，`num` 的值是 14。）

函数 `squareFirst` 的形参 `ref` 是引用参数，形参 `val` 是值参数。变量 `ref` 接收其对应实参的地址，即 `num`，而变量 `val` 复制其对应实参的值，该值也是 `num`。因此，`num` 和 `ref` 都指向同一个内存位置，即 `num`。图 6-16 说明了这种情况。

![](img/b217c421655b51e7494cf3b89bb5432d_448_0.png)

**图 6-16** 函数 `squareFirst` 的参数

`ref` 所做的任何修改都会立即改变 `num`。`val` 所做的任何修改都不会影响 `num`。（注意，在函数 `squareFirst` 执行之前，`num` 的值是 14。）

我们建议你走查示例 6-15 中的程序。输出显示了语句执行的顺序。

## 引用参数与有返回值函数

本章前面在讨论有返回值函数时，你学习了如何仅使用值参数。你也可以在有返回值函数中使用引用参数，尽管不推荐这种做法。根据定义，有返回值函数返回单个值；该值通过 `return` 语句返回。如果一个函数需要返回多个值，按照良好编程风格的惯例，应将其改为 `void` 函数，并使用适当的引用参数来返回这些值。

## 标识符的作用域

前面的小节给出了几个带有用户自定义函数的程序示例。标识符可以在函数头中、块内或块外声明。自然会产生一个问题：是否允许在程序中的任何位置访问任何标识符？答案是否定的。访问标识符必须遵循一定的规则。标识符的作用域是指标识符在程序中可访问（可见）的位置。回想一下，标识符是 C++ 中某个事物的名称，例如变量名或函数名。

本节考察标识符的作用域。首先，我们定义以下两个术语：

- **局部标识符：** 在函数（或块）内声明的标识符。
  局部标识符在函数（块）外不可访问。
- **全局标识符：** 在每个函数定义之外声明的标识符。

此外，C++ 不允许函数嵌套。也就是说，不能将一个函数的定义包含在另一个函数体中。

通常，访问标识符时适用以下规则：

1. **全局标识符**（如变量）在满足以下条件时可由函数或块访问：
   a. 该标识符在函数定义（块）之前声明，
   b. 函数名与该标识符不同，
   c. 函数的所有形参名都与该标识符名不同，并且
   d. 所有局部标识符（如局部变量）的名称都与该标识符名不同。
2. **（嵌套块）** 在块内声明的标识符可访问的范围是：
   a. 仅在该块内，从声明点直到该块结束；并且
   b. 如果嵌套块没有与外部块（包围该嵌套块的块）同名的标识符，则由嵌套在该块内的块访问。
3. 函数名的作用域类似于在任何块之外声明的标识符的作用域。也就是说，函数名的作用域与全局变量的作用域相同。

在考虑用示例解释这些作用域规则之前，首先注意在 `for` 语句中声明的标识符的作用域。C++ 允许程序员在 `for` 语句的初始化语句中声明变量。例如，以下 `for` 语句：

```cpp
for (int count = 1; count < 10; count++)
    cout << count << endl;
```

声明变量 count 并将其初始化为 1。变量 count 的作用域仅限于 `for` 循环体。

> **注意**  
> 在 `for` 语句中声明的变量的这条作用域规则可能不适用于标准 C++，即非 ANSI/ISO 标准 C++。在标准 C++ 中，在 `initialize` 语句中声明的变量的作用域可以从声明点一直延伸到紧邻包围该 `for` 语句的块的末尾。（为了绝对确定，请查阅编译器的文档。）

以下 C++ 编程代码有助于说明这些作用域规则：

```cpp
#include <iostream>

using namespace std;
```

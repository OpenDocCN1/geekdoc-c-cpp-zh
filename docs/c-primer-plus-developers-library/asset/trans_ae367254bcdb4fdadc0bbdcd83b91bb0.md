
程序清单7.5 进行了如下函数调用：

```cpp
int sum = sum_arr(cookies, ArSize);
```

这里，`cookies` 是一个数组名，因此根据 C++ 的规则，`cookies` 是数组第一个元素的地址。函数传递的是一个地址。由于数组的元素类型为 `int`，所以 `cookies` 必须是 int 指针类型，即 `int *`。这意味着正确的函数头应该是这样：

```cpp
int sum_arr(int * arr, int n)  // arr = array name, n = size
```

这里 `int *arr` 取代了 `int arr[ ]`。事实证明，这两个函数头都是正确的，因为在 C++ 中，符号 `int *arr` 和 `int arr[ ]` 在函数头或函数原型中使用时（也仅在这种情况下）含义完全相同。两者都表示 `arr` 是一个指向 `int` 的指针。不过，数组表示法版本（`int arr[ ]`）在符号上提醒你：`arr` 不仅指向一个 `int`，而且指向 int 数组中的第一个 int。当指针指向数组的第一个元素时，本书使用数组表示法；当指针指向一个孤立的值时，则使用指针表示法。请记住，在任何其他上下文中，`int *arr` 和 `int arr[ ]` 都不是同义词。例如，不能在函数体内使用 `int[ ]` 表示法来声明指针。

既然变量 `arr` 实际上是一个指针，函数的其余部分也就顺理成章了。你可能还记得第4章讨论动态数组时的内容：无论使用数组名还是指针，都可以使用方括号数组表示法来访问数组元素。无论 `arr` 是指针还是数组名，表达式 arr[3] 都表示数组的第4个元素。此时提醒你注意以下两个恒等式，大概也无妨：

```cpp
arr[i] == *(arr + i)    // values in two notations
&arr[i] == arr + i      // addresses in two notations
```

记住，对指针（包括数组名）加 1，实际增加的数值等于该指针所指向类型的大小（以字节为单位）。指针加法和数组下标是从数组开头数元素的两种等价方式。

## 使用数组作为参数的含义

让我们来看看程序清单7.5的含义。函数调用 `sum_arr(cookies, ArSize)` 将 cookies 数组第一个元素的地址和数组的元素个数传递给 `sum_arr()` 函数。`sum_arr()` 函数将 cookies 地址初始化为指针变量 arr，并将 ArSize 初始化为 int 变量 n。这意味着程序清单7.5并未真正将数组内容传递给函数。相反，它告诉函数数组在哪里（地址）、元素是什么类型（类型）以及有多少个元素（n 变量）。（见图7.4。）有了这些信息，函数就可以使用原始数组。如果传递的是普通变量，函数使用的是副本；但如果传递的是数组，函数使用的是原始数据。实际上，这种差异并不违背 C++ 的按值传递方式。`sum_arr()` 函数仍然传递一个被赋给新变量的值。但这个值只是一个地址，而不是数组的内容。

![](img/9afc44517b591d64e2e19f623c9308ef_337_0.png)

数组名和指针之间的这种对应关系是好事吗？确实如此。使用数组地址作为参数这一设计决策，节省了复制整个数组所需的时间和内存。如果处理的是大型数组，使用副本的开销可能会高得令人无法承受。使用副本时，程序不仅需要更多的计算机内存，还必须花时间复制大块数据。另一方面，使用原始数据会增加意外破坏数据的可能性。在经典 C 中，这是一个现实问题，但 ANSI C 和 C++ 的 `const` 限定符提供了一种补救措施。你很快就会看到示例。但首先，让我们修改程序清单7.5，以阐明数组函数是如何运作的。程序清单7.6 演示了 cookies 和 `arr` 具有相同的值。它还展示了指针概念如何使 `sum_arr` 函数比乍看起来更加通用。为了增加一点变化，并让你看到它的样子，程序使用了 `std::` 限定符而不是 using 指令来访问 `cout` 和 `endl`。

### 程序清单7.6 `arrfun2.cpp`

```cpp
// arrfun2.cpp -- functions with an array argument
#include <iostream>
const int ArSize = 8;
int sum_arr(int arr[], int n);
// use std:: instead of using directive
int main()
{
    int cookies[ArSize] = {1,2,4,8,16,32,64,128};
// some systems require #pragma once in with static to
// enable array initialization

    std::cout << cookies << " = array address, ";
    // some systems require a type cast: unsigned (cookies)

    std::cout << sizeof cookies << " = sizeof cookies\n";
    int sum = sum_arr(cookies, ArSize);
    std::cout << "Total cookies eaten: " << sum << std::endl;
    sum = sum_arr(cookies, 3);        // a lie
    std::cout << "First three eaters ate " << sum << " cookies.\n";
    sum = sum_arr(cookies + 4, 4);     // another lie
    std::cout << "Last four eaters ate " << sum << " cookies.\n";
    return 0;
}

// return the sum of an integer array
int sum_arr(int arr[], int n)
{
    int total = 0;
    std::cout << arr << " = arr ";
    // some systems require a type cast: unsigned (arr)

    std::cout << sizeof arr << " = sizeof arr\n";
    for (int i = 0; i < n; i++)
        total = total + arr[i];
    return total;
}
```

下面是程序清单7.6 的输出：

```text
003E9FC = array address, 32 = sizeof cookies
003E9FC = arr, 4 = sizeof arr
Total cookies eaten: 255
003E9FC = arr, 4 = sizeof arr
First three eaters ate 7 cookies.
003E9FA0 = arr, 4 = sizeof arr
Last four eaters ate 240 cookies.
```

注意，地址值以及数组和整数的大小会因系统而异。另外，有些实现会以十进制表示法而不是十六进制来显示地址。其他实现则会使用十六进制数字和 0x 十六进制前缀。

### 程序说明

程序清单7.6 阐明了有关数组函数的一些非常有趣的观点。首先，注意 cookies 和 arr 的求值结果都是同一个地址，与我们声称的完全一致。但是 sizeof cookies 是 32，而 sizeof arr 只有 4。这是因为 sizeof cookies 是整个数组的大小，而 sizeof arr 是指针变量的大小。（这次程序运行是在一个使用 4 字节地址的系统上进行的。）顺便说一下，这就是为什么你必须在 sum_arr() 中显式传递数组大小，而不是使用 sizeof arr 的原因；指针本身并不能揭示数组的大小。

由于 sum_arr() 知道数组中元素个数的唯一途径，是通过第二个参数告诉它的，所以你可以对函数撒谎。例如，程序第二次使用该函数时，进行了如下调用：

```cpp
sum = sum_arr(cookies, 3);
```

通过告诉函数 cookies 只有 3 个元素，你使得函数计算前 3 个元素的和。

何必要就此打住？你还可以在数组从哪里开始上撒谎：

```cpp
sum = sum_arr(cookies + 4, 4);
```

由于 cookies 充当第一个元素的地址，因此 cookies + 4 充当第五个元素的地址。这条语句对数组的第5、6、7、8个元素求和。注意输出中，对该函数的第三次调用给 arr 分配的地址与前两次调用不同。是的，你可以使用 &cookies[4] 而不是 cookies + 4 作为参数；两者的含义相同。

> **注意**
>
> 要向处理数组的函数指明数组的类型和元素个数，应将信息作为两个独立的参数传递：
>
>     void fillArray(int arr[], int size);    // prototype
>
> 不要试图使用方括号表示法传递数组大小：
>
>     void fillArray(int arr[size]);          // NO -- bad prototype

## 更多数组函数示例

当你选择使用数组来表示数据时，你正在做出一个设计决策。但设计决策不应仅限于数据存储方式，还应涉及数据的使用方式。你常常会发现，编写专门的函数来处理特定的数据操作是很有益处的。（这些益处包括提高程序的可靠性、便于修改和便于调试。）此外，当你开始在设计程序时将存储属性与操作结合起来时，你就向面向对象编程（OOP）的思维模式迈出了重要一步；这一点在未来也可能被证明是有益的。

让我们考察一个简单的案例。假设你想用一个数组来记录你的房地产的美元价值。（如果有必要，就假设你拥有房地产。）你必须决定使用什么类型。当然，double 在取值范围上比 int 或 long 限制更少，并且它提供了足够的有效数字来精确地表示这些值。接下来，你必须决定数组元素的个数。（对于用 new 创建的动态数组，你可以推迟这个决定，但这里我们还是简单一点。）假设你最多有五处房产，那么你就可以使用一个包含五个 double 的数组。

现在考虑一下你可能想对这个房地产数组执行哪些操作。两个最基本的操作是将值读入数组和显示数组

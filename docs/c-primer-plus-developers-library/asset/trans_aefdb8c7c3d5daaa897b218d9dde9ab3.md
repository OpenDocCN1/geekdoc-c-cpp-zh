

现在让我们看第二种策略，这种策略在开发 C++ 类时变得尤为重要。这种策略基于指针，指针是存储值的地址而不是值本身的变量。但在讨论指针之前，让我们先谈谈如何显式地找到普通变量的地址。你只需对变量应用地址运算符（用 `&` 表示）来获取其位置；例如，如果 `home` 是一个变量，那么 `&home` 就是它的地址。程序清单 4.14 演示了这个运算符。

## 程序清单 4.14 `address.cpp`

```cpp
// address.cpp -- using the & operator to find addresses
#include <iostream>
int main()
{
    using namespace std;
    int donuts = 6;
    double cups = 4.5;

    cout << "donuts value = " << donuts;
    cout << " and donuts address = " << &donuts << endl;
    // NOTE: you may need to use unsigned (&donuts)
    // and unsigned (&cups)
    cout << "cups value = " << cups;
    cout << " and cups address = " << &cups << endl;
    return 0;
}
```

以下是程序清单 4.14 中的程序在某个系统上的输出：

```text
donuts value = 6 and donuts address = 0x0065fd40
cups value = 4.5 and cups address = 0x0065fd44
```

这里展示的 `cout` 特定实现会在显示地址值时使用十六进制记法，因为这是指定内存地址时常用的记法。（有些实现则使用十进制记法。）我们的实现把 donuts 存储在比 cups 更低的内存位置。两个地址之差为 0x0065fd44 − 0x0065fd40，即 4。这是合理的，因为 donuts 是 `int` 类型，使用 4 个字节。当然，不同的系统会给出不同的地址值。有些系统也可能先存储 cups，再存储 donuts，由于 cups 是 `double`，二者相差 8 个字节。还有些系统甚至可能不使用相邻位置。

因此，使用普通变量时，值被当作具名量，而位置被当作派生量。现在让我们看看指针策略，这种策略对于 C++ 内存管理的编程哲学至关重要。（参见下面的侧栏“指针与 C++ 哲学”。）

## 指针与 C++ 哲学

面向对象编程与传统过程式编程的不同之处在于，OOP 强调在运行时而不是在编译时做出决策。*运行时*是指程序正在运行的时候，而*编译时*是指编译器把程序组合起来的时候。运行时决策就像在度假时根据天气和当时的心情选择要看什么景点，而编译时决策更像是遵循预设的日程，不管条件如何。

运行时决策提供了根据当前情况调整的灵活性。例如，考虑为数组分配内存。传统方式是声明一个数组。在 C++ 中声明数组时，你必须确定一个特定的数组大小。因此，数组大小在程序编译时就被设定；这是一个编译时决策。也许你认为 20 个元素的数组在 80% 的情况下足够用，但偶尔程序需要处理 200 个元素。为了保险起见，你使用一个包含 200 个元素的数组。这导致程序在大多数使用时间里浪费内存。OOP 试图通过将这类决策推迟到运行时来使程序更灵活。这样，在程序运行后，你可以告诉它某次只需要 20 个元素，而另一次需要 205 个元素。

简而言之，使用 OOP 时，你会希望把数组大小作为运行时决策。为了使这种方法可行，语言必须允许你在程序运行时创建数组——或等价物。你很快就会看到，C++ 的方法涉及使用关键字 `new` 请求正确数量的内存，并使用指针跟踪新分配的内存所在的位置。

做出运行时决策并非 OOP 独有。但 C++ 让编写代码比 C 稍微更直接一些。

处理存储数据的新策略把关系颠倒过来：把位置当作具名量，把值当作派生量。一种特殊类型的变量——*指针*——保存一个值的地址。因此，指针的名称表示位置。应用 `*` 运算符（称为*间接值*运算符或*解引用*运算符）会得到该位置处的值。（是的，这就是用于乘法的同一个 `*` 符号；C++ 会根据上下文判断你指的是乘法还是解引用。）例如，假设 `manly` 是一个指针。在这种情况下，`manly` 表示一个地址，而 `*manly` 表示该地址处的值。组合 `*manly` 等价于一个普通的 `int` 类型变量。程序清单 4.15 演示了这些概念。它还展示了如何声明指针。

## 程序清单 4.15 `pointer.cpp`

```cpp
// pointer.cpp -- our first pointer variable
#include <iostream>
int main()
{
    using namespace std;
    int updates = 6;          // declare a variable
    int * p_updates;          // declare pointer to an int
    p_updates = &updates;     // assign address of int to pointer

    // express values two ways
    cout << "Values: updates = " << updates;
    cout << ", *p_updates = " << *p_updates << endl;

    // express address two ways
    cout << "Addresses: &updates = " << &updates;
    cout << ", p_updates = " << p_updates << endl;

    // use pointer to change value
    *p_updates = *p_updates + 1;
    cout << "Now updates = " << updates << endl;
    return 0;
}
```

以下是程序清单 4.15 中的程序的输出：

```text
Values: updates = 6, *p_updates = 6
Addresses: &updates = 0x0065fd48, p_updates = 0x0065fd48
Now updates = 7
```

如你所见，int 变量 updates 和指针变量 p_updates 只是同一枚硬币的两面。updates 变量以值为主，并使用 & 运算符获取地址；而 p_updates 变量以地址为主，并使用 * 运算符获取值（见图 4.8）。因为 p_updates 指向 updates，所以 *p_updates 和 updates 完全等价。你可以像使用 int 类型变量一样使用 *p_updates。正如程序清单 4.15 中的程序所示，你甚至可以给 *p_updates 赋值。这样做会改变被指向的值，即 updates。

![](img/9afc44517b591d64e2e19f623c9308ef_170_0.png)

这强调了一个概念：`int*` 是一种类型，即指向 int 的指针。把空格放在哪里对编译器来说没有区别。你甚至可以这样做：

```
int*ptr;
```

但要注意，下面的声明创建了一个指针（`p1`）和一个普通的 `int`（`p2`）：

```
int* p1, p2;
```

每个指针变量名都需要一个 `*`。

> **注意**
> 
> 在 C++ 中，`int *` 这种组合是一种复合类型，即指向 int 的指针。

你可以使用相同的语法声明指向其他类型的指针：

```
double * tax_ptr; // tax_ptr points to type double
char * str;       // str points to type char
```

因为你把 `tax_ptr` 声明为指向 double 的指针，所以编译器知道 `*tax_ptr` 是一个 double 类型的值。也就是说，它知道 `*tax_ptr` 表示一个以浮点格式存储的数，在大多数系统上占用 8 个字节。指针变量从来不只是指针。它始终是指向特定类型的指针。`tax_ptr` 的类型是指向 double 的指针（或类型 double *），而 `str` 的类型是指向 char 的指针（或 char *）。虽然二者都是指针，但它们是两种不同类型的指针。与数组一样，指针也是基于其他类型的。

注意，虽然 `tax_ptr` 和 `str` 指向两种不同大小的数据类型，但 `tax_ptr` 和 `str` 这两个变量本身通常大小相同。也就是说，char 的地址与 double 的地址大小相同，就像 1016 可能是百货商店的街道地址，而 1024 可能是小别墅的街道地址一样。地址的大小或值并不能真正告诉你该地址处所找到的变量或建筑的大小或种类。通常，地址需要 2 或 4 个字节，具体取决于计算机系统。（有些系统的地址可能更大，而且一个系统可以针对不同类型使用不同的地址大小。）

你可以使用声明语句来初始化指针。在这种情况下，初始化的是指针，而不是被指向的值。也就是说，下面的语句把 `pt`（而不是 `*pt`）设置为值 `&higgins`：

```
int higgins = 5;
int * pt = &higgins;
```

程序清单 4.16 演示了如何将指针初始化为一个地址。

## 程序清单 4.16 `init_ptr.cpp`

```cpp
// init_ptr.cpp -- initialize a pointer
#include <iostream>
int main()
{
```


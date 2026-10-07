

# 指针与 C++ 哲学

面向对象编程与传统的过程式编程不同，OOP OOP 强调在运行时而非编译时做出决策。运行时是指程序正在运行的时候，而编译时是指编译器组装程序的时候。运行时决策就像，在度假时，根据当时的天气和心情选择要看的景点，而编译时决策更像是严格遵守预设的日程表，不论条件如何。

运行时决策提供了根据当前情况进行调整的灵活性。例如，考虑为数组分配内存。传统的方法是声明一个数组。在 C++ 中声明数组，你必须承诺使用特定的数组大小。因此，数组大小在程序编译时就已确定；这是一个编译时决策。也许你认为 20 个元素的数组 80% 的时间足够，但偶尔程序需要 120 个元素。所以你使用 200 个元素的数组。这导致你的程序大部分时间都在浪费内存。OOP 试图通过将决策推迟到运行时来使程序更灵活。这样，在程序运行后，你可以告诉它某次只需要 20 个元素，另一次需要 205 个元素。

简而言之，使用 OOP，你希望将数组大小作为运行时决策。为了使这种方法成为可能，语言允许你在程序运行时声明数组——或其等价物。C++ 的方法，如你很快就会看到的，涉及使用关键字 new 请求正确数量的内存，并使用指针来跟踪新分配的内存所在位置。

做出决策并非 OOP 独有。C++ 使编写代码比 C 更为直接。

处理存储数据的新的策略围绕着将位置视为派生量、将值视为派生量。一种特殊的变量——指针——保存变量的地址。因此，指针的名称代表位置。应用 * 运算符，称为间接值运算符或解引用运算符，可得到该位置的值。 （是的，这就是用于乘法的 * 符号；C++ 使用上下文来确定你是表示乘法还是解引用。）假设，例如，manly 是一个指针。在这种情况下，manly 代表一个地址，而 *manly 代表该地址处的值。组合 *manly 等同于一个普通的 type 变量。清单 4.15 演示了这些想法。它还展示了如何声明一个指针。

## 清单 4.15 pointer.cpp

```cpp
// pointer.cpp -- our first pointer variable
#include <iostream>
int main() {

    using namespace std;
    int updates = 6; // declare a variable
    int * p_updates; // declare pointer to an int

p_updates = &updates; // assign address of int to pointer

```cpp
// express values two ways
cout << "Values: updates = " << updates;
cout << " " << *p_updates << " " << *p_updates << endl;
```

```cpp
// express address two ways
cout << "Addresses: &updates = " << &updates;
cout << " " << *p_updates << " " << *p_updates << endl;
```

```cpp
// use pointer to change value
*p_updates = *p_updates + 1;
cout << "New updates = " << updates << endl;
return 0;
```

以下是清单 4.15 中程序的输出：
Values: updates = 6, *p_updates = 6
Addresses: &updates = 0x0065fd48, p_updates = 0x0065fd48
Now updates = 7

正如你所见，int 变量和指针变量 p_updates 只是同一枚硬币的两面。updates 变量将值作为主要部分，并使用 & 运算符获取地址，而 p_updates 变量将地址作为主要部分，并使用 * 运算符获取值（参见图 4.8）。由于 p_updates 指向 updates，*p_updates 和 updates 完全等价。你可以使用 *p_updates 来更新 updates，*updates 就像你使用一个 type int 变量一样。正如清单 4.15 中的程序所示，你甚至可以为 *p_updates 分配值。这样会改变被指向的值 updates。

```cpp
int * jumbo = 23;
int *pe = &jumbo;
```

![](img/cd11a87c1db9aff4db4b1883427463170_0.png)
图 4.8 硬币的两面。

## 声明和初始化指针

让我们检查声明指针的过程。计算机需要跟踪指针所指值的类型。例如，char 的地址通常看起来与 double 的地址相同，但它们使用不同的字节数和内部格式来表示值。因此，指针声明必须指定指针指向的数据类型。例如，前面的示例有此声明：

```cpp
int * p_updates;
```

这说明组合 *p_updates 是 type int。由于 * 运算符通过将其应用于指针，p_updates 变量本身必须是指针。我们说 p_updates 指向 type int。我们还说 p_updates 的类型是 pointer-to-int 或，更简洁地说，*。重申：p_updates 是一个指针（一个地址），而 *p_updates 是一个 int 而不是指针（参见图 4.9）。

| Memory address | Variable name |
| :--- | :--- |
| 1000 | ducks |
| 1002 | birdog |
| 1004 | points to ducks |
| 1006 | 1000 |
| 1008 | birdog |
| 1010 | |
| 1012 | |
| 1014 | |
| 1016 | |

```cpp
int ducks = 12;
int *birdog = &ducks;
```
creates ducks variable, stores the value 12 in the variable
creates birdog variable, stores the address of ducks in the variable

图 4.9 指针存储。

顺便说一下，* 周围使用空格是可选的。传统上，C 程序员使用这种形式：

```cpp
int *ptr;
```

这强调了组合 *ptr 是 type int 值。许多 C++ 程序员则使用这种形式：

```cpp
int* ptr;
```

## 复合类型

这强调了 int* 是 type pointer-to-int。你放置空格的位置对编译器没有任何影响。你甚至可以这样做：

```cpp
int *ptr;
```

请注意，然而，以下声明创建了一个指针（p1）和一个普通的 int（p2）：

```cpp
int* p1, p2;
```

你需要为每个指针名称使用 *。

注意：C++，组合 int * 是一个复合类型，pointer-to-int。你可以使用语法声明指向其他类型的指针：

```cpp
double *tax_ptr; // tax_ptr points to type double
char * str; // str points to type char
```

由于你将 tax_ptr 声明为 pointer-to-double，编译器知道 *tax_ptr 是一个 double 值。也就是说，已知 *tax_ptr 表示一个以浮点格式表示的数字，在大多数系统上占用 8 字节。指针变量永远不是指针。它始终是指向特定类型的指针：tax_ptr（或 double *），而 str 是 type pointer-to-char（或 char *）。尽管两者都是指针，但它们是不同类型的指针。像数组一样，指针基于其他类型。

注意 tax_ptr 和 str 指向不同大小的数据类型时，两个变量 tax_ptr 和 str 本身大小相同。那，char 的地址与 double 的地址大小相同，就像 1016 可能是百货商店的街道地址，1024 可能是小屋的街道地址。地址的大小或值并不能告诉你你在地址处找到的变量的大小或种类。通常，地址需要 2 或 4 字节，具体取决于计算机系统（某些系统具有更大的地址，并且系统可为不同类型使用不同的地址）。

你可以使用声明来初始化指针。在这种情况下，初始化的是指针，而不是被指向的对象。也就是说，以下语句将 pt 和 *pt 设置为 updates 的值：

```cpp
int updates = 5;
int *pt = &updates;
```

清单 4.16：如何将指针初始化为地址。

## 清单 4.16 init_ptr.cpp

```cpp
// init_ptr.cpp -- initialize a pointer
#include <iostream>
int main()
{
    using namespace std;
    int updates = 5;
    int * pt = &updates;

    cout << "Value of updates = " << updates;
    cout << " Address of updates = " << &updates << endl;
    cout << "Value of *pt = " << *pt;
    cout << " Value of pt = " << pt << endl;
    return 0;
}
```

以下是清单 4.16 中程序的一些示例输出：
Value of updates = 5; Address of updates = 0x012FED4
Value of *pt = 5; Value of pt = 0x012FED4

你可以看到指针初始化 pt，而不是 *pt，为 updates 的地址。 （你的系统很可能显示不同的地址值并以不同的格式显示它们。）

# 指针与自由存储

## 指针危险

粗心使用指针会招致危险。一个极其重要的点是，当你在 C++ 中创建指针时，计算机分配内存来保存地址，但它不会分配内存来保存地址指向的数据。创建数据的空间涉及单独的一步。省略该步骤，如下所示，是灾难的邀请：

```cpp
long *fellow; // create a pointer-to-long
*fellow = 22323; // place a value in a never-ever land
```

# 警告

指针黄金法则：在使用解引用运算符 (*) 对其进行操作之前，始终将指针初始化为明确且适当的地址。


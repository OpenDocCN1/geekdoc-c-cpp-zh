
```cpp
for (int i = 0; i < SIZE; i++)
{
    cout << i + 1 << ": ";
    getline(cin, list[i]);
}

cout << "Your list:\n";
display(list, SIZE);

return 0;
}

void display(const string sa[], int n)
{
    for (int i = 0; i < n; i++)
        cout << i + 1 << ": " << sa[i] << endl;
}
```

下面是程序清单 7.14 中程序的一次示例运行：

```text
Enter your 5 favorite astronomical sights:
1: Orion Nebula
2: M13
3: Saturn
4: Jupiter
5: Moon
Your list:
1: Orion Nebula
2: M13
3: Saturn
4: Jupiter
5: Moon
```

这个示例中需要注意的要点是，除了 `getline()` 函数之外，该程序对 `string` 的处理方式与对任何内置类型（例如 `int`）的处理方式完全相同。如果你想要一个 `string` 数组，只需使用通常的数组声明格式：

```cpp
string list[SIZE];    // an array holding 5 string objects
```

于是，`list` 数组的每个元素都是一个 `string` 对象，并且可以按 `string` 对象的方式使用：

```cpp
getline(cin, list[i]);
```

同样，形参 `sa` 是指向 `string` 对象的指针，因此 `sa[i]` 是一个 `string` 对象，可以相应地使用：

```cpp
cout << i + 1 << ": " << sa[i] << endl;
```

## 函数与 array 对象

C++ 中的类对象基于结构，因此一些适用于结构的编程考虑也适用于类。例如，你可以按值将对象传递给函数，此时函数作用于原始对象的副本。或者，你可以传递指向对象的指针，这样函数就能作用于原始对象。让我们看一个使用 C++11 `array` 模板类的示例。

假设我们有一个 `array` 对象，用于保存一年四个季节各自的支出数字：

```cpp
std::array<double, 4> expenses;
```

（回想一下，使用 `array` 类需要包含 array 头文件，并且名称 `array` 属于 `std` 命名空间。）如果我们希望函数显示 `expenses` 的内容，可以按值传递 `expenses`：

```cpp
show(expenses);
```

但如果我们希望函数修改 `expenses` 对象，就需要把该对象的地址传递给函数：

```cpp
fill(&expenses);
```

（下一章将讨论另一种方法，即使用引用。）这与程序清单 7.13 对结构采用的方法相同。

我们如何声明这两个函数呢？`expenses` 的类型是 `array<double, 4>`，因此函数原型中必须出现这种类型：

```cpp
void show(std::array<double, 4> da);   // da an object
void fill(std::array<double, 4> * pa); // pa a pointer to an object
```

这些考虑构成了示例程序的核心。该程序还增加了几个特性。首先，它用符号常量替换了 4：

```cpp
const int Seasons = 4;
```

其次，它增加了一个 `const` 数组对象，其中包含四个表示四季的 `string` 对象：

```cpp
const std::array<std::string, Seasons> Snames =
    {"Spring", "Summer", "Fall", "Winter"};
```

注意，`array` 模板并不限于保存基本数据类型；它也可以使用类类型。程序清单 7.15 完整给出了该程序。

**程序清单 7.15** `arrobj.cpp`

```cpp
//arrobj.cpp -- functions with array objects (C++11)
#include <iostream>
#include <array>
#include <string>
// constant data
const int Seasons = 4;
const std::array<std::string, Seasons> Snames =
    {"Spring", "Summer", "Fall", "Winter"};

// function to modify array object
void fill(std::array<double, Seasons> * pa);
// function that uses array object without modifying it
void show(std::array<double, Seasons> da);

int main()
{
    std::array<double, Seasons> expenses;
    fill(&expenses);
    show(expenses);
    return 0;
}

void fill(std::array<double, Seasons> * pa)
{
    using namespace std;
    for (int i = 0; i < Seasons; i++)
    {
        cout << "Enter " << Snames[i] << " expenses: ";
        cin >> (*pa)[i];
    }
}

void show(std::array<double, Seasons> da)
{
    using namespace std;
    double total = 0.0;
    cout << "\nEXPENSES\n";
    for (int i = 0; i < Seasons; i++)
    {
        cout << Snames[i] << ": $" << da[i] << endl;
        total += da[i];
    }
    cout << "Total Expenses: $" << total << endl;
}
```

下面是一次示例运行：

```text
Enter Spring expenses: 212
Enter Summer expenses: 256
Enter Fall expenses: 208
Enter Winter expenses: 244

EXPENSES
Spring: $212
Summer: $256
Fall: $208
Winter: $244
Total Expenses: $920
```

### 程序说明

因为 const 数组对象 `Snames` 声明在所有函数之前，所以它可以在后面的任何函数定义中使用。与 const 的 `Seasons` 一样，`Snames` 由整个源代码文件共享。该程序没有 using 指令，因此 `array` 和 `string` 必须与 `std::` 限定符一起使用。为了让程序保持简短并聚焦于函数如何使用对象，`fill()` 函数不检查输入是否有效。

`fill()` 和 `show()` 都有缺点。对于 `show()`，问题在于 `expenses` 保存四个 `double` 值，而创建同样大小的新对象并把 `expenses` 的值复制进去是低效的。如果我们修改程序，按月或按日处理支出并相应地扩展 `expenses`，这个问题会变得更严重。

`fill()` 函数通过使用指针避免了这种低效问题，使函数作用于原始对象。但这样做的代价是表示法让编程看起来更复杂。

```cpp
fill(&expenses);    // don't forget the &
...
cin >> (*pa)[i];
```

在最后一条语句中，`pa` 是指向 `array<double, 4>` 对象的指针，因此 `*pa` 是该对象，而 `(*pa)[i]` 是对象中的一个元素。由于运算符优先级，括号是必需的。逻辑很直接，但这增加了出错的机会。

使用引用（将在第 8 章讨论）有助于同时解决效率和表示法问题。

## 递归

现在来看一些完全不同的内容。C++ 函数有一个有趣的特点：它可以调用自身。（不过，与 C 不同，C++ 不允许 `main()` 调用自身！）这种能力称为递归。递归在某些类型的编程（例如人工智能）中是一种重要工具，但我们这里只对其工作原理做一次浅尝辄止的（人为的浅显）考察。

### 带单个递归调用的递归

如果一个递归函数调用自身，那么新被调用的函数又会调用自身，如此无限继续下去，除非代码中包含某种终止调用链的机制。通常的方法是把递归调用作为 `if` 语句的一部分。例如，一个名为 `recurs()` 的 void 递归函数可以具有如下形式：

```cpp
void recurs(argumentlist)
{
    statements1
    if (test)
        recurs(arguments)
    statements2
}
```

如果运气好或有先见之明，`test` 最终会变为 false，调用链就会中断。递归调用会产生一串引人入胜的事件。只要 `if` 语句保持为真，每次调用 `recurs()` 都会执行 `statements1`，然后调用一个新的 `recurs()` 实例，而不会到达 `statements2`。当 `if` 语句变为 false 时，当前调用才会继续执行 `statements2`。然后，当当前调用终止时，程序控制权返回到调用它的前一个 `recurs()` 版本。接着，那个版本的 `recurs()` 完成执行其 `statements2` 部分并终止，把控制权返回给更早的调用，依此类推。因此，如果 `recurs()` 经历五次递归调用，那么首先会按函数被调用的顺序执行 `statements1` 部分五次，然后按与函数被调用顺序相反的顺序执行 `statements2` 部分五次。进入五层递归后，程序必须再通过同样的五层退出。程序清单 7.16 演示了这一行为。

**程序清单 7.16   recur.cpp**

```cpp
// recur.cpp -- using recursion
#include <iostream>
void countdown(int n);

int main()
{
    countdown(4);             // call the recursive function
    return 0;
}

void countdown(int n)
{
    using namespace std;
    cout << "Counting down ... " << n << endl;
    if (n > 0)
```

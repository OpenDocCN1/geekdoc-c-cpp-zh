
# 第 10 章 运算符重载；string 类

对 `d2` 进行自增，以显示日期正确增加到 2 月 29 日。接下来，第 18 行创建一个日期对象 `d3`，并初始化为 2010 年 7 月 13 日。然后第 22 行使用重载的前置增量运算符将 `d3` 增 1。第 20–23 行在增量操作前后输出 `d3`，以确认该操作生效。最后，第 27 行使用重载的后置增量运算符对 `d3` 进行增量。第 25–28 行在后置操作前后输出 `d3`，以确认其运行正常。

### Date 类的前置运算符
重载增量运算符是非常简单的。使用前置增量运算符（定义在图 10.7 第 45–48 行）来增加日期。该函数处理了当我们增加月份最后一天时发生的“回绕”或“进位”，这需要增加月份。如果月份超过 12，则年份加 1，且月份必须设置为 1。`helpIncrement` 函数使用 `endOfMonth` 来判断是否已到达月末，并正确地增加日期。

重载的前置增量运算符返回当前 `Date` 对象的引用（即已增加的那个对象）。发生这种情况是因为当前对象 `*this` 是作为 `Date&` 返回的。这使得前置 `Date` 对象可以作为左值（lvalue）使用，这正是基本类型的内置前置增量运算符的工作原理。

### Date 类的后置运算符
重载后置增量运算符（定义在图 10.7 第 52–58 行）更为复杂。为了模拟后置的效果，我们必须返回 `Date` 对象的未修改的副本。例如，如果 `int x` 的值为 7，则语句

```
cout << x << endl;
```

会输出 `x` 的原始值。我们希望前置增量运算符在 `Date` 对象上也能以相同的方式工作。在 `operator++` 中，我们保存了当前 `Date` 对象（`*this`）。然后，第 57 行返回 `temp`——即原始 `Date` 对象的未修改副本。该函数不能返回局部 `Date` 对象 `temp` 的引用，因为局部变量在声明它的函数退出时会被销毁。因此，将返回类型为 `Date&` 将返回一个已不存在对象的引用。

# 10.9 动态内存管理

你可以控制程序中内置或用户定义类型对象及数组的内存分配和释放。这被称为动态内存管理，通过 `new` 和 `delete` 运算符实现。我们将在下一节中利用这些功能来实现我们的 `Array` 类。

- 你可以使用 `new` 运算符来分配（即在执行时分配一个对象或内置数组所需的内存）。该对象或内置数组创建在自由存储区（free store，也称为堆 heap）中——这是分配给每个程序用于存储动态分配对象的内存区域。内存也是

- 运算符可能无法获取所需的内存，在这种情况下会发生 `bad_alloc` 异常。第 17 章将展示如何处理 `new` 失败。

- 分配，你可以通过 `operator new` 返回的指针访问它。当你不再需要该内存时，可以使用 `delete` 运算符将其返回（即释放）自由存储区，该内存可以被未来的操作重用。

### 使用 new 获取动态内存

考虑以下语句：

```
Time* timePtr{new Time};
```

`new` 运算符为 `Time` 对象分配适当大小的存储空间，调用构造函数初始化对象，并返回一个指向 `new` 运算符右侧指定类型的指针（即 `Time*`）。在前述语句中，调用了 `Time` 类的默认构造函数，因为我们没有提供参数来初始化 `Time` 对象。如果 `new` 无法在内存中为对象找到足够的空间，它将通过抛出异常来指示错误。

### 使用 delete 释放动态内存

要销毁动态分配的对象并释放空间，请使用 `delete` 运算符：

```
delete timePtr;
```

该语句首先调用 `timePtr` 指向对象的析构函数，然后释放对象相关的内存，返回自由存储区。

常见编程错误 10.1
不再需要时未释放动态内存会导致系统内存耗尽。这有时被称为“内存泄漏”。

错误预防建议 10.1
删除动态内存后，务必将指针设置为 `nullptr`。

错误预防建议 10.2
删除 `nullptr` 没有影响。

### 初始化动态内存

你可以为新创建的提供初始化值，如

```cpp
double* ptr{new double{3.14}};
```

这初始化了 `double` 对象。相同的语法也可以为对象指定参数，如

```cpp
Time* timePtr{new Time{12}};
```

这初始化了 `Time` 对象并将其赋值给 `timePtr`。

### 使用 new 分配内置数组

你还可以使用 `new` 运算符分配内置数组。例如，10 个元素的数组可以这样分配并赋值给 `gradesArray`：

```cpp
int* gradesArray(new int[10]);
```

这声明了 `int gradesArray` 并将其指向分配的第一个元素。

### 使用 delete[] 释放内置数组

要删除 `gradesArray` 指向的内存，使用语句

```
delete[] gradesArray;
```

如果指针指向数组，该语句会调用数组中每个对象的析构函数，然后释放内存。如果前述语句没有方括号 `[]` 且 `gradesArray` 指向数组，结果是未定义的。

常见编程错误 10.2
对对象数组使用 `delete` 可能会导致运行时错误。确保数组中的每个对象都接收析构函数调用，始终使用 `delete[]` 释放数组内存。同样，始终使用 `delete` 释放作为单个元素的内存。

### C++11：使用 unique_ptr 管理动态内存

C++11 的 `unique_ptr` 是一种管理动态内存的“智能指针”。当 `unique_ptr` 超出范围时，它的析构函数会自动将管理的内存返回自由存储区。在第 17 章中，我们将引入 `unique_ptr` 并展示如何使用它管理动态分配的对象或内置数组。

# 10.10 案例研究：Array 类

我们在第 8 章讨论过内置数组。基于指针的数组有很多问题，包括：

- 程序很容易越内置数组的任意边界，因为 C++ 不检查下标是否超出了数组范围（尽管你可以显式地这样做）。
- 大小为 n 的内置数组元素编号必须为 0, ..., n–1；不允许交替下标范围。

## 10.10 案例研究：数组类

- 整个内置数组无法一次性输入或输出；每个元素必须逐个读取或写入（除非该数组是以空字符终止的 C 字符串）。
- 两个内置数组无法使用相等或关系运算符进行有意义的比较（因为数组名称仅仅是指向内存中数组起始位置的指针，两个数组始终位于不同的内存位置）。
- 当将内置数组传递给旨在处理任意大小数组的通用函数时，必须将数组的大小作为额外的参数传递。
- 一个内置数组不能通过赋值运算符赋值给另一个数组。

类的开发是一项有趣、富有创意且具有智挑战性的活动——目标是创建有价值的类。在 C++ 中，我们可以通过类和运算符重载来实现更健壮的数组，就像 C++ 标准库中模板和 vector 实现的那样。在本节中，我们将开发一种比内置数组更好的自定义数组类。当在本项研究中提到“数组”时，指的是内置数组。

在例例中，我们创建了一个强大的数组类，它执行范围检查以确保下标保持在 `Array` 的范围内。该类允许使用赋值运算符将一个 `Array` 对象赋值给另一个。`Array` 对象知道自己的大小，因此在分别使用流提取和插入运算符传递给函数 `Array input` 或 `output` 时，不需要单独传递大小。你可以使用相等运算符 `==` 和 `!=` 比较两个 `Arrays`。

作为一名新的 C++ 程序员，你可能会遇到使用 C++ 特性和技术的 C++ 遗留代码。尽管 C++ 编译器完全支持使用智能指针来简化动态内存管理，但我们显式地使用内置指针以及 `new` 和 `delete` 运算符来管理 `Array` 的动态内存，以帮助你理解、维护和修改你在工业界会看到的代码。

### 10.10.1 使用 Array 类

图 10.9–10.11 中的程序演示了我们的 `Array` 类以及使用的运算符。首先，我们查看 `main`（图 10.9）和程序的输出，然后考虑类的定义（图 10.10）以及它的每个成员函数定义（图 10.11）。

```cpp
// Fig 10.9: fig10_09.cpp
// Array 类测试程序。
#include <iostream>
#include <stdexcept>
#include "Array.h"
using namespace std;
int main() {
    Array integers1{7}; // 七个元素的 Array
    Array integers2[]; // 默认十个元素的 Array
    // 打印 integers1.size() 和内容
    cout << "Size of array integers1 is " << integers1.size()
    cout << "\nArray initialization: " << integers1;
}
```

图 10.9 | 数组类测试程序。（3 部分中的第部分）。

```cpp
// 打印 integers2 的大小和内容
cout << "\nsize of Array integers2 is " << integers2.getSize();
cout << "\nArray after initialization: " << integers2;
```

```cpp
// 输入并打印 integers1 和 integers2
cout << "\nEnter 7 integers:" << endl;
cin >> integers1 >> integers2;
```

```cpp
cout << "\nafter input, the Arrays containing:\n";
out << "-integers1: " << integers1;
cout << "-integers2: " << integers2;
```

```cpp
// 使用重载的不等运算符 (!=)
cout << "\nevaluating: integers1 != integers2" << endl;
if (integers1 != integers2) {
    cout << "integers1 and integers2 are not equal" << endl;
}
```

```cpp
// 使用 integers1 作为初始化器创建 Array3；
// 打印大小和内容
Array Array3[integers1]; // 调用拷贝构造函数
```

```cpp
cout << "\nsize of Array integers3 is " << integers3.getSize();
cout << "\nArray after initialization: " << integers3;
```

```cpp
// 使用重载的赋值运算符 (=)
cout << "\nassigning integers2 to integers1:" << endl;
integers1 = integers2; // 目标 Array 小
```

```cpp
cout << "integers1: " << integers1 << " " << integers2;
```

```cpp
// 使用重载的相等运算符 (==)
cout << "\nevaluating: integers1 == integers2" << endl;
if (integers1 == integers2) {
    cout << "integers1 and integers2 are equal" << endl;
}
```

```cpp
// 使用重载的下标运算符创建右值
cout << "\nintegers1[5] is " << integers1[5];
cout << "\nassigning 1000 to integers1[5]" << endl;
integers1[5] = 1000;
cout << "integers1: " << integers1;
```

```cpp
// 尝试越界下标
try {
    cout << "\nattempt to assign 1000 to integers1[15]" << endl;
    integers1[15] = 1000; // 错误：下标越界
}
```

图 10.9 | 数组类测试程序。（3 部分中的第2 部分）。

```cpp
catch (out_of_range& ex) {
    cout << "An exception occurred: " << ex.size() << endl;
}
```

Size of Array integers1 is 7
Array after initialization: 0 0 0 0 0 0 0
Size of Array integers2 is 10
Array after initialization: 0 0 0 0 0 0 0 0 0 0
Enter 17 integers:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17
After input, the Arrays contain:
integers1: 1 2 3 4 5 6 7
integers2: 8 9 10 11 12 13 14 15 16 17
Evaluating: integers1 != integers2
integers1 and integers2 are not equal
Size of Array integers3 is 7
Array after initialization: 1 2 3 4 5 6 7
Assigning integers2 to integers1:
integers1: 8 9 10 11 12 13 14 15 16 17
integers2: 8 9 10 11 12 13 14 15 16 17
Evaluating: integers1 == integers2
integers1 and integers2 are equal
integers1[5] is 13
Assigning 1000 to integers1[5]
integers1: 8 9 10 11 12 1000 14 15 16 17
Exception occurred: Subscript out of range

图 10.9 | 数组类测试程序。（3 部分中的第3 部分）。

**创建数组、输出大小并显示内容** 程序通过实例化两个 `Array` 类对象开始——`integers1`（图 10.9，第 9 行）带有元素，而 `integers2`（第 10 行）具有默认数组大小——10（由图 10.10 第 13 行中 `Array` 默认构造函数的原型指定）。图 10.9 中的 13–14 行使用成员函数 `getSize` 确定 `integers1` 的大小，然后使用 `Array` 插入运算符输出 `integers1` 的内容。示例输出确认了 `Array` 元素被构造函数正确设置为零。接下来，第 17–18 行显示 `integers2` 的大小，然后使用 `Array` 插入运算符输出 `integers2` 的内容。

**使用重载的流提取运算符填充数组** 第 21 行提示用户输入 17 个整数。第 22 行使用 `Array` 流提取运算符将前七个值读入 `integers1`，将剩余十个值读入 `integers2`。第 24–26 行使用重载的 `Array` 插入运算符输出两个数组，以确认输入正确。

**使用重载的不等运算符** 第 31 行通过评估条件测试重载的不等运算符：

```
integers1 != integers2
```

程序输出显示 `Arrays` 不相等。

**使用现有数组内容的拷贝初始化新数组** 第 37 行实例化了名为 `integers3` 的第三个 `Array`，并用 `Array integers1` 的拷贝初始化。这调用了 `Array` 拷贝构造函数将 `integers1` 的元素拷贝到 `integers3` 中。我们将讨论拷贝构造函数的细节。可以通过将第 37 行写如下如下调用拷贝构造函数：

```cpp
Array integers3 = integers1;
```

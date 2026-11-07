
泄漏的内存包含管理其他资源的对象时，这些对象的析构函数将不会被调用以释放资源，从而导致额外的泄漏。

不要删除不是由 `new` 分配的内存。这样做会导致**未定义行为**。删除动态分配的内存后，务必不要再次删除同一内存，因为这通常会导致程序崩溃。防止这种情况的一种方法是立即将指针设置为 `nullptr`——删除这样的指针没有效果。

## 初始化动态分配的对象

可以使用构造函数参数初始化新分配的对象，如下所示：

```
Time* timePtr{new Time{12, 45, 0}};
```

这将一个新的 Time 对象初始化为 12:45:00 PM，并将其指针赋给 timePtr。

## 使用 new[] 动态分配内置数组

还可以使用 new 运算符动态分配内置数组。以下语句动态分配一个包含 10 个元素的 int 内置数组：

```
int* gradesArray{new int[10]};
```

该语句将 int 指针 gradesArray 指向动态分配数组的第一个元素。`new int[10]` 后面的空花括号初始化器会对数组元素进行值初始化，这会将基本类型元素设置为 0，将 bool 设置为 false，将指针设置为 nullptr。花括号初始化器还可以包含用逗号分隔的数组元素初始化器列表。对对象进行值初始化会调用其默认构造函数（如果可用）。对于没有默认构造函数的对象，规则会变得更复杂。有关更多详细信息，请参阅以下网址中的值初始化规则：

```
https://en.cppreference.com/w/cpp/language/value_initialization
```

编译时创建的内置数组的大小必须使用整型常量表达式指定。然而，动态分配数组的大小可以使用任何非负整型表达式指定。

## 使用 delete[] 释放动态分配的内置数组

要释放 gradesArray 所指向的内存，请使用以下语句：

```
delete[] gradesArray;
```

如果该指针指向一个对象内置数组，此语句会先调用数组中每个对象的析构函数，然后释放整个数组的内存。与 delete 一样，对 nullptr 使用 `delete[]` 没有效果。

**对使用 new[] 分配的数组使用 delete 而不是 delete[] 会导致未定义行为。** 某些编译器只会调用数组中第一个对象的析构函数。为确保数组中的每个对象都收到析构函数调用，**始终使用 delete[] 删除由 new[] 分配的内存。** 我们将展示更好的动态分配内存管理技术，使你能够避免使用 new 和 delete。

如果只有一个指针指向一块动态分配的内存，而该指针离开了作用域，或者你将其赋值为 nullptr 或不同的内存地址，就会发生**内存泄漏。**

删除动态分配的内存后，将指针的值设置为 `nullptr`，以表明它不再指向自由存储区中的内存。这确保你的代码不会无意中访问先前分配的内存——这样做可能会导致微妙的逻辑错误。

## 基于范围的 `for` 不适用于动态分配的内置数组

你可能想使用基于范围的 for 语句来遍历动态分配的数组。不幸的是，这无法编译。要使用基于范围的 for 遍历数组，编译器必须在编译时知道元素数量。作为一种变通方法，你可以创建一个 C++20 span 对象，表示动态分配的数组及其元素数量，然后使用基于范围的 for 遍历该 span 对象。

### 检查点

- 1. **（填空）** 删除动态分配的内存后，务必不要再次删除同一内存，因为这通常会导致程序崩溃。防止这种情况的一种方法是立即将指针设置为 `nullptr`——删除这样的指针没有效果。  
  **答案：** `nullptr`。

- 2. **（讨论）** 不能使用基于范围的 `for` 语句遍历动态分配的数组，因为编译器必须在编译时知道元素数量。动态分配数组的大小是在执行时确定的。请描述一种解决此问题的变通方法。  
  **答案：** 创建一个表示动态分配数组及其元素数量的 C++20 span，然后使用基于范围的 `for` 遍历该 span。

- 3. **（代码）** 编写一条语句，动态分配一个 `std::string` 对象，通过调用默认构造函数初始化它，并返回指向新对象的指针。  
  **答案：** `std::string* stringPtr{new std::string{}};`

## 11.5 现代 C++ 动态内存管理：RAII 与智能指针

一种常见的设计模式是

- 分配动态内存，
- 将该内存的地址赋给一个指针，
- 使用该指针操作内存，以及
- 在不再需要时释放该内存。

如果在内存分配成功之后、但在 `delete` 或 `delete[]` 语句执行之前发生异常，就可能发生内存泄漏。因此，C++ Core Guidelines 建议使用 RAII（Resource Acquisition Is Initialization，资源获取即初始化）来管理动态内存等资源。⁸,⁹ 这个概念很直接。对于程序使用完毕后必须归还给系统的任何资源，程序应该

- 在函数中将对象创建为局部变量——对象的构造函数应在初始化对象时获取资源，
- 在程序中按需使用该对象，然后
- 当函数调用终止时，对象离开作用域——对象的析构函数应释放资源。

8. C++ Core Guidelines，“R：资源管理”。访问于 2023 年 4 月 18 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#R-resource。

9. C++ Core Guidelines，“R.1：使用资源句柄和 RAII（资源获取即初始化）自动管理资源”。访问于 2023 年 4 月 18 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#R-rami。

### 11.5.1 智能指针

智能指针使用 RAII 为你管理动态分配的内存。标准库头文件 `<memory>` 定义了三种智能指针类型：

- `unique_ptr`
- `shared_ptr`
- `weak_ptr`

一个 **unique_ptr** 维护一个指向动态分配内存的指针，该内存一次只能属于一个 **unique_ptr**。当 **unique_ptr** 对象离开作用域时，其析构函数使用 `delete` 或 `delete[]` 释放该 unique_ptr 管理的内存。11.5 节的其余部分将演示 unique_ptr，我们也会在 MyArray 案例研究中使用它。我们将在第 20 章“其他主题与 C++ 未来展望”中介绍 shared_ptr 和 weak_ptr。

### 11.5.2 演示 unique_ptr

图 11.2 演示了一个 unique_ptr 指向类 Integer 的动态分配对象（第 7–22 行）。出于教学目的，该类的构造函数和析构函数在被调用时都会显示信息。第 29 行创建一个 unique_ptr 对象 ptr，并用一个指向包含值 7 的动态分配 Integer 对象的指针来初始化它。为了初始化该 unique_ptr，第 29 行调用 make_unique 函数模板，该模板使用 new 分配动态内存，然后返回指向该内存的 unique_ptr。在此示例中，make_unique<Integer> 返回一个 unique_ptr<Integer>——第 29 行使用 auto 关键字从初始化器推断 ptr 的类型。

```cpp
// Fig11_02.cpp
// Demonstrating unique_ptr.
#include <format>
#include <iostream>
#include <memory>

class Integer {
public:
   // constructor
   Integer(int i) : value{i} {
      std::cout << std::format("Constructor for Integer {}\n", value);
   }

   // destructor
   ~Integer() {
       std::cout << std::format("Destructor for Integer {}\n", value);
   }

   int getValue() const {return value;} // return Integer value
private:
   int value{};
};

// use unique_ptr to manipulate Integer object
int main() {
   std::cout << "Creating a unique_ptr that points to an Integer\n";

   // create a unique_ptr object and "aim" it at a new Integer object
   auto ptr{std::make_unique<Integer>(7)};

   // use unique_ptr to call an Integer member function
   std::cout << std::format("Integer value: {}\n\nMain ends\n",
       ptr->getValue());
}
```

**图 11.2** | 演示 `unique_ptr`。（第 1 部分，共 2 部分。）

**图 11.2** | 演示 `unique_ptr`。（第 2 部分，共 2 部分。）

```text
Creating a unique_ptr that points to an Integer
Constructor for Integer 7
Integer value: 7

Main ends
Destructor for Integer 7
```

第 33 行使用 unique_ptr 类的重载 -> 运算符，对 ptr 管理的 Integer 对象调用 getValue。表达式 ptr->getValue() 也可以写成

```cpp
(*ptr).getValue()
```

它使用 unique_ptr 重载的 * 运算符解引用 ptr，然后使用点（.）运算符对 Integer 对象调用 getValue。

由于 ptr 是 main 中的局部变量，因此当 main 终止时它会被销毁。unique_ptr 的析构函数会删除动态分配的 Integer 对象，这会调用 Integer 对象的析构函数。无论程序控制是通过 return 语句正常离开该块、到达该块末尾，还是由于异常而离开，程序都会释放该 Integer 对象的内存。

最重要的是，使用 unique_ptr 可以防止资源泄漏。例如，假设一个函数返回一个指向某个动态分配对象的指针。不幸的是，接收到该指针的函数调用者可能不会删除该对象，从而导致内存泄漏。然而，如果函数返回指向该对象的 unique_ptr，那么当 unique_ptr 对象的析构函数被调用时，该对象将被自动删除。

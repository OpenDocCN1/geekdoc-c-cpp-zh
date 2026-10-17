
程序 11.6 的结果所示：

Biscuit Information
Biscuit Name: SweetBest
Biscuit Price: 7.5
Biscuit Manufacturer: Qingdao Biscuits
Biscuit Item Number: 341

Biscuit Information (using pointer)
Biscuit Name: SweetBest
Biscuit Price: 7.5
Biscuit Manufacturer: Qingdao Biscuits
Biscuit Item Number: 341

## 11.10 结构体与函数

结构体可以像其他类型一样与函数配合使用。通常，函数使用结构体作为参数，结构体可以整体或地址的形式发送到函数。我们可以像传递其他变量或指针一样将结构体作为函数参数。我们可以以本章之前示例的方法访问结构体变量。在程序 11.7 中，结构体作为参数传递的。

```cpp
// Program 11.7
// Functions using structures
#include <iostream>
using namespace std;
struct item {
    char item_name[10];
    float price;
    char manufacturer[40];
    int item_no;
};
// 函数接受结构体作为参数
void printItem(struct item Temp) {
    cout << "Biscuit Name: " << Temp.item_name << endl;
    cout << "Biscuit Price: " << Temp.price << endl;
    cout << "Biscuit Manufacturer: " << Temp.manufacturer << endl;
    cout << "Biscuit Item Number: " << Temp.item_no << endl;
}
int main() {
    // 结构体的声明和初始化
    struct item Biscuit = {"SweetBest", 7.5, "Qingdao Biscuits", 341};
    // 将结构体作为参数传递
    printItem(Biscuit);
    return 0;
}
```

程序 11.7 的结果：

Biscuit Name: SweetBest
Biscuit Price: 7.5
Biscuit Manufacturer: Qingdao Biscuits
Biscuit Item Number: 341

如程序 11.7 所示，结构体 `Biscuit` 作为参数传递给函数 `printItem()`。在函数 `printItem(item)` 中，`temp` 是一个类型匹配的 `struct item` 形式参数。注意的是，在 `main` 或函数中引用它之前，应该先声明 `struct item`。程序 11.8 展示了另一个与函数使用结构体的类似示例（指针除外）。在这个示例中，结构体的地址作为参数传递给函数 `printItem()`。由于结构体地址作为参数传递的，函数接受指向结构体的指针作为形式参数。如程序 11.6 所示，我们可以使用 `->` 运算符显示结构体成员的值。

```cpp
// Program 11.8
// Function accepting pointer to structure
#include <iostream>
using namespace std;
struct item {
    char item_name[10];
    float price;
    char manufacturer[40];
    int item_no;
};
// 函数接受结构体指针作为参数
void printItem(struct item *ptrItem) {
    cout << "Biscuit Name: " << ptrItem->item_name << endl;
    cout << "Biscuit Price: " << ptrItem->price << endl;
    cout << "Biscuit Manufacturer: " << ptrItem->manufacturer << endl;
    cout << "Biscuit Item Number: " << ptrItem->item_no << endl;
}
int main() {
    struct item Biscuit = {"SweetBest", 7.5, "Qingdao Biscuits", 341};
    struct item *ptrBiscuit;
    ptrBiscuit = &Biscuit;
    printItem(ptrBiscuit);
    return 0;
}
```

## 11.11 联合 (Unions)

联合（Unions）和结构体（structures）非常相似，区别在于联合体使用单个内存位置来存储多个变量。联合体是一种用户定义的变量，可以包含不同大小和类型的成员。让我们考虑一些联合体比结构体更优的情况。

- 1. 一个拥有两个变量的程序（例如两个不同类型的 `var1` 和 `var2`）可能在一段时间内使用 `var1`，当其不再被需要时，可以将 `var1` 的相同内存位置分配给 `var2`。
- 2. 有时，无法确定应该向函数传递什么类型的数据。在这些情况下，我们可以传递一个包含所有可能数据类型的联合。

因此，联合体是一种定义类型，其中所有成员共享同一个内存位置，在任何时刻，联合体只能包含其成员列表中的一个对象。这意味着无论联合体有多少个成员，它始终使用足够的内存来存储最大的成员。当我们有大量对象和/或内存有限时，联合体有助于节省内存。然而，这需要额外小心以确保我们始终访问最后写入的成员。声明联合体的语法与结构体相似；唯一的例外是使用关键字 `union` 代替 `struct`。联合体标签（Union-tag）是赋予联合体及其成员定义的统称。联合体声明的一般格式如下：

```cpp
union [union-tag]
{
  member definition;
  member definition;
  ...
  member definition;
} [one or more union variables];
```

以下示例定义了一个联合体 `tempNum` 和一个名为 `intDouble` 的变量。在这里，`tempNum` 是变量名，它的作用与结构体的标签相同。联合体成员的访问方式与结构体成员的方式相同。

```cpp
union tempNum
{
  int number;
  double floatnumber;
} intDouble;
```

由于联合体为单个成员变量分配内存，分配总是根据需要最大内存的变量进行的。在上一个示例中，由于 `floatnumber` 需要的内存比 `number` 多，因此内存分配是针对存储 `double` 的空间。程序 11.9 总结了联合体和结构体之间的区别，并演示了在 C++ 中使用联合体。

```cpp
// Program 11.9
// 理解联合体和结构体
#include <iostream>
using namespace std;
int main() {
    union tempNum1 {
        int number1;
        double floatnumber1;
    }; struct tempNum2 {
        int number2;
        double floatnumber2;
    };
    union tempNum1 TN1 = {3.0,14};
    cout << "Size of union TN1 = " << sizeof(TN1) << endl;
    cout << "Size of structure TN2 = " << sizeof(TN2) << endl;
    cout << "Union member floatnumber1 = " << TN1.floatnumber1 << endl;
    cout << "Structure member number1 = " << TN2.number2 << endl;
    cout << "Structure member floatnumber1 = " << TN2.floatnumber2 << endl;
    return 0;
}
```

程序 11.9 的结果如下：

```
Size of union TN1 = 8
Size of structure TN2 = 16
Union member number1 = 3
Union member floatnumber1 = 1.4822e-323
Structure member number1 = 24
Structure member floatnumber1 = 3.14
```

在程序 11.9 中，有一个结构体和一个联合体，两者的数据成员数量和类型均相同。最初，程序使用 `sizeof()` 运算符找到为联合体和结构体分配的内存地址长度。结果所示，联合体只分配了 8 字节，而结构体分配了 16 字节。由于联合体一次只能存储一个值，因此无法同时初始化它的所有成员。因此，联合体只初始化了一个成员。另一方面，我们可以同时初始化结构体的所有成员。联合体用浮点数初始化；因为我们先显示整数值，所以浮点数对应的整数值被显示。然而，如果我们尝试打印存储在相同内存位置的值，就会显示一个奇怪的值。联合体也可以作为结构体的成员。程序 11.10 展示了将双成员联合体作为结构体成员的示例。

```cpp
// Program 11.10
// 作为结构体成员的联合体
#include <iostream>
#include <cstring>
using namespace std;
int main()
{
    union id
    {
        char name[40];
        int number;
    };
    struct {
        float salary;
        union id description;
    } employee;
    strcpy(employee.description.name, "Jessica");
    cout << "Employee Name : " << employee.description.name << endl;
    employee.description.number = 1729;
    cout << "Employee Number : " << employee.description.number << endl;
    employee.description.salary = 18700.25;
    cout << "Employee Salary : " << employee.description.salary << endl;
    return 0;
}
```

程序 11.10 的结果如下：

```
Employee Name : Jessica
Employee Number : 1729
Employee Salary : 18700.25
```

*(注：原文后续存在大量重复的段落，已按要求去重处理)*

# 12 处理 (Handling)

## 12.1 引言

异常处理（Exception handling）是 C++ 最有用的功能之一。程序在执行时可能会遇到问题，例如运行时错误。这些问题可能在编码期间在程序员不知情的情况下发生，并中断执行的正常流程。程序可以在没有任何错误的情况下通过编译，但执行可能会在某些代码段停止，不再继续执行。这些问题被称为异常。异常是程序运行时发生的问题或错误。这些问题不在程序的控制范围内。在这些情况下，异常提供了特殊的函数——处理程序（handlers），作为应对异常情况的方法。C++ 提供了强大的机制来处理这些异常。本章关注异常处理方法以理解异常的重要性。例如，让我们考虑程序 12.1。

```cpp
// Program 12.1
// 没有异常机制的程序
#include<iostream>
using namespace std;
int main()
{
    int a = 1,b = 0;
    cout << a/b << endl;
    return 0;
}
```

```cpp
#include<iostream>
using namespace std;
int main()
{
    int a, b;
    cout << "Enter two integers for division" << endl;
    cin >> a >> b;
    try
    {
        if(b == 0)
            throw "There is an exception";
        else
            cout << a << " divided by " << b << " = " << endl;
    } catch (const char* msg) {
        cout << msg << endl;
    }
    return 0;
}
```

在程序12.2中，如果我们输入非零整数作为输入，程序将无任何问题地输出。考虑这些结果：

情况 1：

```
Enter two integers for division
4 2
4 divided by 2 = 2
```

情况 2：

```
Enter two integers for division
4 8
4 divided by 8 = 0
```

在两种情况下，结果都是预期的整数除法。因为4 和 8 都是整数，在整数除法中，结果截断为 0。然而，在同一个程序中，如果我们输入 a 为非零且 b 为零，结果将如程序12.1所示。在这些情况下，我们使用C++的异常语句来避免 b 意外变为零。程序12.3显示了使用C++异常机制的方法。这里修改了使得**除以零**的问题可以被处理。

```cpp
// 程序 12.3
// 带有异常机制的程序
#include<iostream>
using namespace std;
int main()
{
    int a, b;
    cout << "Enter two integers for division" << endl;
    cin >> a >> b;
    try{
        if(b == 0)
            throw "There is an exception";
        else
            cout << a << " divided by " << b << " = " << a/b << endl;
    } catch (const char* msg) {
        cout << msg << endl;
    }
    return 0;
}
```

程序12.3的示例结果如下：

情况 1：

Enter two integers for division
18 2
18 divided by 2 = 9

情况 2：

Enter two integers for division
0 1
0 divided by 1 = 0

情况 3：

Enter two integers for division
0 0
There is an exception

情况 4：

Enter two integers for division
2 0
There is an exception

因此，从上一个例子可以看出，正常的执行流可能会停止，或者产生异常。如程序12.3所示，`try`、`catch`和`throw`等几个关键字用于处理“除以零”异常。在下一节中，我们将学习如何使用C++异常机制来处理异常。

## 12.2 处理异常

异常机制的目标是提供检测和报告“异常情况”的方法，以便在正确的时间采取行动。通常，异常机制处理这些任务：(a) 找到可能异常的问题(b) 通知错误的错误或抛出异常，(c) 接收错误信息或捕获异常，最后 (d) 采取纠正措施或处理异常。当块中出现异常情况时，会抛出一个异常并将控制转移到异常处理器。如果没有抛出异常，代码将继续执行，所有处理器都被忽略。在 `try` 块内部使用 `throw` 关键字抛出异常。异常处理器用 `catch` 关键字声明，必须放置在 `try` 块之后。因此，在C++中，异常机制通过三个关键字处理，即 `try`、`catch`和`throw`。下面是这三者的简要细节。

- `try:` 块中包含了可能产生异常的程序或代码部分，后面跟着 `catch` 块。该块由括号 `{}` 包围。当块内产生异常时，异常会被抛出，控制转移到异常处理器。如果没有抛出异常，程序继续正常执行，所有处理器都 true忽略。
- `catch:` `catch` 关键字的作用是捕获异常，其中 `catch` 参数的数据类型与异常类型匹配。`catch` 块必须放置在 `try` 块之后。当捕获到异常时，执行 `catch` 块中的代码。`catch` 块捕获由 `try` 块中的 `throw` 语句“抛出”的异常。
- `throw:` 前述，程序在异常情况下抛出异常。异常通过 `throw` 关键字抛出，可以在代码的任何地方抛出。异常类型也由 `throw` 语句决定。C++ 处理异常的通用格式所示：

```cpp
try {
    // 可能抛出异常的语句
}
```

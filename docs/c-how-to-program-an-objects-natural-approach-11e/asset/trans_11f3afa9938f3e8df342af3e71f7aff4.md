

```cpp
21  // destructor decrements the count
22  Employee::~Employee() {
23      std::cout << std::format("~Employee() called for {} {}\n",
24          m_firstName, m_lastName);
25      --m_count; // decrement static count of employees
26  }
27
28  // return first name of employee
29  const string& Employee::getFirstName() const {return m_firstName;}
30
31  // return last name of employee
32  const string& Employee::getLastName() const {return m_lastName;}
```

**图 9.34** | Employee 类成员函数定义。（第 2 部分，共 2 部分。）

图 9.35 使用静态成员函数 getCount 来确定程序中不同位置内存中 Employee 对象的数量。该程序调用 Employee::getCount()：

- 在创建任何 Employee 对象之前（第 11 行），
- 在创建两个 Employee 对象之后（第 23 行），以及
- 在这些 Employee 对象被销毁之后（第 34 行）。

当 Employee 对象在作用域内时，你也可以在这些对象上调用 getCount。例如，在第 23 行，我们可以写成 e1.getCount() 或 e2.getCount()。两者都会返回类 Employee 的静态 m_count 的当前值。

```cpp
1   // Fig09_35.cpp
2   // static data member tracking the number of objects of a class.
3   #include <format>
4   #include <iostream>
5   #include "Employee.h" // Employee class definition
6
7   int main() {
8       // no objects exist; use class name and scope resolution
9       // operator to access static member function getCount
10      std::cout << std::format("Initial employee count: {}\n",
11          Employee::getCount()); // use class name
12
13      // the following scope creates and destroys
14      // Employee objects before main terminates
15      {
16          const Employee e1{"Alma", "Rusu"};
17          const Employee e2{"Grilo", "Perez"};
18
19          // two objects exist; call static member function getCount again
20          // using the class name and the scope resolution operator
21          std::cout << std::format(
22              "Employee count after creating objects: {}\n\n",
23              Employee::getCount());
```

**图 9.35** | 跟踪类对象数量的静态数据成员。（第 1 部分，共 2 部分。）

```cpp
std::cout << std::format("Employee 1: {} {}\nEmployee 2: {} {}\n",
    e1.getFirstName(), e1.getLastName(),
    e2.getFirstName(), e2.getLastName());
}

// no objects exist, so call static member function getCount again
// using the class name and the scope resolution operator
std::cout << std::format(
    "Employee count after objects are destroyed: {}\n",
    Employee::getCount());
}
```

```text
Initial employee count: 0
Employee constructor called for Alma Rusu
Employee constructor called for Grilo Perez
Employee count after creating objects: 2

Employee 1: Alma Rusu
Employee 2: Grilo Perez

~Employee() called for Grilo Perez
~Employee() called for Alma Rusu
Employee count after objects are destroyed: 0
```

**图 9.35** | 跟踪类对象数量的静态数据成员。（第 2 部分，共 2 部分。）

main 中的第 15–28 行定义了一个嵌套作用域。回想一下，局部变量会一直存在，直到定义它们的作用域终止。在这个例子中，我们在嵌套作用域中创建了两个 Employee 对象（第 16–17 行）。每个构造函数执行时，都会递增类 Employee 的静态数据成员 m_count。当程序执行到第 28 行时，这些 Employee 对象被销毁。此时，每个对象的析构函数执行，并递减类 Employee 的静态数据成员 m_count。

### 静态成员函数说明

如果成员函数不访问类的非静态数据成员或非静态成员函数，则应将其声明为 static。**静态成员函数没有 this 指针，因为静态数据成员和静态成员函数独立于类的任何对象而存在。** this 指针必须指向特定对象，但当内存中没有其类的对象时，也可以调用静态成员函数。因此，在静态成员函数中使用 this 指针会导致编译错误。

静态成员函数不能被声明为 const。const 限定符作用于 this 指针所指向的对象，并表明函数不能修改该对象的内容。然而，静态成员函数独立于类的任何对象而存在和操作，因此将静态成员函数声明为 const 会导致编译错误。

### 检查点

1. **（填空）** 类的静态成员即使在该类没有对象存在时也仍然存在。要访问公有静态类数据成员或成员函数，只需在成员名前加上类名和 ________。
   **答案：** 作用域解析运算符（::）

2. **（讨论）** 解释当类没有对象存在时，如何访问私有静态或受保护静态数据成员。
   **答案：** 提供一个公有静态成员函数，并通过在函数名前加上类名和作用域解析运算符来调用该函数。

3. **（讨论）** 解释为什么静态成员函数没有 this 指针。
   **答案：** 这是因为静态数据成员和静态成员函数独立于类的任何对象而存在。this 指针必须指向特定对象，但当内存中没有其类的对象时，也可以调用静态成员函数。因此，在静态成员函数中使用 this 指针会导致编译错误。

## 9.21 C++20 中的聚合

C++ 标准文档 http://wg21.link/n4861 的第 9.4.1 节将聚合类型描述为内置数组、数组对象或满足以下条件的类对象：

- 没有用户声明的构造函数，
- 没有私有或受保护（第 10 章）的非静态数据成员，
- 没有虚函数（第 10 章），以及
- 没有私有（第 10 章）、受保护（第 10 章）或虚（第 10 章）基类。

你可以使用所有数据均为公有的类来定义聚合。然而，**struct 是一种默认只包含公有成员的类。** 下面的 struct 定义了一个名为 Record 的聚合类型，其中包含四个公有数据成员：

```cpp
struct Record {
    int account;
    string first;
    string last;
    double balance{0.0};
};
```

CG ⦿ 如果任何数据成员或成员函数需要为非公有，C++ Core Guidelines 建议使用 class 而不是 struct。³⁵

### ✓ 检查点

1. *（代码）* 定义一个名为 Point 的聚合类型，其中包含名为 x 和 y 的公有 int 数据成员。

   **答案：**

   ```cpp
   struct Point {
       int x;
       int y;
   };
   ```

2. *（判断正误）* 如果任何数据成员或成员函数需要为非公有，C++ Core Guidelines 建议使用 struct 而不是 class。

   **答案：** 错误。实际上，如果任何数据成员或成员函数需要为非公有，C++ Core Guidelines 建议使用 class 而不是 struct。

### 9.21.1 初始化聚合

可以按如下方式初始化聚合类型 Record（上文）的对象：

```cpp
Record record{100, "Abilio", "Sain", 123.45};
```

如果你用比对象中数据成员数量更少的初始化器来初始化聚合类型对象，例如

```cpp
Record record{0, "Abilio", "Sain"};
```

其余数据成员按如下方式初始化：

- 带有类内初始化器的数据成员使用这些值——在前面的例子中，record 的 balance 被设置为 0.0。
- 没有类内初始化器的数据成员用空花括号（{}）初始化。空花括号初始化将基本类型变量设置为 0，将 bool 设置为 false，并对对象进行值初始化。

### ✓ 检查点

1. *（代码）* 使用你之前创建的聚合类型 Point 创建一个 Point 对象，并将其 x 和 y 数据成员初始化为 10。

   **答案：** `Point point{10, 10};`

2. *（讨论）* 解释如果用比对象中数据成员数量更少的初始化器来初始化聚合类型对象会发生什么。

   **答案：** 其余数据成员如果有类内初始化器，则用这些初始化器初始化。否则，它们用空花括号（{}）初始化，将基本类型变量设置为 0，将 bool 设置为 false，并对对象进行值初始化。

### 9.21.2 C++20 指定初始化器

从 C++20 开始，聚合现在支持指定初始化器，你可以在其中按名称指定要初始化哪些数据成员。使用第 9.21 节开头的 struct Record 定义，我们可以按如下方式初始化 Record 对象：

```cpp
Record record{.first{"Cour"}, .last{"Malonga"}};
```


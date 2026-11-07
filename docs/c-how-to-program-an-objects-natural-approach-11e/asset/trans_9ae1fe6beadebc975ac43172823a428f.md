
```cpp
63  // return Time as string in 12-hour format (HH:MM:SS AM or PM)
64  std::string Time::to12HourString() const {
65      return std::format("{:}:{:02d}:{:02d} {}",
66          (getHour() % 12 == 0) ? 12 : getHour() % 12,
67          getMinute(), getSecond(), (getHour() < 12 ? "AM" : "PM"));
68  }
```

**图 9.31** | 经修改以支持级联成员函数调用的 Time 类成员函数定义。（第 3 部分，共 3 部分。）

在图 9.32 中，我们创建 Time 对象 `t`（第 9 行），然后在级联成员函数调用中使用它（第 11 行和第 19 行）。

```cpp
1  // fig09_32.cpp
2  // Cascading member-function calls with this pointer.
3  #include <format>
4  #include <iostream>
5  #include "Time.h" // Time class definition
6  using namespace std;
7
8  int main() {
9      Time t{}; // create Time object
10
11     t.setHour(18).setMinute(30).setSecond(22); // cascaded function calls
12
13     // output time in 24-hour and 12-hour formats
14     std::cout << std::format("24-hour time: {}\n12-hour time: {}\n",
15         t.to24HourString(), t.to12HourString());
16
17     // cascaded function calls
18     std::cout << std::format("New 12-hour time: {}\n",
19         t.setTime(20, 20, 20).to12HourString());
20 }
```

```text
24-hour time: 18:30:22
12-hour time: 6:30:22 PM
New 12-hour time: 8:20:20 PM
```

**图 9.32** | 使用 `this` 指针进行级联成员函数调用。

为什么将 `*this` 作为引用返回的技术有效？点运算符（`.`）从左到右分组，因此第 11 行

```cpp
t.setHour(18).setMinute(30).setSecond(22);
```

首先对 `t.setHour(18)` 求值，它返回对（已更新的）对象 `t` 的引用，作为此函数调用的值。然后剩余表达式被解释为

```cpp
t.setMinute(30).setSecond(22);
```

`t.setMinute(30)` 调用执行并返回对（进一步更新后的）对象 `t` 的引用。剩余表达式被解释为

```cpp
t.setSecond(22);
```

第 19 行（图 9.32）也使用了级联。我们不能在 `to12HourString` 之后继续链式调用另一个 Time 成员函数，因为它不返回 `Time&`。不过，我们可以链式调用一个字符串成员函数，因为 `to12HourString` 返回一个字符串。第 11 章给出了级联函数调用的实际示例，例如在使用 `<<` 运算符的 `cout` 语句中，以及在使用 `>>` 运算符的 `cin` 语句中。

## 检查点

- 1. *（代码）* 假设类 `Time` 包含数据成员 `m_totalSeconds`。给出两个表达式，可用于在成员函数内通过 `this` 指针访问 `m_totalSeconds`。  
  **答案：** `this->m_totalSeconds`  
  `(*this).m_totalSeconds`
- 2. *（判断题）* `this` 指针的另一个用途是支持级联成员函数调用——即在同一语句中依次调用多个函数。  
  **答案：** 正确。
- 3. *（讨论）* 通过解释下面这行代码如何工作，说明为什么将 `*this` 作为引用返回的技术有效：  
  `t.setHour(11).to12HourString();`  
  **答案：** 点运算符（`.`）从左到右分组，因此前一条语句首先调用 `setHour` 将 `t` 的小时设置为 11。表达式 `t.setHour(11)` 返回对已更新对象 `t` 的引用，随后该语句使用它调用 `to12HourString`，以获取已更新对象 `t` 的字符串表示。

## 9.20 静态类成员：类范围数据和成员函数

每个对象都有其类数据成员自己副本这一规则存在例外。在某些情况下，一个类的所有对象应只共享变量的一份副本。静态数据成员用于这些以及其他原因。这样的变量表示“类范围”信息——即由该类的所有对象共享的数据。当一个类的所有对象可以共享数据的一份副本时，可以使用静态数据成员来节省存储空间。

### 为何需要类范围数据

让我们用一个例子进一步探讨对静态类范围数据的需求。假设我们有一个包含火星人和其他 SpaceCreatures 的视频游戏。当火星人意识到至少存在五个火星人时，每个火星人往往很勇敢，并愿意攻击其他 SpaceCreatures。如果存在的火星人少于五个，每个火星人就会变得胆小。因此每个火星人都需要知道 martianCount。我们可以为 Martian 类的每个对象赋予 martianCount 作为数据成员。如果这样做，每个 Martian 都会拥有该数据成员自己的副本。每次创建新的 Martian 时，我们都必须更新所有 Martian 对象中的数据成员 martianCount。这样做要求每个 Martian 对象都了解内存中的所有其他 Martian 对象。这既会因为冗余的 martianCount 副本而浪费空间，也会因更新各个独立副本而浪费时间。相反，我们将 martianCount 声明为 static，使其成为类范围数据。每个 Martian 都可以像访问数据成员一样访问 martianCount，但程序中只维护静态 martianCount 的一份副本。这节省了空间。我们让 Martian 构造函数递增静态变量 martianCount，并让 Martian 析构函数递减 martianCount。由于只有一份副本，我们不必为每个 Martian 对象递增或递减 martianCount 的独立副本。

### 静态数据成员的作用域和初始化

类的静态数据成员具有类作用域。静态数据成员必须恰好初始化一次。基本类型静态数据成员默认初始化为 0。静态 const 数据成员可以有类内初始化器。对于非 const 静态数据成员，也可以通过在其声明前加上 inline 关键字来使用类内初始化器（如图 9.33 所示）。如果静态数据成员是某个提供默认构造函数的类的对象，则该静态数据成员无需显式初始化，因为将调用其默认构造函数。

### 访问静态数据成员

即使该类的对象不存在，类的静态成员也存在。要访问公有静态类数据成员或成员函数，只需在成员名前加上类名和作用域解析运算符（`::`）。例如，如果我们的 martianCount 变量是公有的，即使没有 Martian 对象，也可以通过 `Martian::martianCount` 访问它。

类的私有（以及受保护；第 10 章）静态成员通常通过类的公有成员函数或友元访问。当类对象不存在时，要访问私有静态或受保护静态数据成员，可提供一个公有静态成员函数，并通过在函数名前加上类名和作用域解析运算符来调用该函数。静态成员函数是整个类的服务，而不是类中某个特定对象的服务。

### 演示静态数据成员

本示例演示一个名为 `m_count` 的私有内联静态数据成员，它被初始化为 0（图 9.33，第 22 行），以及一个名为 `getCount` 的公有静态成员函数（图 9.33，第 16 行）。静态数据成员也可以在类的实现文件中于文件作用域初始化。例如，我们可以在包含 `Employee.h` 头文件之后，将以下语句放在 `Employee.cpp`（图 9.34）中：

```cpp
int Employee::m_count{};
```

```cpp
// Fig. 9.33: Employee.h
// Employee class definition with a static data member to
// track the number of Employee objects in memory
#pragma once
#include <string>
#include <string_view>

class Employee {
public:
   Employee(std::string_view firstName, std::string_view lastName);
   ~Employee(); // destructor
   const std::string& getFirstName() const; // return first name
   const std::string& getLastName() const; // return last name

   // static member function
   static int getCount(); // return # of objects instantiated
private:
   std::string m_firstName;
   std::string m_lastName;

   // static data member
   inline static int m_count{}; // number of objects instantiated
};
```

**图 9.33** | 带有静态数据成员的 Employee 类定义，用于跟踪内存中 Employee 对象的数量。

在图 9.34 中，第 10 行定义了静态成员函数 `getCount()`——注意这里不包含 static 关键字，因为不能将其应用于出现在类定义之外的成员定义。在此程序中，数据成员 `m_count` 维护给定时间内存中 Employee 对象的数量计数。当 Employee 对象存在时，可以通过 Employee 对象的任何成员函数引用成员 `m_count`，如构造函数（第 16 行）和析构函数（第 25 行）所示。

```cpp
// Fig. 9.34: Employee.cpp
// Employee class member-function definitions.
#include <format>
#include <iostream>
#include "Employee.h" // Employee class definition
using namespace std;

// define static member function that returns number of
// Employee objects instantiated (declared static in Employee.h)
int Employee::getCount() { return m_count; }

// constructor initializes non-static data members and
// increments static member m_count
Employee::Employee(string_view firstName, string_view lastName)
   : m_firstName(firstName), m_lastName(lastName) {
   ++m_count; // increment static count of employees
   std::cout << std::format("Employee constructor called for {} {}\n",
      m_firstName, m_lastName);
}
```

**图 9.34** | Employee 类成员函数定义。（第 1 部分，共 2 部分。）

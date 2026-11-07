
头文件可能包含其他头文件。如果同一定义在预处理文件中出现多次，就可能导致编译错误。`#pragma once` 指令（第 4 行）防止 `.h` 的内容在同一源代码文件中被多次包含。这有时称为包含守卫。第 16 章将讨论 C++20 模块如何帮助防止此类问题。

### 9.7.4 成员函数

Time.cpp（图 9.8）定义了 Time 类的成员函数，这些函数已在图 9.7 的第 10–12 行声明。对于成员函数 to24HourString 和 to12HourString，const 关键字必须同时出现在函数原型（图 9.7 第 11–12 行）和函数定义（图 9.8 第 23 行和第 28 行）中。

```cpp
// Fig. 9.8: Time.cpp
// Time class member-function definitions.
#include <format>
#include <stdexcept> // for invalid_argument exception class
#include <string>
#include "Time.h" // include definition of class Time from Time.h

// set new Time value using 24-hour time
void Time::setTime(int hour, int minute, int second) {
   // validate hour, minute and second
   if ((hour < 0 || hour >= 24) || (minute < 0 || minute >= 60) ||
       (second < 0 || second >= 60)) {
      throw std::invalid_argument{
         "hour, minute or second was out of range"};
   }

   m_hour = hour;
   m_minute = minute;
   m_second = second;
}

// return Time as a string in 24-hour format (HH:MM:SS)
std::string Time::to24HourString() const {
   return std::format("{:02d}:{:02d}:{:02d}", m_hour, m_minute, m_second);
}

// return Time as a string in 12-hour format (HH:MM:SS AM or PM)
std::string Time::to12HourString() const {
   return std::format("{:02d}:{:02d}:{:02d} {}",
      ((m_hour % 12 == 0) ? 12 : m_hour % 12), m_minute, m_second,
      (m_hour < 12 ? "AM" : "PM"));
}
```

**图 9.8** | Time 类的成员函数定义。

### 9.7.5 在源代码文件中包含类头文件

为了表明 `Time.cpp` 中的成员函数属于 `Time` 类，我们必须先包含 `Time.h` 头文件（图 9.8 第 6 行）。这使我们能够在 Time.cpp 文件中使用类名 Time（第 9、23 和 28 行）。编译 Time.cpp 时，编译器使用 Time.h 中的信息来确保

- 每个成员函数的第一行与其在 Time.h 中的原型匹配，并且
- 每个成员函数都了解该类的数据成员和其他成员函数。

### 9.7.6 作用域解析运算符（::）

每个成员函数的名称（第 9、23 和 28 行）前面都有类名和作用域解析运算符（::）。这会将它们“绑定”到（现在独立的）Time 类定义（图 9.7），该定义声明了类的成员。Time:: 告诉编译器，每个成员函数都位于该类的作用域中，并且其名称对其他类成员是已知的。

如果每个函数名前面没有 "Time::"，编译器就会将这些函数视为与 Time 类无关的全局函数。这类函数也称为“自由”函数，它们在不接收 Time 对象或其指针/引用的情况下，无法访问 Time 的私有数据或调用该类的成员函数。因此，编译器无法编译这些函数，因为它不知道 Time 类声明了变量 m_hour、m_minute 和 m_second。在图 9.8 中，第 17–19、24 和 30–31 行会导致编译错误，因为 m_hour、m_minute 和 m_second 既没有在每个函数中声明为局部变量，也没有声明为全局变量。

### 9.7.7 成员函数 setTime 与抛出异常

函数 setTime（第 9–20 行）是一个 public 函数，它声明三个 int 参数，并使用这些参数设置时间。第 11–12 行测试每个实参以确定其值是否在范围内。如果在范围内，第 17–19 行会分别将这些值赋给 m_hour、m_minute 和 m_second 数据成员。hour 实参必须大于或等于 0 且小于 24，因为 24 小时时间格式将小时表示为 0 到 23 的整数。同样，minute 和 second 实参必须大于或等于 0 且小于 60。

如果任一值超出其范围，setTime 会抛出 invalid_argument 类型的异常（第 13–14 行）（头文件 <stdexcept>），通知客户端代码收到了无效实参。正如你在 6.15 节所见，可以使用 try...catch 捕获异常并尝试从中恢复，我们将在图 9.9 中这样做。throw 语句创建一个新的 invalid_argument 对象，并用自定义错误消息字符串初始化它。异常对象创建后，throw 语句会终止函数 setTime。随后，异常被返回给调用 setTime 的代码。

无效值无法存储到 Time 对象中，因为

- 创建 Time 对象时会调用其默认构造函数，并且每个数据成员都按图 9.7 第 14–16 行的规定初始化为 0——这相当于凌晨 12 点（午夜）——并且
- 客户端随后对数据成员进行的所有修改尝试都会受到函数 setTime 的审查。

### 9.7.8 成员函数 to24HourString 和 to12HourString

成员函数 to24HourString（图 9.8 第 23–25 行）不接受任何实参，并返回一个格式化的 24 小时字符串，其中包含三对用冒号分隔的数字。因此，如果时间是下午 1:30:07，该函数返回 "13:30:07"。第 24 行中的每个 `{:02d}` 占位符将整数（d）格式化为字段宽度为 2 的形式。字段宽度前的 0 表示少于两位的数字应使用前导零格式化。

函数 to12HourString（第 28–32 行）不接受任何实参，并返回一个格式化的 12 小时时间字符串，其中包含用冒号分隔的 m_hour、m_minute 和 m_second 值，后跟 AM 或 PM 指示符（例如 10:54:27 AM 和 1:27:06 PM）。该函数使用占位符 `{:02d}` 将 m_minute 和 m_second 格式化为必要时带前导零的两位数值。第 30 行使用条件运算符（`?:`）确定 m_hour 应如何格式化。如果 m_hour 为 0 或 12（分别对应 AM 或 PM），则显示为 12；否则，我们使用求余运算符（`%`）得到 1 到 11 的值。第 31 行的条件运算符决定是否包含 AM 或 PM。

### 9.7.9 隐式内联成员函数

如果成员函数在类体内完整定义（如我们的 Account 类示例），它会被隐式声明为 `inline`（5.11 节）。这可以提高性能。请记住，编译器保留不对任何函数进行内联的权利。同样，优化编译器也保留将函数内联的权利，即使这些函数没有使用 `inline` 关键字声明，前提是编译器能够访问该函数的定义。

只有最简单、最稳定的成员函数（即其实现不太可能改变的函数）以及性能最敏感的成员函数才应在类头文件中定义。每次更改头文件都要求你重新编译依赖于该头文件的每个源代码文件——在大型系统中这是一项耗时的任务。

### 9.7.10 成员函数与全局函数

成员函数 `to24HourString` 和 `to12HourString` 不接受任何实参。它们隐式地了解并可以访问调用它们时所针对的 Time 对象的数据成员。这是面向对象编程的一个优点。一般来说，与非面向对象程序中的函数调用相比，成员函数调用要么不接收实参，要么接收更少的实参。这降低了传递错误实参、错误数量的实参或顺序错误的实参的可能性。

### 9.7.11 使用 Time 类

一旦定义了 Time 类，它就可以在声明中用作类型，例如：

```
Time sunset{};                         // object of type Time
std::array<Time, 5> arrayOfTimes{};     // std::array of 5 Time objects
Time& dinnerTimeRef{sunset};             // reference to a Time object
Time* timePtr{&sunset};                   // pointer to a Time object
```

图 9.9 创建并操作一个 Time 对象。将 Time 的接口与其成员函数的实现分离，不会影响此客户端代码使用该类的方式。第 8 行包含 Time.h，以便编译器知道要为 Time 对象 t（第 17 行）预留多少空间，并能确保在客户端代码中正确创建和操作 Time 对象。

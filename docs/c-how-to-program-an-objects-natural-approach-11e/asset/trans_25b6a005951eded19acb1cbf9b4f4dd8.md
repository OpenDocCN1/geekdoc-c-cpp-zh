
```text
Reference count for Book C++ How to Program is 2
Reference count for Author Deitel & Deitel is 2

Access Author name and Book title via weak_ptrs:
Reference count for Author Deitel & Deitel is 3
The book C++ How to Program was written by Deitel & Deitel

Reference count for Book C++ How to Program is 3
Author Deitel & Deitel wrote the book C++ How to Program

Reference count for Book C++ How to Program is 2
Reference count for Author Deitel & Deitel is 2

End of main. shared_ptrs going out of scope.
```

**图 20.6** | shared_ptr 会在循环引用数据中导致内存泄漏。（第 2 部分，共 2 部分。）

接下来，第 25–28 行显示 shared_ptr 的引用计数，以表明每个对象都被两个 shared_ptr 引用：

- Book 对象由第 11–12 行中的 shared_ptr 以及 Author 对象中的 shared_ptr（第 22 行）引用，并且
- Author 对象由第 13–14 行中的 shared_ptr 以及 Book 对象中的 shared_ptr（第 21 行）引用。

注意，weak_ptr 不会影响引用计数。第 32 行调用 Book 对象的 printAuthorName 函数，以显示存储在 Book 的 weak_ptr 数据成员中的信息。第 34 行调用 Author 对象的 printBookTitle 函数，以显示存储在 Author 的 weak_ptr 数据成员中的信息。这些函数还都会显示：在函数调用期间创建了另一个 shared_ptr，从而使 Book 和 Author 的引用计数增加到 3。最后，第 37–40 行再次显示 Book 和 Author 的引用计数，以表明在 printAuthorName 和 printBookTitle 中创建的额外 shared_ptr 在函数执行完毕后被销毁，从而使每个对象的引用计数减少到 2。随后，main 终止。

### 内存泄漏

在 main 结束时，我们创建的指向 Author 和 Book 实例的 shared_ptr 离开作用域并被销毁，但请注意，输出中并未显示类 Author 和 Book 的析构函数。这个程序存在内存泄漏——Author 和 Book 对象因其 shared_ptr 数据成员而未被销毁。当 bookPtr 在 main 函数结束时被销毁，类 Book 对象的引用计数变为 1——Author 对象仍有一个指向 Book 对象的 shared_ptr，因此它不会被删除。当 authorPtr 离开作用域并被销毁时，类 Author 对象的引用计数也变为 1——Book 对象仍有一个指向 Author 对象的 shared_ptr。两个对象都没有被删除，因为它们的引用计数都仍然是 1。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1211_0.png)

### 修复内存泄漏

现在，在 main 中第 21–22 行的每一行开头放置 // 将它们注释掉。这样可防止代码设置类 Author 和 Book 的 shared_ptr 数据成员。重新编译代码并再次运行程序，以产生以下输出。我们用粗体显示了最后两行，表明 Author 和 Book 对象已被正确销毁。

```text
Reference count for Book C++ How to Program is 1
Reference count for Author Deitel & Deitel is 1

Access Author name and Book title via weak_ptrs:
Reference count for Author Deitel & Deitel is 2
The book C++ How to Program was written by Deitel & Deitel

Reference count for Book C++ How to Program is 2
Author Deitel & Deitel wrote the book C++ How to Program

Reference count for Book C++ How to Program is 1
Reference count for Author Deitel & Deitel is 1

End of main. shared_ptrs going out of scope.
Destroying Author: Deitel & Deitel
Destroying Book: C++ How to Program
```

注意，现在每个对象的初始引用计数为 1 而不是 2，因为我们没有设置 shared_ptr 数据成员。输出的最后两行表明，Author 和 Book 对象在 main 结束时被销毁。我们仅通过使用 weak_ptr 数据成员消除了内存泄漏；这些 weak_ptr 不影响引用计数，但在需要时仍允许我们通过创建指向资源的临时 shared_ptr 来访问该资源。**当我们在 main 中创建的 shared_ptr 被销毁时，它们的引用计数变为 0，类 Author 和 Book 的实例会被正确销毁。**

## 20.3 使用 std::variant 和 std::visit 的运行时多态

到目前为止，我们的运行时多态示例使用了实现继承或接口继承——两者都需要类层次结构。如果你有一些不相关类的对象，但仍希望在运行时以多态方式处理这些对象，该怎么办？可以使用类模板 `std::variant` 和标准库函数 `std::visit`（来自头文件 `<variant>`）来实现。⁹,¹⁰,¹¹,¹² 需要注意的是，你必须预先知道程序通过运行时多态需要处理的所有类型——这称为封闭类型集。一个 `std::variant` 对象一次可以存储在你创建该 `std::variant` 对象时指定的任意类型的一个对象。正如你将看到的，你可以使用 `std::visit` 函数调用 `std::variant` 对象中对象上的函数。

这种在类型之间没有类层次关系的对象上调用计算的能力通常称为鸭子类型：

> “如果它走起来像鸭子，叫起来也像鸭子，那么它一定是鸭子。”¹³

- 9. Nevin Liber，“`std::variant` 的多种变体”，YouTube 视频，2019 年 6 月 16 日。访问于 2023 年 4 月 18 日。https://www.youtube.com/watch?v=JUxhwf7YgLg.
- 10. “`std::variant`”。访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/utility/variant.html.
- 11. Bartłomiej Filipek，“使用 `std::variant` 和 `std::visit` 的运行时多态”，2020 年 11 月 2 日。访问于 2023 年 4 月 18 日。https://www.bfilipek.com/2020/04/variant-virtual-polymorphism.html.
- 12. Bartłomiej Filipek，“关于 C++17 中 `std::variant` 你需要知道的一切”，2018 年 6 月 4 日。访问于 2023 年 4 月 18 日。https://www.bfilipek.com/2018/06/variant.html.
- 13. “鸭子类型”。维基百科。维基媒体基金会。访问于 2023 年 4 月 18 日。https://en.wikipedia.org/wiki/Duck_typing.

也就是说，如果一个对象具有合适的成员函数，并且其类型被指定为 `std::variant` 的成员，那么该对象就能工作，正如你将在下一个示例中看到的。

为了演示使用 `std::variant` 和鸭子类型实现的运行时多态，我们将重新实现第 10.11 节中的接口继承示例。这里使用的类几乎完全相同，因此我们只指出不同之处。

### 薪酬模型：Salaried

类 `Salaried`（图 20.7–20.8）定义了按固定工资获得报酬的 Employee 的薪酬模型。这个类与第 10.11 节中的类的唯一区别是，**这个 Salaried 不是派生类。因此，它的 earnings 和 toString 成员函数不会重写基类的虚函数。**

```cpp
// Fig. 20.7: Salaried.h
// Salaried compensation model.
#pragma once
#include <string>

class Salaried {
public:
  Salaried(double salary);
  double earnings() const;
  std::string toString() const;
private:
  double m_salary{0.0};
};
```

**图 20.7** | Salaried 薪酬模型。

```cpp
// Fig. 20.8: Salaried.cpp
// Salaried compensation model member-function definitions.
#include <format>
#include <stdexcept>
#include "Salaried.h" // class definition

// constructor
Salaried::Salaried(double salary) : m_salary{salary} {
  if (m_salary < 0.0) {
    throw std::invalid_argument("Weekly salary must be >= 0.0");
  }
}

// calculate earnings
double Salaried::earnings() const { return m_salary; }

// return string containing Salaried compensation model information
std::string Salaried::toString() const {
  return std::format("salary: ${:.2f}", m_salary);
}
```

**图 20.8** | Salaried 薪酬模型的成员函数定义。

### 薪酬模型：Commission

类 Commission（图 20.9–20.10）定义了按销售总额获得佣金的 Employee 的薪酬模型。与 Salaried 一样，这个 Commission 不是派生类。因此，它的 earnings 和 toString 成员函数不会像第 10.11 节中那样重写基类的虚函数。

```cpp
// Fig. 20.9: Commission.h
// Commission compensation model.
#pragma once
#include <string>

class Commission {
public:
   Commission(double grossSales, double commissionRate);
   double earnings() const;
   std::string toString() const;
private:
   double m_grossSales{0.0};
   double m_commissionRate{0.0};
};
```

**图 20.9** | Commission 薪酬模型。

```cpp
// Fig. 20.10: Commission.cpp
// Commission member-function definitions.
#include <format>
#include <stdexcept>
#include "Commission.h" // class definition

// constructor
Commission::Commission(double grossSales, double commissionRate)
   : m_grossSales{grossSales}, m_commissionRate{commissionRate} {

   if (m_grossSales < 0.0) {
      throw std::invalid_argument("Gross sales must be >= 0.0");
   }

   if (m_commissionRate <= 0.0 || m_commissionRate >= 1.0) {
      throw std::invalid_argument(
         "Commission rate must be > 0.0 and < 1.0");
   }
}

// calculate earnings
double Commission::earnings() const {
   return m_grossSales * m_commissionRate;
}
```

**图 20.10** | Commission 成员函数定义。（第 1 部分，共 2 部分。）


三参数版本默认将**公共范围**的元素相加。四参数版本接收一个**二元函数**作为其最后一个参数，用于自定义如何执行计算。该参数可以通过以下形式提供：

- 一个**指向二元函数的函数指针**，该二元函数接受两个**公共范围**元素类型的参数并返回该类型的结果，
- 一个二元函数对象，其中 **operator()** 函数接受两个**公共范围**元素类型的参数并返回该类型的结果，或者
- 一个 **lambda**，它接受两个**公共范围**元素类型的参数并返回该类型的结果。

此示例分别用函数指针、函数对象和 lambda 调用 **accumulate**。

```cpp
// fig14_16.cpp
// Demonstrating function objects.
#include <array>
#include <algorithm>
#include <functional>
#include <iostream>
#include <iterator>
#include <numeric>
```

**图 14.16** 演示函数对象。

### 函数 sumSquares

第 12–14 行定义了一个函数 **sumSquares**，它接受两个相同类型的参数并返回该类型的值——这是 **accumulate** 可作为参数接收的**二元函数**的要求。sumSquares 函数返回其第一个参数 total 与第二个参数 value 的平方之和。

```cpp
// binary function returns the sum of its first argument total
// and the square of its second argument value
int sumSquares(int total, int value) {
    return total + value * value;
}
```

### 类 SumSquaresClass

第 19–25 行定义类 SumSquaresClass。³¹ 其重载的 **operator()** 有两个 int 参数并返回一个 int。这满足 accumulate 在处理 int 的**公共范围**时可调用的二元函数的要求。函数 **operator()** 返回其第一个参数 total 与第二个参数 value 的平方之和。

31. 该类只处理 int 值，但可以实现为处理多种类型的类模板——我们将在第 15 章定义自定义类模板。

```cpp
// class SumSquaresClass defines overloaded operator()
// that returns the sum of its first argument total
// and the square of its second argument value
class SumSquaresClass {
public:
    // add square of value to total and return result
    int operator()(int total, int value) {
        return total + value * value;
    }
};
```

### 调用算法 accumulate

我们三次调用 accumulate：

- 第 36–37 行以指向 sumSquares 的指针作为最后一个参数调用 **accumulate**。
- 第 44–45 行以 **SumSquaresClass** 函数对象作为最后一个参数调用 **accumulate**。第 45 行中的 **SumSquaresClass{}** 创建一个临时 **SumSquaresClass** 对象并调用其构造函数。然后该函数对象被传递给 **accumulate**，后者调用 **SumSquaresClass** 对象的 **operator()** 函数。
- 第 50–51 行以等价的 lambda 调用 **accumulate**。该 lambda 执行与函数 **sumSquares** 以及 **SumSquaresClass** 中重载的 **operator()** 函数相同的任务。

```cpp
int main() {
    std::array integers{1, 2, 3, 4};
    std::ostream_iterator<int> output{std::cout, " "};

    std::cout << "array integers contains: ";
    std::ranges::copy(integers, output);

    // calculate sum of squares of elements of array integers
    // using binary function sumSquares
    int result{std::accumulate(integers.cbegin(), integers.cend(),
        0, sumSquares)};

    std::cout << "\n\nSum of squares\n"
        << "via binary function sumSquares: " << result;

    // calculate sum of squares of elements of array integers
    // using binary function object
    result = std::accumulate(integers.cbegin(), integers.cend(),
        0, SumSquaresClass{});

    std::cout << "\n\nvia a SumSquaresClass function object: " << result;

    // calculate sum of squares array
    result = std::accumulate(integers.cbegin(), integers.cend(),
        0, [](auto total, auto value){return total + value * value;});

    std::cout << "\n\nvia a lambda: " << result << "\n";
}
```

```text
array integers contains: 1 2 3 4

Sum of squares
via binary function sumSquares: 30
via a SumSquaresClass function object: 30
via a lambda: 30
```

每次调用 **accumulate** 时，其函数参数的使用方式如下：

- 在第一次调用其函数参数时，**accumulate** 传入其第三个参数的值（本例中为 0）和 `integers` 第一个元素的值（本例中为 1）。这会计算并返回 0 + 1 * 1 的结果，即 1。
- 在第二次调用其函数参数时，**accumulate** 传入先前的结果（1）和 `integers` 下一个元素的值（2）。这会计算并返回 1 + 2 * 2 的结果，即 5。
- 在第三次调用其函数参数时，**accumulate** 传入先前的结果（5）和 `integers` 下一个元素的值（3）。这会计算并返回 5 + 3 * 3 的结果，即 14。
- 在最后一次调用其函数参数时，**accumulate** 传入先前的结果（14）和 `integers` 下一个元素的值（4）。这会计算并返回 14 + 16 的结果，即 30。

此时，**accumulate** 到达其前两个参数指定的公共范围的末尾，因此返回对其函数参数最后一次调用的结果（30）。

## 14.6 投影

在处理包含多个数据项的对象时，每个 C++20 **std::ranges 算法**都可以使用投影来选择每个对象中更窄的一部分进行处理。考虑每个都有名、姓和薪水的 Employee 对象。与其基于全部三个数据成员对 Employee 对象排序，你可以仅使用它们的薪水进行排序。图 14.17 按薪水对一个 Employee 对象数组排序——先按升序，再按降序。第 11–22 行定义类 Employee。第 25–29 行提供了一个重载的 operator<< 函数，以便方便地输出 Employee 对象。

```cpp
// Fig14_17.cpp
// Demonstrating projections with C++20 range algorithms.
#include <array>
#include <algorithm>
#include <format>
#include <iostream>
#include <iterator>
#include <string>
#include <string_view>
```

**图 14.17** | 演示 C++20 范围算法中的投影。

```cpp
class Employee {
public:
    Employee(std::string_view first, std::string_view last, int salary)
        : m_first{first}, m_last{last}, m_salary{salary} {}
    std::string getFirst() const { return m_first; }
    std::string getLast() const { return m_last; }
    int getSalary() const { return m_salary; }
private:
    std::string m_first;
    std::string m_last;
    int m_salary;
};

// operator<< for an Employee
std::ostream& operator<<(std::ostream& out, const Employee& e) {
    out << std::format("{:10}{:10}{}",
        e.getLast(), e.getFirst(), e.getSalary());
    return out;
}
```

**图 14.17** | 演示 C++20 范围算法中的投影。

### 定义并显示一个 array<Employee>

第 32–36 行定义一个 array<Employee>，并用三个 Employee 对象初始化它。第 41 行显示这些 Employee 对象，以便我们稍后确认它们已正确排序。

```cpp
int main() {
    std::array<Employee> employees{
        Employee{"Jo-woon", "Woo", 5000},
        Employee{"Amaia", "Jones", 7600},
        Employee{"Titania", "Makaya", 3587}
    };

    std::ostream_iterator<Employee> output{std::cout, "\n"};

    std::cout << "Employees:\n";
    std::ranges::copy(employees, output);
}
```

```text
Employees:
Woo       Jo-woon   5000
Jones     Amaia     7600
Makaya    Titania   3587
```

### 使用投影按升序对 array<Employee> 排序

第 45–46 行调用 `std::ranges::sort` 算法，传入三个参数：

- 第一个参数（employees）是要排序的范围。
- 第二个参数（{}）是 sort 用来在确定排序顺序时比较元素的二元谓词函数。记号 {} 表示

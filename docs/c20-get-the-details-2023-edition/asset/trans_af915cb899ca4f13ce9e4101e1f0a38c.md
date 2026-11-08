

```cpp
auto format(const SingleValue& sVal, std::format_context& context) const {
    return std::format_to(context.out(), "{}", sVal.getValue());
}
};

int main() {

    std::cout << '\n';

    SingleValue sVal0;
    SingleValue sVal2020[2020];
    SingleValue sVal2023[2023];

    std::cout << std::format("Single Value: {} {} {}\n", sVal0, sVal2020, sVal2023);
    std::cout << std::format("Single Value: {1} {1} {0}\n", sVal0, sVal2020, sVal2023);
    std::cout << std::format("Single Value: {2} {1} {0}\n", sVal0, sVal2020, sVal2023);

    std::cout << '\n';

}
```

SingleValue（第 6 行）是一个只有一个值的类。成员函数 getValue（第 10 行）返回这个值。我为 SingleValue 特化了 std::formatter（第 17 行）。这个特化具有成员函数 parse（第 19 行）和 format（第 22 行）。parse 返回格式说明的结尾。格式说明的结尾是右花括号 }。format 格式化该值，而 context.out 创建一个传递给 std::format_to 的对象。format_to 返回用于进一步输出的新位置。

执行这个程序会得到预期结果。

![](img/c60a87adb7f61e2e82071d081bbb389a_364_0.png)

单值格式化器

这个格式化器有一个严重缺陷。它不支持格式说明符。让我改进这一点。

### 5.5.3.1.1 支持格式说明符的格式化器

当你的格式化器基于标准格式化器时，为用户定义类型实现格式化器相当直接。将用户定义的格式化器基于标准格式化器可以通过两种方式完成。

### 5.5.3.1.2 委托

下面的格式化器将其工作委托给标准格式化器。

支持格式说明符的单值格式化器（委托）

```cpp
// formatSingleValueDelegation.cpp

#include <format>
#include <iostream>

class SingleValue {
public:
    SingleValue() = default;
    explicit SingleValue(int s): singleValue{s} {}
    int getValue() const {
        return singleValue;
    }
private:
    int singleValue;
};

template<>
struct std::formatter<SingleValue> {

    std::formatter<int> formatter;

    constexpr auto parse(std::format_parse_context& context) {
        return formatter.parse(context);
    }

    auto format(const SingleValue& singleValue, std::format_context& context) const {
        return formatter.format(singleValue.getValue(), context);
    }

};

int main() {

    std::cout << '\n';

    SingleValue singleValue0;
    SingleValue singleValue2020{2020};
    SingleValue singleValue2023{2023};


    std::cout << std::format("{:*<10}", singleValue0) << '\n';
    std::cout << std::format("{:*>10}", singleValue2020) << '\n';
    std::cout << std::format("{:*^10}", singleValue2023) << '\n';


    std::cout << '\n';
}
```

std::formatter<SingleValue>（第 17 行）有一个用于 int 的标准格式化器：std::formatter<int> formatter（第 20 行）。我将解析工作（第 23 行）委托给该格式化器（第 23 行）。相应地，格式化工作 format 也被委托给该格式化器（第 27 行）。

该程序的输出表明，这个格式化器支持填充字符和对齐。

![](img/c60a87adb7f61e2e82071d081bbb389a_366_0.png)

### 5.5.3.1.3 继承

得益于继承，为用户定义类型 SingleValue 实现格式化器轻而易举。

支持格式说明符的单值格式化器（继承）

```cpp
// formatSingleValueInheritance.cpp

#include <format>
#include <iostream>

class SingleValue {
public:
    SingleValue() = default;
    explicit SingleValue(int s): singleValue{s} {}
    int getValue() const {
        return singleValue;
    }
private:
    int singleValue{};
};

template<>
struct std::formatter<SingleValue> : std::formatter<int> {
    auto format(const SingleValue& singleValue, std::format_context& context) const {
        return std::formatter<int>::format(singleValue.getValue(), context);
    }
};

int main() {

    std::cout << '\n';

    SingleValue singleValue{};
    SingleValue singleValue2020{2020};
    SingleValue singleValue2023{2023};

    std::cout << std::format("{:*>10}", singleValue) << '\n';
    std::cout << std::format("{:*>10}", singleValue2020) << '\n';
    std::cout << std::format("{:*>10}", singleValue2023) << '\n';

    std::cout << '\n';

}
```

我从 `std::formatter<int>` 派生 `std::formatter<SingleValue>`（第 18 行）。只需实现 format 函数。该程序的输出与前一个程序 `formatSingleValueDelegation.cpp` 的输出相同。

委托给标准格式化器或从标准格式化器继承，是实现用户定义格式化器的直接方式。此策略仅适用于只有一个值的用户定义类型。

### 5.5.3.2 用于多个值的格式化器

Point 是一个有三个成员的类。

支持格式说明符的 Point 格式化器

```cpp
// formatterPoint.cpp

#include <format>
#include <iostream>
#include <string>

struct Point {
    int x{2017};
    int y{2020};
    int z{2023};
};

template <>
struct std::formatter<Point> : std::formatter<std::string> {
    auto format(Point const& point, std::format_context& context) const {
        return std::formatter<std::string>::format(
            std::format("({}, {}, {})", point.x, point.y, point.z), context);
    }
};

int main() {

    std::cout << '\n';

    Point point;

    std::cout << std::format("{:*<25}", point) << '\n';
    std::cout << std::format("{:*^25}", point) << '\n';
    std::cout << std::format("{:*>25}", point) << '\n';

    std::cout << '\n';

    std::cout << std::format("({} {} {})", point.x, point.y, point.z) << '\n';
    std::cout << std::format("{0:*<10} {0:*^10} {0:*>10}", point) << '\n';

    std::cout << '\n';
}
```

在这种情况下，我从标准格式化器 `std::formatter<std::string>` 派生。也可以使用 `std::string_view`。`std::formatter<Point>` 通过对 `std::formatter` 调用 `format` 来创建格式化输出。这个函数调用已经获得一个格式化字符串作为值。因此，`std::string` 的所有格式说明符都适用（第 27 – 29 行）。相反，你也可以格式化 `Point` 的每个值。这正是第 33 和 34 行发生的情况。

![](img/c60a87adb7f61e2e82071d081bbb389a_369_0.png)

## 5.5.4 国际化

格式化函数 `std::format*` 和 `std::vformat*` 具有接受 locale 的重载。这些重载允许你本地化格式字符串。

下面的代码片段展示了 `std::format` 的对应重载：

接受 locale 的 std::format 重载

```cpp
template< class... Args >
std::string format( const std::locale& loc,
                    std::format_string<Args...> fmt, Args&&... args );
```

要使用给定的 locale，请在格式字符串中的类型说明符前指定 L。现在，你在每次调用 `std::format` 时应用该 locale，或者用 `std::locale::global` 全局设置它⁴⁴。

在下面的示例中，我在每次 `std::format` 调用中显式应用德语 locale。

⁴⁴ https://en.cppreference.com/w/cpp/locale/locale/global

```cpp
45
46        const auto now = std::chrono::system_clock::now();
47        std::cout << "Default locale: " << std::format("{}\n", now);
48        std::cout << "German locale:  " << std::format(loc, "{:L}\n", now);
49
50        std::cout << '\n';
51
52 }
```

函数 createLocale（第 8 行）创建德语 locale。如果失败，则返回使用美式格式的默认 locale。我在第 26、31、42 和 48 行使用德语 locale。为了看到差异，我还在其后立即应用了 std::format 调用。因此，整数值（第 26 行）使用依赖 locale 的千位分隔符，浮点值（第 31 行）使用依赖 locale 的小数点和千位分隔符。相应地，时间长度（第 42 行）和时间点（第 48 行）使用给定的德语 locale。

下面的截图显示了该程序的输出。

![](img/c60a87adb7f61e2e82071d081bbb389a_371_0.png)

使用德语 locale


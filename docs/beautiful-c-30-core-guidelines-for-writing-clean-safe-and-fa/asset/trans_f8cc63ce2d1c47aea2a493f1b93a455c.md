

int amend_content(std::string const& format,
    /*输出参数*/ std::string& destination);

void* memcpy(
_Out_writes_bytes_all_(count) void* dest,
_In_reads_bytes_(count) const void* src,
size_t count
);

BigObj create_big_obj(); // 函数原型
BigObj big_obj = create_big_obj();

SmallObj so() {
    return SmallObj(); // RVO（见下文）
}
int main() {
    std::cout <<"Testing...\n";
    SmallObj s = so();
}

std::pair<int, int> f(int a, int b) {
    return {a + b, a * b};
}

BigObj do_stuff(int a, int b, error_code& err);

std::pair<BigObj, error_code> do_stuff(int a, int b) {
    // 验证输入
    return { {a, b}, {error} };
}

BigObj bo;
error_code ec;

std::tie(bo, ec) = do_stuff(1, 2);

auto [bo, ec] = do_stuff(1, 2);

int a[2] = {1, 2};
auto [b, c] = a; // b 和 c 是整数，其中 b = 1，c = 2

struct S {
    int a;
    int b;
};
S make_s();

auto [d, e] = make_s(); // d = 返回的结构体的第一个成员
                        // e = 第二个成员。

返回值，标识符（输入参数、输入-输出参数、
输出参数）；

class Report { ...};

int report_rendering(int, int, Report&);  // 输入参数..
int report_fileIO(int, int, int, Report&); // 然后是输入-输出参数

std::pair<Report, int> collect_report(const char* title) {
    auto report = Report(title);
    int item_count =  report_rendering(1, 2, report);
    item_count += report_fileIO(0, 0, 1024, report);
    return {report, item_count};
}

std::pair<Report, int> collect_report(const char* title) {
    auto report = Report(title);
    int item_count = report_rendering(1, 2, report).second;
    item_count += report_fileIO(0, 0, 1024, report).second;
    return {report, item_count};
}

int report_rendering(Report&, int, int);
int report_fileIO(Report&, int, int, int);

int Report::report_rendering(int, int);
int Report::report_fileIO(int, int, int);

std::cout << "Hello, world!" << std::endl;

operator <<(std::cout, "Hello, world!").operator <<(std::endl);

if (x > 15) {
    auto y = 200;
    auto z = do_work(y);
    auto gamma = do_more_work(z);
    inform_user(z, gamma);
}

if (x > 15) {
    auto y = 200;
    auto z = do_work(y);
    {
        auto y = z;                 // 新作用域
        // 下一个 y 的作用域从这里开始
        y += mystery_factor(8);     // 仍然指向下一个 y
        inform_user(y, 12);         // 仍然指向下一个 y
    }                               // 下一个 y 的作用域在这里结束
    y = do_more_work(z);            // 第一个 y 的作用域从这里恢复
    inform_user(z, y);
}

namespace CG30 { // 作用域从这里开始

```cpp
namespace CG30 {
    auto y = 76; // Scope of y begins here
} // Scope of y is interrupted here

...

namespace CG30 { // Scope of y resumes here
    auto x = y;
}
```

namespace CG30 {
    auto y = 76;
    namespace {
        auto x = 67;
    } // x 仍在其作用域内
    auto z = x;
} // x 的作用域在这里中断。

namespace {
    constexpr auto pi = 3.14159f;
} // pi 仍在其作用域内

namespace CG30 {
    auto y = 76;
    inline namespace version_1 {
        auto x = 67;
    } // x 仍在其作用域内
    auto z = x;
} // x 的作用域在这里中断

class RPM {
    static constexpr int LP = 33;
    static constexpr int Single = 45;

public:
    static constexpr int SeventyEight = 78;
    int RotorMax(int x, int y = LP);
}; // RotorMax、LP、Single 和 SeventyEight 仍在其作用域内
    // 在 RPM 的成员函数体内

int RPM::RotorMax(int x, int y)
{
    return LP + x + y;
}

float divide(float a, // a 的作用域从这里开始
    float b); // a 的作用域到这里结束

float divide(float a, // a 的作用域从这里开始
    float b) {
  return a / b;
} // a 的作用域到这里结束

float divide(float a, // a 的作用域从这里开始
            float b)
try {
    std::cout << "Dividing\n";
    return a / b;
} catch (...) { // a 的作用域在此之后仍然持续
    std::cout << "Dividing failed, was the denominator zero?\n";
} // a 的作用域到这里结束

enum US_state_abbreviation { // 无作用域枚举
  ...
  VT,
  VA,
  VI,
  WA,
  WV,
  WI,
  WY
}; // VI（美属维尔京群岛）的作用域不会在这里结束。

enum class Element { // 有作用域枚举
  ...
  Nh,
  Fl,
  Mc,
  Lv,
  Ts,
  Og
}; // Lv（鉝）的作用域在这里结束。

US_state_abbreviation southernmost = HI; // HI 在其作用域内
// Element lightweight = H;               // H 不在作用域内
Element lightweight = Element::H;         // H 在其作用域内

template< typename T,           // T 的作用域开始
          T* p >                // T 仍在其作用域内
class X : public std::pair<T, T> // T 仍在其作用域内
{
    ...
    T m_instance;              // T 仍在其作用域内
    ...
};                              // T 的作用域结束

UIComponent* spin_cards(UIComponent* first,
    UIComponent* n_first,
    UIComponent* last) {
    if (first == n_first) return last;
    if (n_first == last) return first;
    UIComponent* write = first;
    UIComponent* next_read = first;
    UIComponent* read = n_first;
    while (read != last) {
        if (write == next_read) {
            next_read = read;
        }
        std::iter_swap(write++, read++);
    }
    spin_cards(write, next_read, last);
    return write;
}

UIComponent* spin_cards(UIComponent* first,
                        UIComponent* n_first,
                        UIComponent* last) {
    if (first == n_first) return last;
    if (n_first == last) return first;
    auto write = first;
    auto next_read = first;
    auto read = n_first;
    while (read != last) {
        if (write == next_read) {
            next_read = read;
        }
        std::iter_swap(write++, read++);
    }
    spin_cards(write, next_read, last);
    return write;
}

```cpp
template <typename T>
T* spin_cards(T* first, T* n_first, T* last) {
    if (first == n_first) return last;
    if (n_first == last) return first;
    auto write = first;
    auto next_read = first;
    auto read = n_first;
    while (read != last) {
        if (write == next_read) {
            next_read = read;
        }
        std::iter_swap(write++, read++);
    }
    spin_cards(write, next_read, last);
    return write;
}
```

UIComponent* spin_cards(UIComponent* first,
    UIComponent* n_first,
    UIComponent* last) {
    if (first == n_first) return last;
    if (n_first == last) return first;
    UIComponent* write = first;
    UIComponent* next_read = first;
    UIComponent* read = n_first;
    while (read != last) {
        if (write == next_read) {
            next_read = read;
        }
        UIComponent tmp = *write;
        *write++ = *read;
        *read++ = tmp;
    }
    spin_cards(write, next_read, last);
    return write;
}


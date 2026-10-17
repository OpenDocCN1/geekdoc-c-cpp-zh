
一旦 `promise` 返回了一个将将向子函数发送值的 `future`，函数 `fu.share()` 就会将该对象转换为 `std::shared_future` 对象。

共享未来对象作为参数传递给子函数。由于共享对象可以进行拷贝构造和拷贝赋值，因此我们不需要传递指向子对象的引用。

语句 `p.set_value(10)` 通过共享 `future` 对象将相同的值 10 发送给所有子函数。

# C++ 标准库: std::atomic

`std::atomic` 类模板的声明如下：

```cpp
template <class T> struct atomic { }
```

类型为 `std::atomic<class T>` 的对象会以原子方式更改标量变量的值。也就是说，该类型的变量保证在产生任何数据竞态的情况下提供读取和写入访问。原子变量可以在不需要互斥锁（`mutex`）的情况下进行更改。整数原子类型变量可以定义如下：

```cpp
atomic<int> x;
```

`atomic` 类模板支持的类型如：`bool`, `char`, `int`, `long`, `unsigned int`, `unsigned long`, `short`, `unsigned short`, `wchar_t`, `unsigned long long` 等。

原子变量不能被拷贝或移动。

语句 `atomic<int> x;` 将创建一个类型为 `int` 的未初始化原子变量 `x`。

原子模板类的一些方法是：`store`, `load`, `exchange`, `operator++` 和 `operator--`。

以下是一个用法示例：

```cpp
#include <iostream>
#include <atomic>
int main()
{
    std::atomic<int> val(5);
    std::cout << "value of atomic variable val with constructor 5: ";
    std::cout << val << std::endl;
    int x = 3400;
    std::cout << "value of variable x: " << x << std::endl;
    x = val.load();
    std::cout << "value of x after x = val.load(): ";
    std::cout << x << std::endl;
    val++;
    std::cout << "value of atomic variable after val++: ";
    std::cout << val << std::endl;
    val.store(99);
    std::cout << "value of atomic variable after val.store(99): ";
    std::cout << val << std::endl;
    --val;
    std::cout << "value of atomic variable after --val: ";
    std::cout << val << std::endl;
} // output
value of atomic variable val with constructor 5: 5
value of variable x: 3490
value of x after x = val.load(): 5
value of atomic variable after val++: 6
value of atomic variable after val.store(99): 99
value of atomic variable after --val: 98
```

## 原子类型别名

`std::atomic<bool>` `std::atomic_bool`

`std::atomic<int>` `std::atomic_int`

其他类型别名也类似。

# C++ 标准库: std::bind

注意：另请参见 `std::function`。`std::bind` 的声明如下：

```cpp
template <class F, class... Args>
```

`std::bind` 是一个函数适配器。它创建一个可调用对象，该对象使用给定参数调用函数。

以下是一个示例：

```cpp
#include <iostream>
#include <functional>
int adder(int x, int y)
{
    return x + y;
}
int main()
{
    auto f = std::bind(adder, std::placeholders::_1, std::placeholders::_2);
    std::cout << f(10, 20) << std::endl;
    auto f2 = std::bind(adder, 10, std::placeholders::_1);
    std::cout << f2(20) << std::endl;
}
```
Output:
30
30
```

```cpp
#include <iostream>
#include <ratio>
int main()
{
    std::ratio<3,7> rl;
    std::cout << rl.num << " " << rl.den << std::endl;
    typedef std::ratio<4, 8> r2;
    std::cout << r2::num << " " << r2::den << std::endl;
}
// 输出
3 : 7
1 : 2
```

注意在声明中：`ratio<4, 8>`，`r2::num` 和 `r2::den` 被约简为最大公分数。

# 时长 (Durations)

`std::chrono::duration` 是一个表示时间间隔的类模板。它的声明如下：

```cpp
#include <chrono>
template<class Type, class Period = std::ratio<1>>
class duration;
```

该类模板有两个参数。`Type` 是一个算术类型，如 `int`、`long`、`double`、`float` 等。它表示以刻（ticks）计的时间（自时钟起点以来的刻数）。`Period` 是一个 `std::ratio` 参数。它表示每秒的刻数，或者如果大于秒，则表示从一个刻到下一个刻的秒。`Period` 是编译时的有理常量。

`Period<1,500>` 意味着每秒有五千个刻。`Period<1000,1>`（或 `Period<1000>`）意味着每 1000 秒有一个刻。

默认周期是 `Period<1>`（每秒一个刻）。

假设我们每秒有 5000 个刻，那么20 秒的时长可以定义如下：

```cpp
#include <iostream>
#include <chrono>
#include <ratio>
using namespace std;
int main() {
    // 100000 是以刻计的时长
    chrono::duration<int,5000> dur{100000};
    cout << (double) dur.count()/5000;
}
```

`duration` 对象的构造函数接受一个以刻计的值。

`duration` 对象有一个成员函数 `count()`。`count` 返回一个 `Type` 类型的常量。该数值是对象以刻计的时长，或自时钟起点以来的刻数。假设我们的 `count` 函数返回 1000。这是以刻表示的时长。该值根据 `duration` 的周期进行解释。假设周期是 `ratio<1,1000>`。这意味着每秒有一千个刻。因此，`count` 被解释为返回一秒的时长。如果周期是 `ratio<1,10>`，则每秒有 10 个刻。因此 `count` 被解释为返回 10 秒的时长。

总结来说，`duration` 类包含编译时的刻周期，它是一个 `std::ratio` 类型。刻周期指定了每秒的刻数。默认周期是 `ratio<1,1>`，每秒一刻（表示为 `ratio<1>`）。如 `ratio<1,1000>` 这样的周期意味着每秒有一千个刻，因此一刻是毫秒。`ratio<1,1000000>` 周期意味着每秒有一百万个刻，因此一刻是微秒。`ratio<3600,1>`（或 `ratio<3600>`）意味着每 3600 秒有一个刻。

标准库定义了一些常见的时长类型：

```
typedef std::chrono::duration<signed int, ratio<1,1000000000>> std::chrono::nanoseconds;
typedef std::chrono::duration<signed int, ratio<1,100000>> std::chrono::microseconds;
typedef std::chrono::duration<signed int, ratio<1,1000>> std::chrono::milliseconds;
typedef std::chrono::duration<signed int, ratio<1,1>> std::chrono::seconds;
typedef std::chrono::duration<signed int, ratio<60,1>> std::chrono::minutes;
typedef std::chrono::duration<signed int, ratio<3600,1>> std::chrono::hours;
```

使用这些预定义类型的 `<iostream>` 示例如下：

```
#include <iostream>
#include <chrono>
int main()
{
    // 定义一个时长为 1 秒的 duration 对象
    std::chrono::seconds sec(1);
    // 创建一个接收一秒时长对象的微秒对象
    std::chrono::microseconds ms(sec);
    std::cout << ms.count() << std::endl;
    // 输出
    1'000'000
}
```

`duration` 类重载了 `+`、`-`、`*`、`%`、`==`、`<=`、`>`、`>=`、`!=`、`>` 运算符。这些运算符允许对不同周期的 duration 对象进行算术运算和比较。对于算术运算符，两个 duration 操作数都会转换为它们的最大公周期。

另一个 duration 示例：

```cpp
#include <iostream>
#include <chrono>
#include <ratio>
int main()
{
    std::chrono::duration<long, std::ratio<1>> dr1(100);
    std::cout << "duration = " << dr1.count() << std::endl;
    std::chrono::duration<long, std::ratio<60, 1>> dr2(50);
    std::cout << "duration = " << dr2.count() << std::endl;
    std::chrono::duration<double, std::ratio<1, 2>> dr3(100);
    std::cout << "duration = " << dr3.count() << std::endl;
    // 相加两个 duration 对象
    auto dr4 = dr1 + dr2;
    std::cout << "duration = " << dr4.count() << std::endl;
    // 减去 duration 对象
    auto dr5 = dr2 - dr1;
    std::cout << "duration = " << dr5.count() << std::endl;
    return 0;
    // 输出
    duration = 100
    duration = 50
    duration = 100
    duration = 3100
    duration = 2900
```

函数模板 `std::duration_cast` 将 duration 对象转换为具有不同周期的 duration 对象。由于编译器会隐式地将 duration 对象的周期转换为公共周期，因此只有在发生精度损失时才需要此函数。函数模板 `std::duration_cast` 如下：

```
template <class ToDuration, class Rep, class Period>
ToDuration duration_cast(const duration<Rep, Period>& d);
```

函数模板 `duration_cast` 将 duration 对象转换为具有不同周期的 duration 对象。由于编译器会隐式地将 duration 对象的周期转换为公共周期，因此只有在发生精度损失时才需要此函数。

使用 duration_cast 的示例：

```
#include <iostream>
#include <chrono>
int main() {
    // 定义一个 144 分钟的对象
    std::chrono::minutes mins(144);
    // 转换为小时对象
    std::chrono::hours hrs = std::chrono::duration_cast<std::chrono::hours>(mins);
    std::cout << hrs.count() << std::endl;
}
```

# 时间点 (Time Points)

`time_point` 表示自时钟起点（epoch）以来的时间点。

```cpp
#include <chrono>
template <
    class Clock,
    class Duration
>
class time_point;
```

`Clock` 是一个如 `system_clock`、`steady_clock` 或其他类。第二个模板参数是 duration 类型。

`time_point` 的一些成员函数有：

- `time_since_epoch` 自起点开始时长（刻数）
- `operator++`、`operator--` 增加或减少时钟时长
- `operator+=`、`operator-=` 通过给定时长修改时间点
- `operator+`、`operator-` 相加或减去时长

`time_point` 对象可以比较：`operator==`、`operator!=`、`operator>`、`operator <` 和 `operator <=`

`time_point_cast` 将时间点转换为同一时钟上不同时长的时间点。

使用 `time_point` 的示例：

```cpp
#include <iostream>
#include <chrono>
int main() {
    // 获取当前系统时间
    std::chrono::system_clock::time_point now = std::chrono::system_clock::now();
    // 转换为 time_t
    std::time_t t = std::chrono::system_clock::to_time_t(now);
    // 打印
    std::cout << "now is: " << std::ctime(&t);
}
```

# 让当前线程休眠

注意：查看 `std::thread`

```cpp
#include <thread>
#include <chrono>
std::this_thread::sleep_for(std::chrono::seconds(15));
```

# 自 Unix 纪元以来的秒数

```cpp
#include <stdio.h>
#include <time.h>
long seconds = time(NULL);
printf("自 1970 年 1 月 1 日以来的秒数 = %ld\n", seconds);
```

我们也可以使用 `std::chrono`：

```cpp
#include <chrono>
#include <ratio>
size_t time_now = duration_cast<seconds>(std::system_clock::now().time_since_epoch()).count();
```

# C++ 标准库：std::copy

函数模板 `std::copy` 将一个容器拷贝到另一个相同类型的容器中。`std::copy` 的声明如下：

```cpp
template <class InputIterator, class InputIterator, class OutputIterator>
OutputIterator copy(InputIterator first, InputIterator last, OutputIterator res);
```

`copy` 函数接收指向第一个容器起始位置的迭代器以及指向第一个容器末尾的迭代器。该函数将第一个容器从第一个迭代器值到（包含）最后一个迭代器值的所有值拷贝到从 `res` 迭代器开始的第二个容器中。该函数返回指向第二个容器的迭代器，该迭代器位于最后一个拷贝项之后的位置：

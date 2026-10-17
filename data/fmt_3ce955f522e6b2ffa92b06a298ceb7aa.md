
```cpp
void adder(std::string id, size_t loop_limit) {

    // 使用参数 m1 创建一个 lock_guard 对象

    std::lock_guard<std::mutex> lock(m1);

    // critical section

    for (size_t i = 0; i < loop_limit; i++) {

        sum += i;

    }

    std::cout << id << ":" << sum << std::endl;

}

int main() {

    std::thread t1(adder, "t1", 20);

    std::thread t2(adder, "t2", 30);

    t1.join();

    t2.join();

    return 0;

}

// output

t1:190

t2:625
```

我们为互斥锁 `m1` 创建了一个 `lock_guard` 对象 `lock`。进入 `adder` 函数的线程将等待获取锁。一旦 `lock_guard` 对象离开作用范围或抛出异常，锁将自动释放。

`lock_guard` 对象的所有权无法通过拷贝构造函数或赋值来传递。

## std::unique_lock<std::mutex>

`std::unique_lock<std::mutex>` 类模板是一个包装器，允许锁定、带时间限制的锁定和递归锁定。互斥锁模板类型必须支持以下函数之一：`lock()`、`try_lock_for` 或 `try_lock_until`。模板类型还必须支持 `unlock()` 函数。

支持以下互斥锁类型：

- 1. `lock(some_mutex)`
- 2. `try_lock(some_mutex)`
- 3. `try_lock_for(some_mutex)`
- 4. `try_lock_until(some_mutex)`
- 6. `owns_lock(some_mutex)` - 对象是否拥有该互斥锁

`owns_lock()` 函数判断 `std::unique_lock` 是否已获取锁。

如果抛出异常或锁对象离开作用范围，由 `unique_lock` 对象获取的锁将自动释放。

`std::unique_lock` 对象可以与条件变量配合使用。此外，这些对象是可移动但不可拷贝的。

这是一个用法示例：

```cpp
#include <iostream>
#include <thread>
#include <mutex>
std::mutex m1; // mutex for critical section
void print_block(int n, char c) {
    // 可以使用以下互斥锁：
    // std::unique_lock<std::mutex> lock (m1);
    // std::unique_lock<std::mutex> try_lock (m1);
    // std::unique_lock<std::mutex> lock (m1);
    // std::unique_lock<std::mutex> try_lock_until (m1);
    std::unique_lock<std::mutex> lock (m1);
    // critical section
    for (int i = 0; i < n; i++) {
        std::cout << c;
    }
    std::cout << '\n';
}
int main () {
    std::thread t1(print_block, 20, 'a');
    std::thread t2(print_block, 20, 'b');
    t1.join();
    t2.join();
    return 0;
}
```
如果我们使用类型推断，可以指定 `std::unique_lock<std::mutex>` 对象为：

条件变量允许我们同步线程；它们只能与 `unique_lock` 对象配合使用。线程可以在条件变量上等待。当条件变量变化时，等待的线程会被通知。以下示例展示了条件变量的标准用法。在示例中，我们想要向银行账户存款然后取款。显然，取款之前必须先存款。

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
std::mutex mu;
std::condition_variable cv;
size_t balance = 0; // shared resource
void deposit(size_t amt) {
    mu.lock();
    balance += amt;
    mu.unlock();
    cv.notify_one();
}
void withdraw(size_t amt) {
    std::unique_lock<std::mutex> lock(mu);
    cv.wait(lock, [] { return balance > 0; });
    balance -= amt;
    lock.unlock();
}
int main() {
    std::thread t1(deposit, 500);
    std::thread t2(withdraw, 400);
    t1.join();
    t2.join();
    std::cout << "final balance: " << balance << std::endl;
    return 0;
}
```
注意：条件变量的使用需要 `unique_lock`。在 `withdraw` 函数中，我们首先尝试锁定互斥锁。如果无法锁定，则保持等待。如果 `cv.wait()` 的条件不满足，互斥锁会被释放并继续等待。如果条件变量对象发送通知（`cv.notify_one()`），我们再次尝试获取锁。如果无法获取锁，则保持等待。如果获取了锁，则再次测试条件变量谓词。在 `deposit` 函数中，线程等待获取锁。如果获取了锁，执行存款。接下来释放锁。然后通知一个等待线程（`notify_one`）或所有等待线程（`notify_all`）。

## 线程本地存储

线程可以维护私有的数据。这种数据被称为线程本地数据或线程本地存储。每个线程本地变量的作用域限于创建它的线程。线程本地变量的行为类似于静态变量，只要线程存在它们一直存在。当线程需要这种存储时就会创建，也就是说存储是按需创建的。存储限定 `thread_local` 用于创建线程本地变量。

这是一个线程本地存储的示例：

```cpp
#include <iostream>
#include <string>
#include <thread>
#include <mutex>
std::mutex mu;
thread_local std::string s {"hello "};
void greet(std::string id)
{
    std::lock_guard<std::mutex> lock(mu);
    s = s + id;
    std::cout << s << std::endl;
}
int main()
{
    std::thread t1(greet, "t1");
    std::thread t2(greet, "t2");
    std::thread t3(greet, "t3");
    t1.join();
    t2.join();
    t3.join();
}
// output
hello t1
hello t2
hello t3
```

## C++ 标准库：std::tuple

`tuple` 是一种可以存储任意数量异构类型项目的数据结构：

```cpp
#include <string>
#include <tuple>
std::tuple<int, std::string, float> t1(5, "hello world", 5.3);
```

这创建了一个给定类型和值的 `tuple`。`tuple` 也可以在没有任何值的情况下构造：

```cpp
std::tuple<int, std::string, float> t2;
```

**注意：** 通常 STL 容器只能存储非引用的值。与其它 STL 容器不同，`tuple` 有一个特殊特性，它可以存储引用。

### Tuple 赋值

我们可以如下所示进行 tuple 拷贝赋值：

```cpp
std::tuple<int, std::string, float> t1{5, "hello", 5.5};
std::tuple<int, std::string, float> t2;
t2 = t1;
```

赋值运算符执行逐成员拷贝。

## 获取 Tuple 元素

我们可以通过如下方式提取 `tuple` 的成员：

```cpp
#include <iostream>
#include <string>
#include <tuple>
```

```cpp
int main() {
    std::tuple<int, std::string, double> t1(5, "hello world", 5.3);
    int x0 = std::get<0>(t1);
    std::string x1 = std::get<1>(t1);
    float x2 = std::get<2>(t1);
    std::cout << x0 << " " << x1 << " " << x2 << std::endl;
    return 0;
}
```

`std::get` 函数返回一个元组值的引用。`std::get<<i>>` 函数中的索引 `i` 必须是一个编译时常量。

相同类型的元组可以按字典序进行比较：

```cpp
if (t2 < t1) {
    ...
}
```

### 元组拼接

元组可以进行拼接：

```cpp
std::tuple<int, std::string, float> t1(5, "hello", 5.5);
std::tuple<std::string, char> t2;
t3 = std::tuple_cat(t1, t2);
```

`t3` 是一个类型为 `<int, string, float, string, char>` 的元组

### 设置元组元素的值

`std::get<<i>>(foo)` 返回元组中第 i<sup>th</sup> 个元素的引用。我们可以通过以下方式设置第 i<sup>th</sup> 个元素：

```cpp
std::get<<i>>(my_tuple) = "hello world";
```

## 元组类型特质 (Tuple Type Traits)

我们可以通过以下方式获取元组的大小和元组成员的类型：

```cpp
// 获取元组 t3 的大小
auto tsize = std::tuple_size<decltype(t3)>::value;
// 获取元组成员的类型
auto tuple_t = std::tuple_element<1, decltype(t3)>::type;
```

## std::pair

`pair` 是 `std::tuple` 的一种特殊情况，拥有两个元素。`std::pair` 定义如下：

```cpp
template <class T1, class T2>
struct pair;
```

## C++ 标准库: std::tie

注意：请先查看 `std::tuple`

模板 `std::tie` 创建一个元素均为引用的元组。`std::tie` 的语法为：

```cpp
template < class T1, class T2, class T3 >
tuple(T1&, T2&, T3&) tie( T1, T2, T3 ) noexcept;
```

以下示例使用 `std::tie` 创建了一个元组：

```cpp
#include <iostream>
#include <string>
#include <tuple>
int main() {
    int x = 5;
    std::string y = "hello world";
    double z = 6.8;
    std::tuple<int, std::string, double> mytuple;
    // 将引用赋值给 my_tuple
    mytuple = std::tie(x, y, z);
    std::cout << "tuple (0): " << std::get<0>(mytuple) << std::endl;
    std::cout << "tuple (1): " << std::get<1>(mytuple) << std::endl;
    std::cout << "tuple (2): " << std::get<2>(mytuple) << std::endl;
    return 0;
}
```

输出：
tuple (0): 5
tuple (1): hello world
tuple (2): 6.8

元组 `mytuple` 包含对 `x`、`y` 和 `z` 的引用。更改 `x`、`y` 或 `z` 会改变 `mytuple`，反之亦然。

我们可以通过使用 `std::ignore` 作为元素值来忽略 `std::tie` 函数中的元素。

## 解析元组

我们也可以使用 `std::tie` 将元组解放到变量中：

```cpp
#include <iostream>
#include <string>
#include <tuple>
int main() {
    int x;
    std::string y;
    double z;
    std::tuple<int, std::string, double, int> mytuple;
    // 给 mytuple 赋值
    mytuple = {5, "hello world", 0.67, 0};
    // 解析元组
    std::tie(x, y, z, std::ignore) = mytuple;
    std::cout << "x: " << x << std::endl;
    std::cout << "y: " << y << std::endl;
    std::cout << "z: " << z << std::endl;
    return 0;
}
// 输出
x: 5
y: hello world
z: 0.67
```

## C 和 C++ 程序的内存布局

典型的 C/C++ 程序在内存中包含以下部分：

- 代码段 (Text Segment)
- 数据段 (Data Segment)
- BSS 段 (BSS Segment)
- 堆段 (Heap Segment)
- 栈段 (Stack Segment)

![](img/dbc91000ed9a70eff6930bb93f194ab_532_0.png)

**代码段 (Text Segment)** 也称为 Code Segment，包含了将执行的机器语言代码。通常该部分是共享且只读的。

**数据段 (Data Segment)** 也称为初始化数据段，包含已初始化的全局变量静态变量。

**BSS 段 (BSS Segment)** 也称为未初始化数据段。在程序启动前，操作系统会将其初始化为零。

**堆段 (Heap Segment)**：程序使用 `malloc`、`calloc`、`realloc` 或 `new` 分配动态内存。内存向下增长。

**栈段 (Stack Segment)**：由栈指针管理，存储局部变量和函数参数。栈段的行为类似于后进先出 (`LIFO`)，当栈指针遇到堆时耗尽。我们可以通过以下代码获取程序的内存布局：

```c
#include <stdio.h>
/* BSS 段中的未初始化变量 */
int global;
// 存储在栈上的参数
int Foo(int z) {
    // 存储在数据段的静态变量
    static int i = 100;
    // 存储在栈上的局部变量
    int x = 5;
    // 存储在栈上的返回值
    return x;
}
int main() {
    // 堆上的动态分配
    float* y = malloc;
    free(y);
}
```

可以通过命令获取此程序的内存布局：
```bash
gcc -c -o memory-layout memory.c
```

## C++ 编译器

### GNU C++ 版本
```bash
g++ --version
```

### gcc 和 g++ 的区别

`GCC` 或 GNU Collection 指编译器支持的所有不同语言。

```bash
gcc 是 GNU 编译器
g++ 是 GNU C++ 编译器
```

- `gcc` 分别将 `*.c` 和 `*.cpp` 文件编译为 C 和 C++ 文件。
- `g++` 会编译 `*.c` 和 `*.cpp` 文件，但会将它们视为 C++ 文件。
- 如果我们使用 `g++` 链接由编译器创建的对象文件，它会自动链接 C++ 库（`gcc` 不这样做）。

### 编译并运行程序

```bash
g++ -a helloworld.cpp foo.cpp bar.c
```

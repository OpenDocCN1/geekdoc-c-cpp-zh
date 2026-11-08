

```cpp
std::string message = std::format("The answer is {}.", 42);
```

std::format 使用 Python 的格式化语法。以下示例展示了一些典型用例：

- 格式化并使用位置参数

```cpp
std::string s = std::format("I'd rather be {1} than {0}.", "right", "happy");
// s == "I'd rather be happy than right"
```

- 以安全方式将整数转换为字符串

```cpp
memory_buffer buf;
std::format_to(buf, "{}", 42);      // replaces itoa(42, buffer, 10)
std::format_to(buf, "{:x}", 42);    // replaces itoa(42, buffer, 16)
```

- 格式化用户定义类型

### 3.3.5 日历和时区

来自 C++11 的 chrono 库[^5] 扩展了日历和时区功能。日历由表示年、月、星期几以及某月第 n 个星期几的类型组成。这些基本类型可以组合成复杂类型，例如 year_month、year_month_day、year_month_day_last、year_month_weekday 和 year_month_weekday_last。运算符 "/" 被重载，以便方便地指定时间点。此外，我们获得了新的字面量：d 表示一天，y 表示一年。

时间点可以在各种时区中显示。由于扩展了 chrono 库，以下用例现在很容易实现：

- 以特定格式表示日期
- 获取某月的最后一天
- 获取两个日期之间的天数
- 在各种时区中打印当前时间

以下程序显示不同时区中的本地时间。

`std::atomic_flag`⁴ 类型的值是一种原子布尔值。它有一个清除状态和设置状态。为简单起见，我将清除状态称为 `false`，将设置状态称为 `true`。`clear()` 成员函数使你可以将其值设置为 `false`。使用 `test_and_set()` 成员函数，你可以将值设置为 `true` 并获取先前的值。没有成员函数用于查询当前值。这在 C++20 中会改变，因为 `std::atomic_flag` 有一个 `test()` 方法。

此外，`std::atomic_flag` 可以通过成员函数 `notify_one()`、`notify_all()` 和 `wait()` 用于线程同步。在 C++20 中，通知和等待可用于 `std::atomic` 和 `std::atomic_ref` 的所有部分特化和完全特化。特化可用于布尔值、整数、浮点数和指针。

### 3.4.2 信号量

信号量是一种同步机制，用于控制对共享资源的并发访问。计数信号量（例如 C++20 中新增的信号量）是一种特殊信号量，其初始计数器大于零。计数器在构造函数中初始化。获取信号量使计数器递减，释放信号量使计数器递增。如果线程在计数器为零时尝试获取信号量，该线程会阻塞，直到另一个线程通过释放信号量使计数器递增。

### 3.4.3 闩锁和屏障

闩锁和屏障是简单的线程同步机制，使一些线程能够阻塞直到计数器变为零。这两种同步线程的机制之间有什么区别？`std::latch` 只能使用一次，但 `std::barrier` 可以多次使用。`std::latch` 适用于管理多个线程执行一个任务；`std::barrier` 适用于管理多个线程重复执行任务。此外，`std::barrier` 可以在每次迭代中调整计数器。

以下内容基于提案 N4204⁵ 中的代码片段。我修正了一些拼写错误并重新格式化了它。

**使用 `std::latch` 进行线程同步**

```cpp
void DoWork(threadpool* pool) {
  std::latch completion_latch(NTASKS);
  for (int i = 0; i < NTASKS; ++i) {
    pool->add_task([&] {
      // perform work

      completion_latch.count_down();
    });
  }
  // Block until work is done
  completion_latch.wait();
}
```

⁴ https://en.cppreference.com/w/cpp/atomic/atomic_flag

⁵ http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4204.html

`std::latch` 的计数器 `completion_latch` 被设置为 `NTASKS`（第 3 行）。线程池执行 `NTASKS` 个作业（第 4 至 10 行）。每个作业结束时，计数器递减（第 8 行）。运行函数 `DoWork` 的线程在第 12 行阻塞，直到所有任务完成。

### 3.4.4 协作式中断

得益于 `std::stop_token`，`std::jthread` 可以被协作式中断。

**中断 `std::jthread`**

```cpp
int main() {
    std::cout << '\n';

    std::jthread nonInterruptible([]{
        int counter{};
        while (counter < 10){
            std::this_thread::sleep_for(0.2s);
            std::cerr << "nonInterruptible: " << counter << '\n';
            ++counter;
        }
    });

    std::jthread interruptible([](std::stop_token stoken){
        int counter{};
        while (counter < 10){
            std::this_thread::sleep_for(0.2s);
            if (stoken.stop_requested()) return;
            std::cerr << "interruptible: " << counter << '\n';
            ++counter;
        }
    });

    std::this_thread::sleep_for(1s);

    std::cerr << '\n';
    std::cerr << "Main thread interrupts both jthreads" << std::endl;
    nonInterruptible.request_stop();
    interruptible.request_stop();

    std::cout << '\n';
}
```

主程序启动两个线程：nonInterruptible 和 interruptible（第 5 行和第 14 行）。只有线程 interruptible 获得 `std::stop_token`，它在第 18 行使用该令牌检查是否被中断。如果发生中断，lambda 会立即返回。调用 `interruptible.request_stop()` 会触发该线程的取消。调用 `nonInterruptible.request_stop()` 没有任何效果。

![](img/c60a87adb7f61e2e82071d081bbb389a_43_0.png)

### 3.4.5 `std::jthread`

`std::jthread` 代表可汇合线程。`std::jthread` 通过自动汇合已启动的线程来扩展 `std::thread`。`std::jthread` 也可以被中断。

[^10]: https://en.cppreference.com/w/cpp/thread/jthread

std::jthread 被加入 C++20 标准，是因为 std::thread 的行为不直观。如果 std::thread 仍可汇合，则其析构函数中会调用 std::terminate()。如果既没有调用 thr.join() 也没有调用 thr.detach()，则线程 thr 可汇合。

**线程 thr 仍可汇合**

```cpp
int main() {
    std::cout << '\n';

    std::cout << std::boolalpha;
    std::thread thr{[] { std::cout << "Joinable std::thread" << '\n'; }};
    std::cout << "thr.joinable(): " << thr.joinable() << '\n';

    std::cout << '\n';

}
```

![](img/c60a87adb7f61e2e82071d081bbb389a_44_0.png)

仍可汇合线程时的 std::terminate

程序的两次执行都会终止。在第二次运行中，线程 thr 有足够时间显示其消息："Joinable std::thread"。

在修改后的示例中，我使用 C++20 标准中的 std::jthread。

[^11]: https://en.cppreference.com/w/cpp/error/terminate

**线程 thr 自动汇合**

```cpp
int main() {
    std::cout << '\n';

    std::cout << std::boolalpha;
    std::jthread thr([] { std::cout << "Joinable std::jthread" << '\n'; });
    std::cout << "thr.joinable(): " << thr.joinable() << '\n';

    std::cout << '\n';

}
```

现在，thr 会在必要时在其析构函数中自动汇合。

![](img/c60a87adb7f61e2e82071d081bbb389a_45_0.png)

线程 thr 自动汇合

### 3.4.6 同步输出流

在 C++20 中，我们获得了同步输出流。当更多线程在没有同步的情况下并发写入 std::cout 时会发生什么？

**对 std::cout 的未同步写入**

```cpp
void sayHello(std::string name) {
    std::cout << "Hello from " << name << '\n';
}

int main() {
    std::cout << "\n";

    std::jthread t1(sayHello, "t1");
    std::jthread t2(sayHello, "t2");
    std::jthread t3(sayHello, "t3");
    std::jthread t4(sayHello, "t4");
    std::jthread t5(sayHello, "t5");
    std::jthread t6(sayHello, "t6");
    std::jthread t7(sayHello, "t7");
    std::jthread t8(sayHello, "t8");
    std::jthread t9(sayHello, "t9");
    std::jthread t10(sayHello, "t10");

    std::cout << '\n';
}
```

你可能会得到一团乱麻。

![](img/c60a87adb7f61e2e82071d081bbb389a_46_0.png)

对 std::cout 的未同步写入

将函数 sayHello 中的 std::cout 切换为 std::osyncstream(std::cout)，就能把混乱变为和谐。

**对 std::cout 的同步写入**

```cpp
void sayHello(std::string name) {
    std::osyncstream(std::cout) << "Hello from " << name << '\n';
}
```


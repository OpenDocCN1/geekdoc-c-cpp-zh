
```cpp
void div(int x) {
    std::lock_guard lk2(mx_); // inner
    value_ /= x;
}
void mulDiv(int x, int y) {
    std::lock_guard lk3(mx_); // outer
    mul(x);
    div(y);
}
};
int main() {
    MulDiv m{42}; // 3*7*2*5
    m.mulDiv(5, 15);
    std::cout << m.value_ << '\n'; // Output: 14
}
```

**清单 29.27** 当互斥量需要被多次锁定时，必须采取预防措施。

这里，调用 `mulDiv` 会通过 `lk3` 使用简单的 `lock_guard` 锁定 `mx_`。从现在起，没有其他线程能对这个实例 `m` 执行计算。其他线程必须等待，因为每个方法都会立即获取锁。主线程随后进入 `mul`。在那里，`lk1` 通过 `lock_guard` 在同一线程中再次锁定同一个互斥量；对于简单的 `mutex` 来说，这将是错误，但对于 `recursive_mutex` 则是允许的。一旦退出 `mul`，这个内部锁会再次释放。然而，这对于可能已经在等待继续执行的其他线程来说还不够。只有当外部的 `lk3` 释放其锁时，其他线程才能继续。

如果你正在编写一个程序，并且认为 `recursive_mutex` 是解决方案，这通常表明你应该重新考虑你的设计。在类中，互斥量通常保护封装的数据。如果公共方法调用另一个公共方法，你就需要递归互斥量。然而，锁之所以存在，通常是因为在临界区中类的“不变量”被破坏了。在实例处于不正确状态时调用公共方法，这听起来是个好主意吗？不。通常更好的做法是定义一个私有方法，然后由两个公共方法调用它。你通常在公共层面建立锁，而私有方法可以假设锁已经存在。

## 29.4 在自身存储中使用“thread_local”

并非所有内存对所有线程都是可见的。如果在运行中的线程中使用 `thread_local` 定义一个变量，只有创建它的线程才能看到它。当线程终止时，该变量也会被移除。

```cpp
// https://godbolt.org/z/j8W7GjTf
#include <iostream>
#include <string>
#include <thread>
#include <mutex>

thread_local unsigned int usage = 0;
static std::mutex cout_mutex;

void use(const std::string thread_name) {
    ++usage;
    std::lock_guard lock(cout_mutex); // Protect output
    std::cout << thread_name << ": " << usage << '\n';
}

int main() {
    std::jthread a(use, "a"), b(use, "b");
    use("main");
}
```

**清单 29.28** 仅用于当前线程的内存。

你将得到以下输出（可能按其他顺序）：

```
main: 1
b: 1
a: 1
```

这里的 1 表示线程 a、b 和 main 各自拥有自己的 usage 变量，并且不必与其他线程共享。否则，最后会显示 3。

你可以像使用 `static` 或 `extern` 一样使用 `thread_local`，但不能与它们结合使用。在函数内，该变量每个线程只初始化一次，就像 `static` 在只有一个线程时那样：

```cpp
void func() {
    thread_local vector<int> data{};
    // ...
}
```

## 29.5 使用“condition_variable”等待事件

使用互斥量和锁，你可以做很多事，它们构成了线程工作所需的基础。然而，有时处理互斥量和锁很繁琐。通过 `call_once`，你已经看到了另一种方式，标准库将基本构建块组合成新的东西供你使用。这里我还会介绍一些其他高级工具。

多线程的一个典型场景是：一个线程产生数据，另一个线程等待数据准备好再处理。这两者可以通过条件变量 `condition_variable` 进行通信。

```cpp
int main() {
    // a producer:
    std::jthread thProd{produce, 1'000};
    // three consumers
    std::jthread thCon1{consume, '[', ']'};
    std::jthread thCon2{consume, '<', '>'};
    std::jthread thCon3{consume, '{', '}'};
    // wait and finish
    thProd.join();
    thCon1.join(); thCon2.join(); thCon3.join();
    std::cout << '\n';
}
```

**清单 29.29** 两个线程通过条件变量进行通信。

这里，在函数 `produce` 中有一个生产者线程 `thProd`，在函数 `consume` 中有三个消费者线程 `thCon1` 到 `thCon3`。后者应输出数据。为了区分哪个线程处理输出，我使用了不同的括号对，并将它们作为参数传递给 `consume` 函数。

产生的数据以生产者能够交付的速度被放入全局队列 `g_data`。因此，可能会出现 `g_data` 的填充速度快于结果被消费的速度，但也可能出现消费者清空 `g_data` 后确实需要等待新结果的情况。以质数计算为例，它一开始运行很快，然后逐渐变慢。然而，1'000 甚至 1'000'000 在现代计算机上太小，无法察觉。为了输出更少的数字，你可以添加另一个测试来检查是否存在质数六元组。

> 参见 https://en.wikipedia.org/wiki/Prime_tuple.

### 条件变量的优点

`condition_variable` 的设计目的是尽可能短暂地持有必要的锁。因此，在一次 `wait()` 调用期间，lambda 的条件可能会被多次检查。为此，互斥量会被锁定，但总是立即再次解锁，以允许其他线程处理共享数据结构。

手工重建这一过程是费力的、容易出错的，或者很可能导致次优代码。你应该使用 `condition_variable`。

### 29.5.2 同步输出

如果你选择 1'000 作为限制，程序输出大致如下：

```
[3] <5> [11] {7} {13} [19] {23} [29] <17> {31} <41> [47] {43}
{53} <59> [61] {71} {73} [79] <83> {89} [97] <101> {103} [107]
<109> ... <881> [887] [919] <907> [911] [929] [941] [947] <937> [953]
[967] <971> [977] [997] {983} <991>
```

你可以从不同的括号看出，这些数字确实由不同的线程输出。你还可以看到，数字并不总是按正确顺序出现。这是一个有意为之的设计决定。通常，你希望数据尽快被消费。由谁消费、彼此之间的顺序如何，通常无关紧要。也许它们是来自互联网的独立工作任务。然而，如果输出顺序很重要，请使用不同的机制。

对于输出，你会看到输出并非直接通过 `cout` 进行，而是使用类型为 `osyncstream` 的实例 `osync`：

```cpp
std::osyncstream osync(std::cout);  // Synchronize output
osync << l << prim << r << ' ';
```

如果省略这一点，流在输出时可能会互相打断，输出将变得一团糟（准确地说，是`undefined`）。`osyncstream` 类的工作方式类似于 unique_lock，只是你不需要额外的互斥量。

还没有可用的 `osyncstream`？那就全局定义一个互斥量并使用 `unique_lock`。或者，你也可以先将需要保持在一起的输出收集到 `stringstream` 中，以便尽可能缩短持锁时间：

```cpp
std::mutex g_coutMx;
// ...
std::stringstream ss;
ss << l << prim << r << ' ';
std::lock_guard<std::mutex> l2{g_coutMx};
std::cout << ss.str();
```


### 列表 29.22 "MxStack"的"swap"。

在交换操作中，你需要锁定两个参数的互斥锁，以确保在交换期间没有其他线程将其中一个参数更改为不一致的状态。锁定两个互斥锁意味着死锁的风险。解决方案如下：

- 首先，使用函数 `lock(...)` 同时锁定两个互斥锁。
- 为了确保锁被自动释放，请使用 `lock_guard`，但你必须通过额外的参数 `adopt_lock` 指定互斥锁已经被锁定，在 `lock_guard` 构造函数不需要再次锁定。

如往常一样，`libre` 和 `lkli` 在离开临界区域时会释放它们的锁。

以下是关于该列表的通用说明：我按照通常惯用法实现了 `swap`——即一个 `friend` get函数——这样它就可以像自由函数 `swap(a,b)` 一样使用，而不是像方法 `swap(b)` 那样。这是函数与标准库协作得最好的方式。在 `swap` 内部，你应该首先像赋值一样检查 `swap(a,a)` 是否被直接或间接地调用，这会使得交换变得没有必要，甚至是危险的。

## 避免死锁的技巧

完全避免潜在的死锁是很困难的。然而，实现这一点至关重要。因此，仔细的考虑和测试是非常重要的——而且由于寻找与线程线程、特别是死锁相关的错误是一项非常困难的任务。

因此，这里有一些通用的技巧：

- 避免嵌套锁。
- 如果你已经持有一个锁，就不应该再获取另一个锁。通过这种方式，你可以完全避免基于锁的死锁。在实践中，你应该尽可能少地这样做。
- 不要要在持有锁时调用用户代码。
- 这源于上一个准则，因为你不知道用户提供的代码做了什么。这在实践中也并非总是可行的。
- 按照固定顺序建立你的锁。
- 当你在多个互斥锁上建立多个锁时，力求始终以相同的顺序执行。
- 定义锁的层级。
- 如果很难维持清晰、固定的锁顺序，请定义一个你或未来互斥锁的使用者应该遵守的层级。高层函数应该只锁定高层互斥锁并调用低层函数。低层函数应该只锁定低层互斥锁。
- 即使在不直接尝试锁定互斥锁的地方也要考虑死锁。
- 每只要涉及到等待，你就可能遇到死锁：`join()`、`互斥锁`、从其他地方正在写入的文件读取数据以及许多其他事情都会相互干扰。

## 29.2.7 使用 "unique_lock" 更灵活的锁定

虽然 `lock_guard` 提供了最简单的使用接口，但我们也可以使用更灵活的 `unique_lock`：

- `unique_lock{..., adopt_lock}`;
互斥锁已经锁定；只需负责解锁即可。
- `unique_lock{..., defer_lock}`
不要立即锁定互斥锁。稍后通过 `lk..`（不在互斥锁上！）或调用 `std::lock(lk)` 函数来处理。
- `unique_lock{..., try_to_lock}`
尝试锁定，如果不起作用，继续执行。

使用 `unique_lock` 代替 `lock_guard`，功能是完全相同的。巨大的区别是它可以临时不持有与其关联的互斥锁。类似于 `unique_ptr` 可以将其内容作为返回值或参数传递给另一个 `unique_ptr`，`unique_lock` 也可以对与其关联的互斥锁做同样的事情。你可以将互斥锁的锁权从方法或函数移出或传入。

```
https://cppbolt.org/z/e7rraPGx4
#include <thread>
#include <mutex>
#include <vector>
#include <numeric> // accumulate, iota
using std::mutex; using std::unique_lock;

std::vector<int> myData; // shared data
mutex myMutex;
unique_lock<mutex> prepareData() {
    unique_lock lk(myMutex); // lock
    myData.resize(1000);
```

```cpp
std::iota(myData.begin(), myData.end(), 1); // 1..1000
return lk1;
// Transfer lock
int processData() {
    unique_lock lk2 = prepareData(); // Lock transferred
    return std::accumulate(myData.begin(), myData.end(), 0);
}
```

## 列表 29.23 互斥锁是可以传递的。

在处处，对 `myData` 数据的处理分布在两个函数中。首先，使用 `lk1` 锁定了 `myMutex`。因此，没有人可以通过同样想要锁定 `myMutex` 的点；这并不新奇。在锁的保护下，`prepareData` 函数现在操作 `myData`，没有人可以干扰。如果 `lk1` 只是一个 `lock_guard`，锁将在退出 `prepareData()` 时被释放，其他人就可以更改 `myData`。但我还没有完成对 `myData` 的工作：我仍然想在调用者 `processData()` 中执行 `accumulate`。对 `myData` 的中间更改尚未完成。

由于使用了 `unique_lock`，锁从 `prepareData()` 处移出了。只有当 `lk2` 作用域结束时锁才会被释放。在 `lock_guard` 之后 `unique_lock` 在某些情况下使用 `unique_lock` 总是更好的，因为 `unique_lock` 它可以临时不持有与其关联的互斥锁。

使用 `unique_lock` 代替 `lock_guard`，在某些情况下，使用 `unique_lock` 来处理互斥锁是有益的。

## 29.3 锁的其他选项

### 29.3.1 使用 "once_flag" 和 "call_once" 仅调用一次

通常情况下，你不希望在第一次使用资源之前就创建它，因为该资源可能永远不会被使用。在这种情况下，你可以使用 `call_once` 来在第一次使用时初始化它。

```cpp
// https://cppbolt.org/z/TcsrefEPhh
#include <mutex>
#include <memory>
struct Connection {
    void csend(const char* data) {} // dummy
    const char* recv() {} // dummy
};
class Sender {
    std::shared_ptr<Connection> conn_;
    std::once_flag connInitFlag_;
    void open() {
        conn_.reset(new Connection());
    }
public:
    void send(const char* data) {
        std::call_once(connInitFlag_, &Sender::open, this); // method pointer
        conn_->csend(data);
    }
    const char* recv() {
        std::call_once(connInitFlag_, [this]{this->open();}); // lambda
        return conn_->recv();
    }
}
```

### 29.3.2 延迟初始化

通常情况下，你不希望在第一次使用资源之前就创建它，因为该资源可能永远不会被使用。在这种情况下，你可以使用延迟初始化在第一次使用时创建它。

```cpp
// https://cppbolt.org/z/3vcnGf
#include <mutex>
#include <memory>
struct BigData {
    void csend(const char* data) {} // dummy
    const char* recv() {} // dummy
};
std::shared_ptr<BigData> bigData;
std::once_flag bigInitFlag;
void initData() {
    bigData = std::make_shared<BigData>();
}
BigData& getData() {
    std::call_once(bigInitFlag, initData);
    return *bigData;
}
```

### 29.3.3 单例模式

第 13 章，列表 13.7 展示了延迟初始化的另一种方法：使用 Meyer 的单例模式。

> 这只是延迟初始化的一种方式

第 13 章，列表 13.7 展示了延迟初始化的另一种方法：使用 Meyer 的单例模式。

这里展示的带有 `shared_ptr` 和 `once_flag` 的示例更具适用性。你也可以将 `once_flag` 作为类的字段与资源一起使用。这样它们就以面向对象的方式封装在一起。

```cpp
// https://cppbolt.org/z/T7veha5
#include <mutex>
#include <memory>
struct Connection {
    void csend(const char* data) {} // dummy
    const char* recv() {} // dummy
};
class Sender {
    std::shared_ptr<Connection> conn_;
    std::once_flag connInitFlag_;
    void open() {
        conn_.reset(new Connection());
    }
public:
    void send(const char* data) {
        std::call_once(connInitFlag_, &Sender::open, this); // method pointer
        conn_->csend(data);
    }
    const char* recv() {
        std::call_once(connInitFlag_, [this]{this->open();}); // lambda
        return conn_->recv();
    }
}
```

### 列表 29.24 单线程的延迟初始化。

这种方法在多线程环境下是有问题的。如果两个线程同时调用 `getData()`，`bigData` 将被初始化两次。

```cpp
// https://cppbolt.org/z/3vcnGf
#include <mutex>
#include <memory>
struct BigData {
    void csend(const char* data) {} // dummy
    const char* recv() {} // dummy
};
std::shared_ptr<BigData> bigData;
std::once_flag bigInitFlag;
void initData() {
    bigData = std::make_shared<BigData>();
}
BigData& getData() {
    std::call_once(bigInitFlag, initData);
    return *bigData;
}
```

### 列表 29.25 多线程的延迟初始化。

这种方式，`getData` 可以在线程中被调用，标准库保证 `initData` 只会被调用一次。

就像你通过 `jthread{func, arg...}` 为 `func` 传递类似 `arg` 的额外参数一样。

如果这种方法语法看起来很令人生畏，你可以使用 lambda 表达式。我在 `recv` 中演示了这一点。你需要将其作为捕获变量在 lambda 中。仅用 `[]{open();}` 是不够的，因为默认情况下这些变量在 lambda 中是不可见的。

这两种调用方法是等价的。在现实世界中，你不应该在相关的 `call_once` 中使用不同的调用方式，因为这只会困扰你的读者，而且容易出错。

你现在可以顺利地在多个线程中使用同一个 `Sender` 实例（前提是多个线程同时从 `Connection` 发送和接收数据是可以接受的）。即使在存在多个线程的情况下，`conn_` 也只初始化一次。因此，`call_once` 将互斥锁的功能与布尔标志结合在了一起。

## 29.3.2 使用 "recursive_mutex" 锁

尝试锁定一个已经锁定的互斥锁将由于未定义行为而失败。在需要多次锁定互斥锁的稀有情况下，请使用 `recursive_mutex`。

你可以在一个线程内多次调用 `recursive_mutex` 的 `lock()` 方法。另一个线程必须等待它的 `lock()` 成功，这意味着你调用 `unlock()` 的次数必须等于调用 `lock()` 的次数。

你可以手动在互斥锁上调用 `lock()` 和 `unlock()`，也可以使用 `lock_guard` 或其他锁对象来帮助。

```
// https://godbolt.org/z/KPaoh4Gn
#include <mutex> // recursive_mutex
#include <iostream>
struct MulDiv {
    recursive_mutex mx;
    int value;
    explicit MulDiv(int value) : value{value} {}
    void lock(int x) {
        std::lock_guard lk1(mx_); // inner
        value_ = x;
    }
    void div(int x) {
        std::lock_guard lk2(mx_); // inner
        value_ = x;
    }
    void muldiv(int x, int y) {
        std::lock_guard lk3(mx_); // outer
        mul(x);
        div(y);
    }
};
int main() {
    MulDiv m(42); // 3*7*2 *5
    m.muldiv(5, 15);
    std::cout << m.value << '\n'; // Output: 14
}
```

### Listing 29.27 当互斥锁需要被多次锁定时，采取措施是必要的。

在这里，调用 `muldiv` 会通过 `lk3` 使用简单的 `lock_guard` 锁定 `mx_`。从现在起，没有其他线程可以对此实例 `m` 执行计算。其他线程必须等待，因为每个方法都会立即获取锁。随后主线程进入 `mul`。在那里，通过 `lk1` 的 `lock_guard` 在同一个线程中再次锁定了同一个互斥锁；对于普通的 `mutex` 来说这是一个错误，但对于 `recursive_mutex` 来说是允许的。一旦退出 `mul`，这个内层锁就会再次释放。然而，这对于可能已经在等待继续执行的其他线程来说是不够的。只有当外层的 `l3` 释放它的锁后，其他线程才能继续。

如果你正在编写一个你认为 `recursive_mutex` 是解决方案的程序，这通常意味着你应该重新考虑你的设计。在类中，互斥锁通常保护封装的数据。如果一个公共方法调用了另一个公共方法，你就需要递归互斥锁。然而，锁的出现通常是因为类的“不不变性”在临界区中被违反了。在实例处于错误状态时调用公共方法听起来是个好主意吗？不。通常定义一个私有方法并由两个公共方法调用它更好。你通常在公共级别建立锁，而私有方法可以假设锁已经存在。

## 29.4 使用 "thread_local" 在其自己的存储中

并不是所有内存对所有线程都可见。如果你在运行的线程中使用 `thread_local` 定义一个变量，只有创建它的线程才能看到。当线程终止时，该变量也会被移除。

```
// https://godbolt.org/z/1j8W7GjTf
#include <iostream>
#include <string>
#include <thread>
#include <mutex>
thread_local unsigned int usage = 0;
static std::mutex cout_mutex;
void use(const std::string thread_name) {
    ++usage;
    std::lock_guard lock(cout_mutex); // Protect usage
    std::cout << thread_name << " : " << usage << '\n';
}
int main() {
    std::thread a(use, "a"), b(use, "b");
    use("main");
}
```

### List 29.28 仅限当前线程的内存。

你将得到以下输出（顺序可能）：

```
main: 1
b: 1
a: 1
```

`1` 显示每个线程 a、b 和 main 都拥有自己的 `usage` 变量，不需要与其他线程共享。否则，在最后会显示 `3`。

你使用 `thread_local` 就像使用 `static` 或 `extern` 一样，并且不能与这些结合。在函数内部，该变量每个线程初始化一次，就像 `static` 在只有一个线程时执行的那样：

```
void func() {
    thread_local vector<int>
```

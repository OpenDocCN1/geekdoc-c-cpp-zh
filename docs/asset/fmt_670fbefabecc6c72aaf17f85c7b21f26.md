
通过析构函数进行连接，因此顺序与构造顺序相反。在这里我们先等待 `t2`，再等待 `t1`。程序的线程共享单个地址空间。在此这一点上，线程与进程不同，进程不共享数据。由于线程共享地址空间，它们可以通过共享对象进行通信。这种通信通常由锁或其他机制控制，以防止数据竞态（对变量的无控制访问）。

编写并发任务可能是复杂的。考虑任务 `f`（一个函数）和 `F`（一个函数对象）的可能实现：

```cpp
void f() {
    cout << "Hello";
}

struct F {
    void operator() { cout << "World!"; }
}
```

这是一个错误的错误示例：`f` 和 `F()` 分别使用 `cout` 而没有任何形式的同步。结果输出将是不可预测，并在不同的执行之间可能变化，因为单个任务的执行顺序没有定义。程序可能会产生奇怪的输出。为了避免此类输出问题，只让一个线程使用流（§17.5）。

在定义并发程序的任务时，我们的目标是保持任务分离，除非它们以明显的方式通信。考虑并发任务的最简单方法是将其视为调用者并发运行的函数。为了实现这一点，我们只需要传递参数、获取结果，并确保中间没有数据数据（数据竞态）。

## 18.2.1 传递参数

通常，任务需要数据来处理。我们可以很容易地将数据（或数据的指针或引用）作为参数传递。考虑：

```cpp
void f(vector<double>& v); // 函数：对 v 进行操作

struct F {
    vector<double>& v; // 函数对象：对 v 进行操作
    F(vector<double>& vv) : v(vv) {}
    void operator()(); // operator() 的应用
}

int main() {
    vector<double> some_vec = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    vector<double> vec2 = {10, 11, 12, 13, 14};
    thread t1(f, ref(some_vec)); // f(some_vec) 在单独线程中执行
    thread t2(F(vec2)); // F(vec2) 在单独线程中执行
}
```

`F(vec2)` 在 `F` 的 `vector` 中保存了对参数的引用。`F` 现在可以使用该 `vector`，并希望在 `F` 执行期间没有其他对 `vec2` 的访问。按值传递将消除该风险。

通过使用 `ref(some_vec)` 进行初始化使用了线程变长模板构造函数，它可以接受任意序列的参数（§8.4）。`ref` 是来自 `<functional>` 的类型，不幸的是，需要它来欺骗变长模板将 `some_vec` 作为引用而不是对象。如果没有 `ref()`，`some_vec` 将按值传递。编译器检查第一个参数在给定后续参数的情况下调用，并构建传递给线程的必要函数。因此，如果 `F::operator()` 和 `f` 执行相同的算法，任务的处理方式等相等：在两种情况下，都构造了一个用于执行的函数。

## 18.2.2 返回结果

在示例 18.2.1 中，我通过非常量引用传递参数。只有当我预期任务修改所引用数据的值时才会这样做（§1.7）。这是一种微妙但并不常见的返回结果的方法。不那么隐晦的技术是以常量引用传递输入数据，并将存放结果的位置作为单独参数传递：

```cpp
void f(const vector<double>& v, double* res); // 获取 v；将结果存放在 *res

class F {
public:
    F(const vector<double>& vv, double* p) : v(vv), res(p) {} // 将结果存放在 *res
    void operator()();
private:
    const vector<double>& v; // 输入源
    double* res; // 输出目标
};

double g(const vector<double>&); // 使用返回值
```

## 18.2.2 节

## 返回结果 241

```cpp
void user(vector<double>& vec1, vector<double> vec2, vector<double> vec3)
{
    double res1;
    double res2;
    double res3;
    thread t1(f(vec1),&res1); // 在单独线程中执行
    thread t2(f(vec2),&res2); // 在单独线程中执行
    thread t3 ([&]{res3 = g(vec3); }); // 通过引用捕获局部变量
    t1.join(); // 使用结果前等待
    t2.join();
    t3.join();
    cout << res1 << " << " << res2 << " << " << res3 << "\n";
}
```

在这里，`f(vec1)` 将 `vec1` 的常量引用作为参数传递给 `t1`。这样做是有效的，而且这种技术非常常见，但我认为通过这种方式返回结果并不完美优雅，因此我将在 §18.5.1 中回到这个主题。

## 18.3 共享数据

有时任务需要共享数据。在这种情况下，必须对数据的访问进行同步，以确保同一时间只有一个任务可以访问数据。经验丰富的程序员会识别出这种简化（例如，许多任务同时读取不可变数据没有问题），但请考虑如何确保同一时间只有一个任务拥一组对象。

### 18.3.1 互斥锁与锁

互斥锁（`mutex`，即“互斥对象”）是线程间通用数据共享的关键元素。线程通过 `lock()` 操作获取互斥锁：

```cpp
mutex m;
int sh; // 控制互斥锁
// 共享数据
void f()
{
    scoped_lock lck(m); // 获取互斥锁
    sh += 7; // 操作共享数据
} // 隐式释放互斥锁
```

`lck` 的类型被推断为 `scoped-lock-mutex(7.2.3)`。`scoped_lock` 通过调用 `m.lock()` 获取互斥锁。如果另一个线程已经获取了互斥锁，该线程将等待（“阻塞”），直到另一个线程完成访问。一旦完成对共享数据的访问，`scoped_lock` 通过调用 `m.unlock()` 释放互斥锁。当互斥锁被释放时，等待它的线程将恢复执行（“被唤醒”）。互斥和锁定设施可以在 `<mutex>` 中。

## 242 并发 第 18 章

注意 RAII（§6.3）。使用资源句柄（如 `scoped_lock` 和 `unique_lock`（§18.4））比显式地锁定和解锁互斥锁更简单、也更安全得多。共享数据与互斥锁之间的对应关系依赖于约定：程序员必须知道哪个互斥锁应该保护哪部分数据。显然，这是容易出错的，同样显然，我们试图通过各种语言使这种对应关系变得清晰。例如：

```cpp
class Record {
public:
    mutex rm;
};
```

不需要天才也能知道，对于名为 `rec` 的 `Record`，你应该在访问 `rec` 之前获取 `rec.rm`，尽管注释或更好的命名可能对读者有所帮助。

为了执行某些操作而同时访问多个资源。这可能导致死锁。例如，如果 `thread1` 获取了 `mutex1` 并尝试获取 `mutex2`，而 `thread2` 获取了 `mutex2` 然后尝试获取 `mutex1`，那么两者都永远无法继续执行。`scoped_lock` 通过同时获取多个互斥锁来帮助我们：

```cpp
void f() {
    scoped_lock lck(mutex1,mutex2,mutex3); // 获取所有三个锁
    // ...操作共享数据...
} // 隐式释放所有互斥锁
```

这个 `scoped_lock` 只有在获取了所有互斥锁参数后才会继续，并且在持有互斥锁时永远不会阻塞（“睡眠”）。`scoped_lock` 的析构函数确保在线程离开作用域时释放互斥锁。

通过共享数据进行通信是非常底层的。特别是，程序员必须设计方法来知道哪些操作是有效的且尚未被各种任务完成。在这方面，使用共享数据的方法优于调用和返回的方法。另一方面，当可用大量数据时，共享数据……确实可以是，但锁定和解锁是相对昂贵的操作。另一方面，现代机器非常擅长复制数据，尤其是紧凑的数据，如 `vector`。所以，不要在没有思考、可能没有测量的情况下为了“效率”而选择共享数据进行通信。

基础互斥锁允许一个线程访问数据。共享数据最常见的方式之一是在许多读取者和一个写入者之间。这种“读者-写者锁”模式被 `shared_mutex` 支持。读取者将获取“共享”互斥锁，以便其他读取者仍然可以访问，而写入者将要求排斥访问。例如：

### 18.3.1 节

```cpp
shared_mutex mx; // 一个可以共享的互斥锁
void reader()
{
    shared_lock lck(mx); // 与其他读取者共享访问
    // ... 读取 ...
}
```

```cpp
void writer()
{
    unique_lock lck(mx); // 需要排斥（唯一）访问
    // ... 写入 ...
}
```

### 18.3.2 原子

互斥锁是一种涉及操作系统的重量级机制。它允许任意数量的工作免于数据竞态。然而，有一种简单得多且廉价的机制来实现同样的事情：原子性（`atomic`）。例如，经典双重检查锁定的一种简单变体：

```cpp
mutex mut;
atomic<bool> init_x; // 初始化为 false
// 需要的变量
```
if (!init_x) {
    lock_guard lck(mut);
    // ...非复杂的初始化
    init_x = true;
}
```

原子性为我们避免了大多数数据竞态。如果 `init_x` 不是原子的，就会频繁失败。使用 `lock_guard` 就足够了。

## 18.4 等待事件

有时线程需要等待某些外部事件，例如另一个线程完成任务或时间流逝。简单的“事件”就是时间流逝。使用 `<chrono>` 中的时间设施可以写：

```cpp
using namespace chrono; // 查看 16.2
auto t0 = high_resolution_clock::now();
this_thread::sleep(milliseconds(20));
auto t1 = high_resolution_clock::now();
```

```cpp
cout << duration_cast<nanoseconds>(t1-t0).count() << " nanoseconds passed!\n";
```

我不需要等待线程；默认情况下，`this_thread` 可以等待。使用外部事件进行通信的基础支持由 `<condition_variable>` 提供的。`condition_variable` 是一种允许等待其他的机制。特别是，它允许线程等待某个条件（通常是其他线程工作的结果）发生。

使用条件变量支持许多优雅且高效的形式，但可能很复杂。为了简单起见，我使用了队列以及避免该队列竞态条件的机制。队列对生产者和消费者全局可见

```cpp
class Message {
  // 要通信的对象
  // ...
};
```

```cpp
queue<Message> mqueue;
condition_variable mcond;
mutex mutex;
// 消息队列
// 通信事件的变量
// 用于同步访问
```

`queue`、`condition_variable` 和 `mutex` 类型由标准库提供。`consumer()` 等待并处理消息：

```cpp
void consumer() {
  while(true) {
    unique_lock lck(mutex);
    mcond.wait(lck, []{ return !mqueue.empty(); });
    // 获取锁
    // 释放锁并等待；
    // 唤醒后重新获取锁
    // 只有当 mqueue 不为空时唤醒
    auto m = mqueue.front();
    mqueue.pop();
    lck.unlock();
    // 获取消息
    // ... 处理 m
  }
}
```

在这里，通过 `unique_lock(mutex)` 显式地保护对队列和条件变量的操作。等待 `condition_variable` 会释放其锁参数，直到等待结束（即队列不为空），然后重新获取它。显式检查条件（这里是 `!mqueue.empty()`）防止了在唤醒后发现某些其他任务已经“先了一一步”导致条件不再成立。

## 第18.4节 等待事件

我使用 `unique_lock` 而不是 `scoped_lock` 有两个原因：

- 我们需要将锁传递给 `condition_variable` 的 `wait()`。`scoped_lock` 无法被移动，但 `unique_lock` 可以。
- 我们希望在处理消息之前解锁保护条件变量的互斥锁。`unique_lock` 提供了如 `lock()` 和 `unlock()` 等操作，用于对同步进行低级控制。

另一方面，`unique_lock` 只能处理单个互斥锁。相应的生产者看起来如下：

```cpp
void producer() {
    while(true) {
        Message m;
        // 填充消息 ...
        scoped_lock lck(mutex); // 保护操作
        mqueue.push(m);
        mcond.notify_one(); // 通知
    } // 释放互斥锁（在作用域结束时）
}
```

## 18.5 任务通信

标准库提供了一些设施，允许程序员在任务的概念层面进行操作（而不是可能并发地），而不是直接在线程和锁的较低层面进行：

- `future` 和 `promise` 用于从在单独线程启动的任务返回值。
- `packaged_task` 用于帮助启动任务并连接返回结果的机制。
- `async(future)` 以非常类似于调用函数的方式启动任务。

这些设施可以在 `<future>` 中。

### 18.5.1 future 和 promise

`future` 和 `promise` 的重要点在于，它们允许在两个任务之间传输值，而不需要排斥性使用锁；“系统”高效地实现了这种传输。基本思想是：当一个任务想要将值传递给另一个任务时，它将值放入 `promise` 中。通过某种方式，实现使得该值出现在对应的 `future` 中，并从那里读取（通常由任务的启动者读取）。我们可以用图表来表示这一点：

![](img/c00e25f90ff6ca6a5619b7dcdafeb9db_257_0.png)

如果我们有一个 `future<X> fx`，我们可以从它 `get()` 获取一个 `X` 类型的值：

```cpp
X v = fx.get(); // 如果必要，等待值被计算
```

如果值不在那里，我们的线程将被阻塞，直到它到达。如果值无法计算，`get()` 可能会抛出一个异常（来自系统或从 `promise` 传递）。

`promise` 的主要目的是提供“放入”操作（称为 `set_value()` 和 `set_exception()`）以匹配 `future()`。"future" 和 "promise" 的名称是历史留下的；请不要指责或表扬它们。它们是另一种富有成效的双关语。

如果你有一个 `promise` 并需要向 `future` 发送 `X` 的结果，你可以采取两种方法之一：传递一个值或一个捕获的异常。例如：

```cpp
void f(promise<X>& px) // 一个任务：将结果放入 px
{
    // ...
    try {
        X res;
        // ... 计算 res 的值 ...
        px.set_value(res);
    } catch (...) {
        // 哎：无法计算 res
        px.set_exception(current_exception()); // 我将异常传递给 future 的线程
    }
}
```

`current_exception()` 函数引用被捕获的异常。

为了处理通过 `future` 传递的异常，`get()` 的调用者必须准备在某处捕获它。例如：

```cpp
void g(future<X>& fx) // 一个任务：从 fx 获取结果
{
    // ...
    try {
        X v = fx.get(); // 如果必要，等待值被计算
        // ... 使用 v ...
    } catch (...) {
        // 哎：有人无法计算 v
        // ... 处理错误 ...
    }
}
```

如果错误没有由 `g()` 自身处理，代码将简化为最形式：

```cpp
void g(future<X>& fx) // 一个任务：从 fx 获取结果
{
    // ...
    X v = fx.get(); // 如果必要，等待值被计算
    // ... 使用 v ...
}
```

现在，从 `fx()` 的函数 `f()` 抛出的异常将隐式地传播给 `g()` 的调用者，就像 `g()` 直接调用 `f()` 一样。

### 18.5.2 packaged_task


```cpp
bool pop( T& t)
{
    // (Unique)unique_lock<mutex> lk(myMutex);

    // 如果队列为空，释放锁直到被通知
    while (!myInterrupt && myQueue.empty()) myCV.wait(lk);

    // 重新获取锁，恢复

    // 检查是否中断
    if(myInterrupt) return false;

    // 合并头部访问与弹出
    t = move(myQueue.front());
    myQueue.pop();

    return true;
}
// 解锁
```

以下是 `ConcurrentQueue.h` 中并发生产者消费者队列的最终列表：

```cpp
1 #include <queue>
2 #include <mutex>
```

```cpp
#include <condition_variable>
using namespace std;

template <class T>
class ConcurrentQueue
{
    queue<T> myQueue;
    mutable mutex myMutex;
    condition_variable myCV;
    bool myInterrupt;

public:
    ConcurrentQueue() : myInterrupt(false) {}
    ~ConcurrentQueue() { interrupt(); }

    bool empty() const
{
        // 加锁
        lock_guard<mutex> lock(myMutex);
        // 访问底层队列
        return myQueue.empty();
    } // 解锁

    // 参数弹出
    bool tryPop(T& t)
    {
        // 加锁
        lock_guard<mutex> lock(myMutex);
        if (myQueue.empty()) return false;
        // 从队列移动
        t = move(myQueue.front());
        // 合并头部访问与弹出
        myQueue.pop();

        return true;
    } // 解锁

    // 通过 push(move(t)) 按值传递或移动
    void push(T t)
    {
        // 加锁
        lock_guard<mutex> lock(myMutex);
        // 移动到队列
        myQueue.push(move(t));
    } // 通知前解锁

    myCV.notify_one();

    // 如果为空则等待
    bool pop(T& t)
    {
        // (Unique) 加锁
        unique_lock<mutex> lk(myMutex);

        // 如果队列为空，释放锁直到被通知
        while (!myInterrupt && myQueue.empty()) myCV.wait(lk);

        // 重新获取锁，恢复

        // 检查是否中断
        if (myInterrupt) return false;

        // 合并头部访问与弹出
        t = move(myQueue.front());
        myQueue.pop();

        return true;

    } // 解锁

    void interrupt() {
        lock_guard<mutex> lk(myMutex);
        myInterrupt = true;
    }

    myCV.notify_all();
}

void resetInterrupt() {
    myInterrupt = false;
}

void clear() {
    queue<T> empty;
    swap(myQueue, empty);
}
```

### 3.14 高级同步

C++11 只提供了两种同步原语：互斥锁（`mutex`）和条件变量（`condition variable`）。经典的并行编程通常还涉及更高级的同步结构，如信号量（`semaphore`）、屏障（`barriers`）和共享互斥锁（`shared mutexes`）。标准线程库并没有提供这些结构¹¹¹它们都可以通过组合互斥锁和条件变量来开发。

> ¹¹ 虽然共享互斥锁及其相关的 RAII 共享锁已计划在未来的 C++ 更新中引入。

尽管在本书书的剩余部分或典型应用中不需要这些结构，但我们鼓励读者尝试自己实现它们，因为这是操作互斥锁和条件变量并深层理解并发编程的绝佳机会。

#### 信号量

信号量本质上是一个增加了灵活性的互斥锁。

首先，信号量可以处于锁定的状态构造，而互斥锁总是以未锁的状态构造。因此，信号量可以在大门显式打开之前禁止访问关键区域，这是互斥锁无法做到的。

其次，信号量可以授予对关键代码的访问权限，以便同时管理多个线程。它有一个参数 `$n$`，使得没有超过 $n$ 个线程可以获取锁并并发执行关键区域。当 $n$ 个线程正在执行关键区域时，另一个第 $(n+1)$ 个请求锁的线程将等待，直到其中一个线程离开关键区域并释放信号量。例如，多下载管理使用信号量来限制同时下载的数量，避免网络拥塞。

信号量类的签名如下：

```cpp
1 template <LOCKABLE>
2 class Semaphore
3 {
4 
5 public:
6 
7     // 锁定时构造
8     // 构造时使用 n=0
9     Semaphore( size_t n);
10
11    // 允许通过
12     // 与 lock() 语义相同
13    void post( const size_t n = 1);
14
15     // 与 unlock() 语义相同
16    void wait();
17
18    // 释放锁
19    void unlock();
20 };
```

由于历史原因，`lock()` 被调用 `wait()`，而 `unlock()` 被调用 `post()`。信号量实现了 `lockable` 接口，并与 RAII 工作。主动或主动等待（取决于信号量是使用互斥锁还是自旋锁）。

#### 屏障

屏障是另一种经典的同步结构。调用 `wait()` 的线程会将线程放入睡眠或主动等待（取决于屏障是用互斥锁还是自旋锁实现的），直到 $n$ 个线程调用，此时所有 $n$ 个线程恢复执行。

其签名如下：

```cpp
template <class LOCKABLE>
class Barrier {
  public:
    Barrier( const size_t n);
    void wait();
};
```

#### 共享锁

更困难的是共享互斥锁的正确实现，这是一个在数据结构中非常有用的结构。假设我们实现一个共享互斥锁，只要有一个读者，写入者就会被拒绝访问。在读者不断出现的情况下，写入者永远无法获得访问并一直等待。这种策略会饿饿写入线程。写入者需要对读者和其他写入者的排他访问，因此它们一次访问一个结构。只要队列中有读者，读者就会被允许。

因此，这里需要一些计数。优先级必须取决于队列中读者和写入者的数量，以及线程等待的时间。就像迪士尼景点入口的保安人员一样，共享互斥锁必须尽可能平衡共享和独占通行证。

### 3.15 懒初始化模式

懒初始化模式是一种常用的编程模式，包括金融领域。当某个对象（如数据库连接或插值曲线）初始化开销很大，且在程序执行期间可能使用也可能不使用，常识是将昂贵的初始化推迟到第一次使用。

以下是曲线的懒初始化示例。懒初始化曲线在金融的样线文中非常常见。样线的初始化成本很高，是懒化的天然选择。

```cpp
class Curve
{
    // 是否初始化？
    bool myInit;

    // 昂贵的初始化
    void init();

    // 在曲线上取值
    // 曲线必须已初始化
    double getPrivate(const double) const;

public:

    // 构造时未初始化
    Curve() : myInit(false) {}

    // 高层取值函数
    // 实现懒初始化
    // 然后调用私有的 getVal
    double getVal(const double x)
};
```

```cpp
if( myInit){
  // 延迟初始化
  init();
  myInit = true;
}

return getValPrivate( x);
};
```

代码应该是自解释其懂的，特别是带有注释的情况下。这在序列化上下文中是一个完全有效的曲线对象。但它不能被并发使用。当然，在曲线上取值是线程安全的，我们注意到相关方法 `getValPrivate()` 是 `const` 的。初始化不是，而且我们注意到实现了懒性初始化的公共方法 `getVal()` 并不是 `const` 的。

我们如何在不牺牲这一非常有用的懒性初始化特性的情况下，让曲线安全并发安全呢？一种自然的解决方案是用锁来保护初始化：

```cpp
#include <mutex>
using namespace std;

class Curve {
  mutex myMutex;

  // ...
public:
  // ...
  double getVal( const double x) {
    unique_lock<mutex> lk(myMutex);
    if( myInit){
      // 延迟初始化
      init();
      myInit = true;
    }
    lk.unlock();
    return getValPrivate( x);
  }
};
```

（这里使用了 `unique_lock`，以便我们可以在调用线程安全的 `getValPrivate()` 之前释放锁）。锁应该尽快释放。

然而，这个解决方案存在一个问题：它是极其低效的。每次调用 `getVal()` 都必须获取锁，尽管这只在初始化时是必须的。获取锁是昂贵的，

通常比读取曲线要昂贵；因此该方案完全不令人意。事实上，它比牺牲懒性初始化还要糟糕。尽管这种方案是*损坏的*，但它仍然可能出现在文献中：

```cpp
#include <mutex>
using namespace std;

// ...
double getVal(const double x)
{
    // 首先在未解锁状态下检查
    if (!myInit)
    {
        // 初始化后我们永远不会到达这里
        // 所以我们只加锁一次
        lock_guard<mutex> lock(myMutex);

        // 在锁的保护下再次检查
        if (!myInit)
        {
            init();
            myInit = true;
        }
    }
    return getValPrivate(x);
}
```

这段代码不起作用：一个线程可能在第一个未解锁的检查下检查 *myInit*，而另一个线程可能正在锁的保护下写入 *myInit* 并执行“*myInit=true”。这会导致数据竞态。可以通过将 *myInit* 设为原子布尔值，并调用原子 *exchange* 来执行检查来修复，就像我们为自旋锁所做的那样，但这不是必要的。懒性初始化是非常常见的，以至于 `once_flag` 类型和 `call_once()` 函数（两者都定义在 `<mutex>` 头文件中）这种构造解决了问题，并保证传递给 `call_once()` 的*可调用对象*参数被调用了一次且仅调用一次。一种可能的实现方法是使用原子的双重检查锁定，如上所述。这就是它如何被应用于修复我们的曲线的：

```cpp
#include <mutex>
using namespace std;

class Curve {
    once_flag myOF;

    void init();
    double getValPrivate(const double x) const;

public:

    double getVal( const double x)
    {
    call_once(myOF, &Curve::init, this);
    return getValPrivate( x);
}
};
```

`call_once()` 之后跟随 `once_flag` 的参数遵循第 3.2 节描述的可调用对象模式。

### 3.16 原子类型

在第 3.8 节编写自旋锁互斥量时，我们简要介绍了原子类型。更具体地说，我们引入了 `atomic<bool>` 类型，它在很多方面的行为上都像一个 `bool`，但提供了一个 `exchange()` 方法，该方法以原子方式设置原子布尔的状态并返回其之前的状态，也就是说在整个设置+检查操作期间，另一个线程无法读取或写入该原子对象，提供了防止数据竞态的保证。

另一个典型的例子是统计对象访问的次数。例如，可以将一个计数器放在一个计数器上，并在每次读取计数器时增加它。我们在下面定义了一个基本的计数器类：

```cpp
class Counter
{
    int myCount;
public:
    Counter(const int count = 0) : myCount(count) {}
    int get() const { return myCount; }
    void set(const int count) { myCount = count; }
    void increment() { myCount++; }
    void decrement() { myCount--; }
};
```

显而易见这个计数器不是线程安全的，不能被并发操作。一个问题是 `++`、`--`、`+=` 等操作不是原子的。例如，像“x++”这样的语句实际上翻译为多条指令：

- 1. 读取 x 的状态。

- 2. 加 1。

- 3. 将 x 的状态设置为结果。

- 4. 返回 x 之前的状态。

问题当然是，另一个线程在这一操作序列期间介入并导致竞态条件。我们可以通过锁以性能为代价使计数器变为线程安全：

```cpp
#include <mutex>
using namespace std;
class Counter
{
    int myCount;
    mutable mutex myMutex;
public:
    Counter(const int count = 0) : myCount(count) {}
    int get() const
    {
        lock_guard<mutex> lock(myMutex);
        return myCount;
    }
    void set(const int count)
    {
        lock_guard<mutex> lock(myMutex);
        myCount = count;
    }
    void increment()
    {
        lock_guard<mutex> lock(myMutex);
        myCount++;
    }
    void decrement()
    {
        lock_guard<mutex> lock(myMutex);
        myCount--;
    }
};
```

或者，使用原子操作：

```cpp
#include <atomic>
using namespace std;
class Counter
{
    atomic<int> myCount;
public:
    Counter(const int count = 0) : myCount(count) {}
    int get() const
    {
        return myCount.load();
    }
    void set(const int count)
    {
        myCount.store(count);
    }
    void increment()
    {
        myCount++;
    }
    void decrement()
    {
        myCount--;
    }
};
```

在许多情况下，原子提供了比锁更快的替代方案。甚至可以使用原子操作编写无锁队列，并在 [15] 中给出了详细示例。无锁算法和数据结构的发展是非常高级的，在特定情况下才有意义，据我们所知，我们只在引用计数器或自旋锁等简单情况下使用原子。

### 3.17 任务管理

标准线程库在 `<future>` 头文件中提供了许多方便的构造，用于将任务发送到另一个线程并在调度线程监控执行情况：`async()` 函数、`future` 和 `promise` 类以及 `packaged_task` 构造。`async()` 函数是一个一站式解决方案，将可调用对象发送到另一个线程执行。其他低级构造提供了线程间通信的设施，而不是线程本身的管理。结合第 3.2 节解释的线程管理，这些构造为在线程池的一组工作线程上执行任务提供了方便实用的方法，它们构成了重要的构建块。

#### Async

C++11 提供的用于异步执行的最简单构造是定义在 `<future>` 中的自由函数 `async()`。该函数接受一个可调用参数，它必须异步执行，并返回一个 `future` 以便调用者监控其执行情况。

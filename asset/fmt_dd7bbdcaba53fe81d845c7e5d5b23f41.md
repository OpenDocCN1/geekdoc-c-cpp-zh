
```cpp
std::timed_mutex timedMutex;
timedMutex.try_lock_for(chrono::seconds(5));
```

- `* bool try_lock_until(chrono::time_point<Clock, Duration> const &absTime) noexcept:`

调用线程尝试在 `absTime` 经过之前获取互斥锁的所有权。如果获取所有权，则返回 `true`，否则返回 `false`。如果调用线程拥有该锁，也返回 `true`，在这种情况下，递归互斥锁还会增加其内部锁计数。`Clock` 和 `Duration` 类型根据实际的 `absTime` 参数推断得出。

```cpp
std::timed_mutex timedMutex;
timedMutex.try_lock_until(chrono::system_clock::now() + chrono::seconds(5));
```

## 20.21 多线程程序中的初始化

使用本节引入的 `std::once_flag` 和 `std::call_once` 函数，必须包含 `<mutex>` 头文件。

在单线程程序中，全局数据的初始化并不一定发生在代码的某一个点。一个例子是单例类的初始化（参见 Gamma 等人 (1995) 的《设计模式》，Addison-Wesley）。单例类可以定义一个静态数据成员 `Singleton *s_object`，指向单例对象，并可以提供一个静态成员实例，其实现方式如下：

```cpp
Singleton &Singleton::instance()
{
    return s_object =
           *s_object
           : (s_object = new Singleton);
}
```

在多线程程序中，这种方法会立即变得复杂。例如，如果两个线程同时调用 `instance()`，而 `s_object` 仍然等于 0，那么它们都可能调用 `new Singleton`，导致一个动态分配的对象变得无法访问。其他线程在 `s_object` 为第一个线程初始化后，可能会返回该对象的引用，也可能会返回由第二个线程初始化的对象的引用。这并不完全是单例预期的行为。

互斥锁（参见第 20.2 节）可以用于解决这类问题，但它们会带来一些开销和效率低下，因为在每次调用 `Singleton::instance()` 时都必须检查互斥锁。

## 第 20 章 多线程

当变量需要初始化，且初始化应该只发生一次时，应该使用 `std::once_flag` 类型和 `std::call_once` 函数。

`call_once` 函数期望两个或三个参数：

- 第一个参数是 `once_flag` 变量，用于跟踪实际的初始化状态。如果 `once_flag` 表明初始化已经发生，`call_once` 函数将直接返回；
- 第二个参数是必须只调用一次的函数地址。该函数可以是一个自由函数，也可以是类成员函数的地址；
- 如果第二个参数是类成员函数的地址，则必须作为 `call_once` 的第三个参数提供调用该成员函数所需的对象。

现在可以轻松地设计单例实例函数的线程安全实现（为了简洁起见使用了类内实现）：

```cpp
class Singleton {
    static std::once_flag s_once;
    static Singleton *s_singleton;
    public:
    static Singleton *instance() {
        std::call_once(s_once, []() { s_singleton = new Singleton(); });
        return s_singleton;
    }
};
```

然而，即使对于多线程程序，还有其他初始化数据的方法：

- 首先，假设使用 `constexpr` 关键字声明构造函数（参见第 8.1.4 节），满足常量初始化的要求。在这种情况下，使用该构造函数初始化的静态对象保证在静态初始化阶段的任何代码运行之前完成初始化。`std::mutex` 利用了这一点，因为它消除了互斥锁初始化时出现竞态条件的可能性。
- 第二，可以使用复合语句内部定义的静态变量（例如函数体内的静态变量）。定义在复合语句内的静态变量会在函数第一次被调用时，在代码中定义静态变量的地方进行初始化。这里是一个示例：

```cpp
#include <iostream>

struct Cons {
    Cons() {
        std::cout << "Cons called\n";
    }
};
```

```cpp
void called(char const *time)
{
    std::cout << time << "time called() activated\n";
    static Cons cons;
}
int main()
{
    std::cout << "Pre-1\n";
    called("first");
    called("second");
    std::cout << "Pre-2\n";
    Cons cons;
}
```

```cpp
/* 显示：
Pre-1
firsttime called(activated)
Cons called
secondtime called(activated)
Pre-2
Cons called
*/
```

## 20.2. 同步（互斥锁）

此功能会导致线程等待，直到互斥锁可用。

### 20.2.2 共享互斥锁

共享互斥锁允许多个线程读取数据，但只有一个线程可以修改它。共享互斥锁提供了以下成员：

- `void lock()`

  阻塞调用线程直到获取所有权。如果互斥锁已锁定，则抛出异常。

- `void unlock()`

  释放调用线程持有的锁。如果线程未拥有该锁，则无操作发生。

- `bool try_lock()`

  当前线程尝试非阻塞地获取所有权。如果未获取所有权，则返回 `false`。如果获取了所有权则返回 `true`。

- `bool try_lock_for(rel_time relTime)`

  尝试在 `relTime` 指定的相对时间内获取锁。如果 `relTime` 指定的时间小于或等于 `rel_time::zero()`，该成员尝试非阻塞地获取所有权（类似于 `try_lock()`）。该成员将在指定时间内返回，如果获取了所有权则返回 `true`，否则返回 `false`。

- `bool try_lock_until(abs_time absTime)`

  尝试在 `absTime` 指定的时间之前为调用线程获取所有权。如果 `absTime` 指定的时间已过去，该成员尝试非阻塞地获取所有权（类似于 `try_lock()`）。如果获取了所有权则返回 `true`，否则返回 `false`。

## 20.3 锁与锁处理

互斥量（mutex）负责控制，而它们的析构函数保留了 `lock_guard` 提供的解锁保证。

`lock_guard` 类提供了一个有限但实用的接口：

- `lock_guard<Mutex>(Mutex &mutex)`:

  在定义 `lock_guard` 对象时，指定互斥锁类型（例如 `std::mutex`、`std::timed_mutex`、`std::shared_mutex`），并将指示类型的互斥锁作为参数传递。构造会阻塞直到 `lock_guard` 对象拥有锁。`lock_guard` 的析构函数会自动释放互斥锁。

- `lock_guard<Mutex>(Mutex &mutex, std::adopt_lock_t)`:

  此构造函数用于将互斥锁的控制权从调用线程转移到 lock_guard。该锁必须已经被调用线程拥有。以下是其使用方法的示例：

  - 在第 1 行，`threadAction` 接收到一个互斥锁的引用。假设该互斥锁拥有锁；
  - 在第 3 行，它被转移给 `lock_guard`。尽管我们没有显式使用 `lock_guard` 对象，但应该定义一个对象以防止编译器在函数结束前销毁匿名对象；
  - 当函数结束时（在第 5 行），互斥锁的锁由 `lock_guard` 的析构函数释放。

```
void threadAction(std::mutex mutex, int &sharedInt)
{
  std::lock_guard<std::mutex> lg(mutex, std::adopt_lock_t());
  // 对 sharedInt 进行某些操作
}
```

- `mutex_type`:

  除了构造函数和析构函数，`lock_guard<Mutex>` 类型还定义了 `mutex_type`；它是传递给 `lock_guard` 构造函数的 `Mutex` 类型的别名。

这是一个使用 `lock_guard` 的多线程程序的简单示例，用于防止插入到 `cout` 中的信息混合。

```cpp
bool oneLine(istream &in, mutex &mut, int &nr)
{
  lock_guard<mutex> lg(mut);

  string line;
  if (not getline(in, line))
    return false;

  cout << nr << " : " << line << endl;

  return true;
}
```

```cpp
void io(ostream &in, mutex &mut, int &nr)
{
  while (oneLine(in, mut, nr))
    this_thread::yield();
}

int main(int argc, char **argv)
{
    ifstream in (argv[1]);
    mutex ioMutex;

    thread t1(in, ref(ioMutex), 1);
    thread t2(in, ref(ioMutex), 2);
    thread t3(in, ref(ioMutex), 3);

    t1.join();
    t2.join();
    t3.join();
}
```

使用 `lock_guard` 时，定义 `std::unique_lock` 类对象时必须指定互斥锁类型。`unique_lock` 类比基础的 `lock_guard` 模板复杂得多。它的接口没有定义拷贝构造函数或重载的赋值运算符，但它定义了移动构造函数和移动赋值运算符。在以下 `unique_lock` 接口的概述中，`Mutex` 指的是定义 `unique_lock` 时指定的互斥锁类型：

- `unique_lock() noexcept`:

  默认构造函数尚未使用互斥锁激活。在执行任何操作之前，必须分配一个互斥锁（例如使用移动赋值）；

- `explicit unique_lock(Mutex&)`: 

  用现有互斥锁对象初始化 `unique_lock`，并调用 `mutex.lock()`；

- `unique_lock(Mutex&, defer_lock_t) noexcept`:

  用现有互斥锁对象初始化 `unique_lock`，但不调用 `mutex.lock()`。

  通过将 `defer_lock_t` 对象作为构造函数的第二个参数，例如 `unique_lock<mutex> u(mutex, defer_lock_t)`。

- `unique_lock(Mutex&, try_to_lock_t) noexcept`:

  用现有互斥锁对象初始化 `unique_lock`，并调用 `mutex.try_lock()`；如果无法锁定，构造函数将不会加锁：

- `unique_lock(Mutex&, adopt_lock_t) noexcept`:

  用现有互斥锁对象初始化 `unique_lock`，并假设当前线程已经锁定了该互斥锁；

- `unique_lock(Mutex&, chrono::duration<Rep, Period> const&) noexcept`:

  此构造函数通过调用 `mutex.try_lock_for(relTime)` 尝试获取互斥锁对象的所有权。因此，指定的互斥锁类型必须支持此成员（例如，它是 `std::timed_mutex`）。它可能如下：

```cpp
std::unique_lock<std::timed_mutex> u(mutex, chrono::seconds(5));
```

- `unique_lock(Mutex, chrono::time_point<Clock, Duration> const &absTime) noexcept`:

  此构造函数通过调用 `mutex.try_lock_until(absTime)` 尝试获取互斥锁对象的所有权。

- `lock()`:

  锁定互斥锁。

- `unlock()`:

  释放互斥锁。

- `try_lock()`:

  尝试锁定互斥锁。

- `try_lock_for(relTime)`:

  尝试在相对时间内锁定互斥锁。

- `try_lock_until(absTime)`:

  尝试在绝对时间内锁定互斥锁。

- `release()`:

  释放互斥锁的所有权，但不解锁。

- `owns() const`:

  检查互斥锁是否被锁定。

- `get_lock()`:

  返回互斥锁的引用。

- `swap(other)`:

  交换两个 `unique_lock` 对象的内容。

- `operator=(Mutex&)`: 

  赋值运算符。

- `operator=(unique_lock&&)`: 

  移动赋值运算符。

- `unique_lock(Mutex)`: 

  构造函数。

- `unique_lock(unique_lock&&)`: 

  移动构造函数。

- `operator bool() const`: 

  布尔运算符，检查互斥锁是否被锁定。

# 20.3. 锁与处理

### 20.3.2 死锁

当处理数据需要两个锁时，如果一个线程获取了第一个锁而另一个线程获取了第二个锁，就会发生死锁。C++ 定义了通用的 `std::lock` 和 `std::try_lock` 函数，可以帮助防止此类情况发生。

在使用这些函数之前，必须包含 `<mutex>` 头文件。

在接下来的概述中，`ll, ...` 表示对一个或多个可锁类型（lockable types）对象的引用：

- `void std::lock(ll, ...);`

当函数返回时，已获取了所有 `ll` 对象的锁。如果无法获取至少一个对象的锁，则到目前已获取的所有锁都将被释放，即使为无法获取锁的对象抛出异常也是。

- `int std::try_lock(ll, ...);`

该函数调用可锁对象的 `try_lock` 成员函数。如果获取了所有的锁，则返回 -1。否则返回第一个无法锁定的参数的索引（从 0 开始），并释放之前获取的所有锁。

考虑以下多线程程序的示例：线程使用互斥量来获取对 `count` 和一个 `int` 值的访问。然而，`fun` 锁定 `count`（第 7 行），然后锁定 `value`（第 10 行）；`fun2` 锁定 `value`（第 16 行），然后锁定 `cout`（第 19 行）。显然，`fun` 锁定了 `count`，在 `fun` 之前 `fun2` 无法锁定 `count`。但为了访问 `value` 中的信息，`fun` 只在返回时才释放它的锁。它必须获取 `value` 的锁，但它做不到，因为 `fun2` 已经锁定了 `value`：线程正在互相等待，且没有线程让步：

```cpp
1:
2: int value;
3: mutex valueMutex;
4: mutex coutMutex;
5:
6: void fun()
7: {
8:
9: lock_guard<mutex> lg1(coutMutex);
10:
cout << "fun 1 locks cout\n";
11: lock_guard<mutex> lg2(valueMutex);
12:
cout << "fun 1 locks value\n";
13: }
14: void fun2()
15: {
16:
lock_guard<mutex> lg1(valueMutex);
17:
cerr << "fun 2 locks value\n";
18:
19: lock_guard<mutex> lg2(coutMutex);
20:
cout << "fun 2 locks cout\n";
21: }
22:
23: int main()
24: {
26:   thread t1(fun1);
27:   fun2();
28:   t1.join();
29: }
```

避免死锁的良好配方是防止嵌套（或多个）互斥锁锁定。但如果必须使用多个互斥量，请始终按照相同的顺序获取锁。与其手动执行这样做，不如尽可能使用 `std::lock` 和 `std::try_lock` 来获取互斥锁。这些函数接受多个参数，这些参数必须像 `lock_guard`、`unique_lock` 甚至普通的 `mutex` 一样是可锁的。之前的死锁程序可以修改为使用 `std::lock` 同时锁定两个互斥量。在这个示例中，使用一个互斥量也可以，但修改后的程序现在看起来与之前的程序非常相似。注意第 10 行和第 21 行中 `unique_lock` 参数使用了不同的排序顺序：在调用 `std::lock` 或 `std::try_lock` 时，不需要使用相同的顺序。

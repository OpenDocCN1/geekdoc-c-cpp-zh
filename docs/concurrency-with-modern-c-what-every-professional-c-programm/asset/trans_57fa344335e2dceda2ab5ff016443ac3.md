
```cpp
34    std::cout << '\n';

35
36    std::thread t1(setDataReady);
37    std::thread t2(waitingForWork);

38
39    t1.join();
40    t2.join();

41
42    std::cout << '\n';

43
44 }
```

偶然情况下，程序的第一次调用运行正常。第二次调用会阻塞，因为 notify 调用（第 28 行）在线程 t2（第 37 行）进入等待（第 19 行）之前就发生了。

![](img/d61a6c83410484053b8892275d2fcc4f_662_0.png)

阻塞的条件变量

当然，死锁和活锁是竞态条件的副作用。死锁通常取决于线程的交错执行，有时可能发生，有时可能不发生。活锁与死锁类似。死锁会阻塞，而活锁看起来像是在取得进展——注意是“看起来”。想一想事务内存用例中的事务。每次事务本应提交时，都会发生冲突；因此，会进行回滚。下面是事务的细节。

## 15.3 破坏程序不变量

程序不变量是在程序的整个生命周期内都应保持不变的不变量。

恶意竞态条件会破坏程序的一个不变量。程序的不变量是：所有余额的总和应保持不变。在我们的例子中，这个总和是 200 欧元，因为每个账户初始都有 100 欧元（第 9 行）。我既不想通过转账创造钱，也不想销毁钱。

```cpp
45     std::cout << "    acc2.balance: " << acc2.balance << '\n';
46
47     std::cout << "Final sum: ";
48     printSum(acc1, acc2);
49
50     std::cout << '\n';
51
52 }
```

一开始，账户总和是 200 欧元。第 33 行通过使用第 21–23 行中的函数 printSum 来显示总和。第 38 行使该不变量可见。由于第 16 行有一个短暂的 1 秒 sleep，中间总和为 182 欧元。最终一切正常；每个账户都有正确的余额（第 44 行和第 45 行），并且总和为 200 欧元（第 48 行）。

下面是程序的输出。

```
Initial sum: 200
Intermediate sum: 182
        acc1.balance: 108
        acc2.balance: 92
Final sum: 200
```

账户的不变量

## 15.4 数据竞争

数据竞争是指至少两个线程同时访问一个共享变量的情况。其中至少有一个线程试图修改变量。

如果你的程序存在数据竞争，它就具有未定义行为。这意味着一切结果都有可能，因此再对程序进行推理已毫无意义。

让我向你展示一个存在数据竞争的程序。

### 一个数据竞争

```cpp
// addMoney.cpp

#include <functional>
#include <iostream>
#include <thread>
#include <vector>

struct Account{
  int balance{100};
};

void addMoney(Account& to, int amount){
  to.balance += amount;
}

int main(){

  std::cout << '\n';

  Account account;

  std::vector<std::thread> vecThreads(100);


  for (auto& thr: vecThreads) thr = std::thread(addMoney, std::ref(account), 50);

  for (auto& thr: vecThreads) thr.join();


  std::cout << "account.balance: " << account.balance << '\n';

  std::cout << '\n';

}
```

一百个线程正在向同一个账户（第 20 行）添加 50 欧元（第 25 行）。它们使用函数 addMoney。关键观察是，对账户的写入是在没有同步的情况下完成的。因此，我们存在数据竞争，结果无效。这是未定义行为，最终余额（第 30 行）会在 5000 到 5100 欧元之间变化。

![](img/d61a6c83410484053b8892275d2fcc4f_666_0.png)

*数据竞争会导致余额不正确*

## 15.5 死锁

死锁是一种状态：至少有一个线程永久阻塞，因为它在等待一个它永远得不到的资源被释放。

死锁有两个主要原因：

- 1. 互斥量没有被解锁。
- 2. 你以不同的顺序锁定互斥量。

为了克服第二个问题，经典 C++ 中会使用锁层级³等技术。

有关死锁以及如何用现代 C++ 克服死锁的详细信息，请阅读“互斥量与锁的问题”小节。

³http://collaboration.cmc.ec.gc.ca/science/rpn/biblio/ddj/Website/articles/DDJ/2008/0801/071201hs01/071201hs01.html

![](img/d61a6c83410484053b8892275d2fcc4f_667_0.png)

### 多次锁定非递归互斥量

多次锁定非递归 `mutex` 是未定义行为。

**多次锁定**

```cpp
// lockTwice.cpp

#include <iostream>
#include <mutex>

int main(){

    std::mutex mut;

    std::cout << '\n';

    std::cout << "first lock call" << '\n';

    mut.lock();

    std::cout << "second lock call" << '\n';

    mut.lock();

    std::cout << "third lock call" << '\n';

}
```

通常，你会遇到死锁。

![](img/d61a6c83410484053b8892275d2fcc4f_667_1.png)

非递归互斥量造成的死锁

## 15.6 伪共享

当处理器从主内存读取诸如 `int` 这样的变量时，它从内存中读取的字节数会超过一个 `int` 的大小。处理器会从内存中读取一整条缓存行（通常是 64 字节）。如果两个线程同时读取位于同一缓存行上的不同变量 a 和 b，就会发生伪共享。尽管 a 和 b 在逻辑上是分离的，但它们在物理上是相连的。由于 a 和 b 共享同一条缓存行，因此需要对缓存行进行昂贵的硬件同步。结果是你能得到正确的结果，但并发应用的性能会下降。下面这个程序中发生的正是这种现象。

### 伪共享

```cpp
// falseSharing.cpp

#include <algorithm>
#include <chrono>
#include <iostream>
#include <random>
#include <thread>
#include <vector>

constexpr long long size(100000000);

struct Sum{
    long long a{0};
    long long b{0};
};

int main(){

    std::cout << '\n';

    Sum sum;

    std::cout << &sum.a << '\n';
    std::cout << &sum.b << '\n';

    std::cout << '\n';

    std::vector<int> randValues, randValues2;
    randValues.reserve(size);
    randValues2.reserve(size);

    std::mt19937 engine;
    std::uniform_int_distribution<> uniformDist(1,10);

    int randValue;
    for (long long i = 0; i < size; ++i){
        randValue = uniformDist(engine);
        randValues.push_back(randValue);
        randValues2.push_back(randValue);
    }

    auto sta = std::chrono::steady_clock::now();

    std::thread t1([&sum, &randValues]{
        for (auto val: randValues) sum.a += val;
    });

    std::thread t2([&sum, &randValues2]{
        for (auto val: randValues2) sum.b += val;
    });

    t1.join(), t2.join();

    std::chrono::duration<double> dur= std::chrono::steady_clock::now() - sta;
    std::cout << "Time for addition" << dur.count()
              << " seconds" << '\n';

    std::cout << "sum.a: " << sum.a << '\n';
    std::cout << "sum.b: " << sum.b << '\n';

    std::cout << '\n';

}
```

第 13 行和第 14 行中的变量 a 和 b 共享同一条缓存行。线程 t1（第 44 行）和线程 t2 使用这两个变量并发地对向量 randValues 和 randValues2 求和。两个向量都有 1 亿个介于 1 到 10 之间的整数。程序的输出显示了有趣的事实：a 和 b 按 8 字节边界对齐，因为在我的系统上这是 long long int 的对齐方式。

![](img/d61a6c83410484053b8892275d2fcc4f_670_0.png)

伪共享

如果我把 a 和 b 的对齐方式改为 64 字节，会发生什么？64 是我的系统上缓存行的大小。下面是我必须对 struct Sum 做的细微修改。我没有为随机数生成器使用种子；因此，我每次都会得到相同的随机数。

```cpp
struct Sum{
    alignas(64) long long a{};
    alignas(64) long long b{};
};
```

![](img/d61a6c83410484053b8892275d2fcc4f_670_1.png)

伪共享已解决

现在 a 和 b 按 64 字节边界对齐，程序变得快了六倍以上。原因是 a 和 b 现在位于不同的缓存行上。

### 优化器检测到伪共享

如果我用最高优化级别编译最后几个程序，我的优化器会检测到伪共享并消除它。这意味着无论有没有伪共享，我得到的性能数值都相同。这在 Windows 上也是如此。下面是优化后的数值。

![](img/d61a6c83410484053b8892275d2fcc4f_671_0.png)

伪共享已被优化器解决

### 在 C++17 中使用 std::hardware_destructive_interference_size 和 std::hardware_constructive_interference_size

函数 `std::hardware_destructive_interference_size` 和 `std::hardware_constructive_interference_size` 让你能够以可移植的方式处理缓存行大小。`std::hardware_destructive_interference_size` 返回两个对象之间避免伪共享所需的最小偏移量，而 `std::hardware_constructive_interference_size` 返回促进真共享的连续内存最大大小。

在 C++17 中，Sum 可以以平台无关的方式编写。

```cpp
struct Sum{
    alignas(std::hardware_destructive_interference_size) long long a{};
    alignas(std::hardware_destructive_interference_size) long long b{};
};
```

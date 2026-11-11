
```cpp
std::thread reader3([] { printNumber("Dijkstra"); });
std::thread reader4([] { printNumber("Scott"); });
std::thread w2([] { addToTeleBook("Bjarne", 1965); });
std::thread reader5([] { printNumber("Scott"); });
std::thread reader6([] { printNumber("Ritchie"); });
std::thread reader7([] { printNumber("Scott"); });
std::thread reader8([] { printNumber("Bjarne"); });

reader1.join();
reader2.join();
reader3.join();
reader4.join();
reader5.join();
reader6.join();
reader7.join();
reader8.join();

w1.join();
w2.join();

std::cout << '\n';

std::cout << "\nThe new telephone book" << '\n';
for (auto teleIt: teleBook) {
    std::cout << teleIt.first << ": " << teleIt.second << '\n';
}

std::cout << '\n';
}
```

第9行的电话簿是共享变量，必须受到保护。八个线程想读取电话簿；两个线程想修改它（第31-40行）。为了并发访问电话簿，读取线程在第23行使用 `std::shared_lock<std::shared_timed_mutex>`。这与写入线程形成对比，写入线程需要对临界区进行独占访问。这种独占性由第15行的 `std::lock_guard<std::shared_timed_mutex>` 提供。最后，程序显示更新后的电话簿（第55-58行）。

修复此问题的一种明显方法是在函数 printNumber 中仅使用读取操作：

### 读写锁问题已解决

```cpp
1  // readerWriterLocksResolved.cpp
2
3  ...
4
5  void printNumber(const std::string& na){
6    std::shared_lock<std::shared_timed_mutex> readerLock(teleBookMutex);
7    auto searchEntry = teleBook.find(na);
8    if(searchEntry != teleBook.end()){
9      std::cout << searchEntry->first << ": " << searchEntry->second << '\n';
10   }
11   else {
12     std::cout << na << " not found!" << '\n';
13   }
14 }
15
16 ...
```

如果某个键不在电话簿中，我只把该键和文本 not found! 写到控制台。

![](img/d61a6c83410484053b8892275d2fcc4f_156_0.png)

数据竞争已解决

在第二次程序执行中，你可以看到消息 Bjarne not found!。在第一次程序执行中，addToTeleBook 先执行；因此，找到了 Bjarne。

### 3.3.3 std::lock

std::lock 可以以原子步骤锁定其 Lockables9（例如互斥量或锁）。Lockable 是一种数据类型，支持成员函数 lock、unlock 和 try_lock。std::lock 是可变参数模板，因此可以接受任意数量的参数。std::lock 尝试使用死锁避免算法在一个原子步骤中获取所有锁。这些 Lockable 通过一系列未指定的 lock、try_lock 和 unlock 调用来锁定。如果某次 lock 调用引发异常，则在重新抛出之前，会对任何已锁定的 Lockable 调用 unlock。

还记得“互斥量的问题”小节中的死锁吗？

### 以不同顺序锁定互斥量

```cpp
// deadlock.cpp

#include <iostream>
#include <chrono>
#include <mutex>
#include <thread>

struct CriticalData{
  std::mutex mut;
};

void deadLock(CriticalData& a, CriticalData& b){

  a.mut.lock();
  std::cout << "get the first mutex" << '\n';
  std::this_thread::sleep_for(std::chrono::milliseconds(1));
  b.mut.lock();
  std::cout << "get the second mutex" << '\n';
  // do something with a and b
  a.mut.unlock();
  b.mut.unlock();

}

int main(){

  CriticalData c1;
  CriticalData c2;

  std::thread t1([&]{deadLock(c1,c2);});
  std::thread t2([&]{deadLock(c2,c1);});

  t1.join();
  t2.join();

}
```

让我们解决这个问题。函数 deadLock 必须以原子方式锁定其互斥量，而这正是下面示例中发生的情况。

### 延迟锁定互斥量

```cpp
// deadlockResolved.cpp

#include <iostream>
#include <chrono>
#include <mutex>
#include <thread>

using namespace std;

struct CriticalData{
    mutex mut;
};

void deadLock(CriticalData& a, CriticalData& b){

    unique_lock<mutex> guard1(a.mut,defer_lock);
    cout << "Thread: " << this_thread::get_id() << " first mutex" << '\n';

    this_thread::sleep_for(chrono::milliseconds(1));

    unique_lock<mutex> guard2(b.mut,defer_lock);
    cout << "  Thread: " << this_thread::get_id() << " second mutex" << '\n';

    cout << "    Thread: " << this_thread::get_id() << " get both mutex" << '\n';
    lock(guard1,guard2);
    // do something with a and b
}

int main(){

    cout << '\n';

    CriticalData c1;
    CriticalData c2;

    thread t1([&]{deadLock(c1,c2);});
    thread t2([&]{deadLock(c2,c1);});

    t1.join();
    t2.join();

    cout << '\n';
}
```

如果你用 std::defer_lock 调用 std::unique_lock 的构造函数，则底层互斥量不会自动锁定。此时（第16行和第21行），std::unique_lock 只是互斥量的所有者。得益于可变参数模板 std::lock，锁定操作在一个原子步骤中执行（第25行）。

在此示例中，std::unique_lock 管理资源的生命周期，而 std::lock 锁定关联的互斥量。你也可以反过来做。第一步，锁定互斥量。第二步，std::unique_lock 管理资源的生命周期。下面是第二种方法的示例。

```cpp
std::lock(a.mut, b.mut);
std::lock_guard<std::mutex> guard1(a.mut, std::adopt_lock);
std::lock_guard<std::mutex> guard2(b.mut, std::adopt_lock);
```

两种变体都能解决死锁。

![](img/d61a6c83410484053b8892275d2fcc4f_159_0.png)

使用 std::unique_lock 解决死锁

### 3.3.4.1 常量表达式

常量表达式是编译器可以在编译时求值的表达式。它们隐式线程安全。将关键字 constexpr 放在变量前会使该变量成为常量表达式。常量表达式必须立即初始化。

`constexpr double pi = 3.14;`

此外，用户定义的类型也可以是常量表达式。对于这些类型，要使其在编译时初始化，必须满足一些限制。

- 它们不能有虚成员函数或虚基类。
- 它们的构造函数必须是常量表达式。
- 每个基类和每个非静态成员都必须初始化。
- 它们的成员函数（应可在编译时调用）必须是常量表达式。

MyDouble 的实例满足所有这些要求。因此可以在编译时实例化它们。这种实例化是线程安全的。

### 用户定义的常量表达式

```cpp
// constexpr.cpp

#include <iostream>

class MyDouble{
private:
    double myVal1;
    double myVal2;
public:
    constexpr MyDouble(double v1, double v2): myVal1(v1), myVal2(v2){}
    constexpr double getSum() const { return myVal1 + myVal2; }
};

int main() {

    constexpr double myStatVal = 2.0;
    constexpr MyDouble myStatic(10.5, myStatVal);
    constexpr double sumStat = myStatic.getSum();

}
```

```cpp
26    t1.join();
27    t2.join();
28    t3.join();
29    t4.join();
30
31    std::cout << '\n';
32
33 }
```

程序以四个线程开始（第21-24行）。其中两个调用 do_once，另外两个调用 do_once2。预期结果是字符串 "Only once" 或字符串 "Only once2" 只显示一次。

![](img/d61a6c83410484053b8892275d2fcc4f_163_0.png)

std::call_once 和 std::once_flag 的用法

著名的单例模式保证只创建一个类实例。这在多线程环境中是一项具有挑战性的任务。得益于 std::call_once 和 std::once_flag，这项工作轻而易举。

现在单例以线程安全的方式初始化。

### 使用 std::call_once 和 std::once_flag 的单例模式

```cpp
1    // singletonCallOnce.cpp
2
3    #include <iostream>
4
5    #include <mutex>
6
7    using namespace std;
8
9    class MySingleton{
10
11   private:
12       static once_flag initInstanceFlag;
13       static MySingleton* instance;
14       MySingleton() = default;
15       ~MySingleton() = default;
```

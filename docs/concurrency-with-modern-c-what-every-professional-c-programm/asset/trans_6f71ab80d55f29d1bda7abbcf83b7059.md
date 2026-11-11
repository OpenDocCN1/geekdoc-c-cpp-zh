

## 读写锁

```cpp
1  // readerWriterLock.cpp
2
3  #include <iostream>
4  #include <map>
5  #include <shared_mutex>
6  #include <string>
7  #include <thread>
8
9  std::map<std::string,int> teleBook{{"Dijkstra", 1972}, {"Scott", 1976},
10                                   {"Ritchie", 1983}};
11
12 std::shared_timed_mutex teleBookMutex;
13
14 void addToTeleBook(const std::string& na, int tele){
15   std::lock_guard<std::shared_timed_mutex> writerLock(teleBookMutex);
16   std::cout << "\nSTARTING UPDATE " << na;
17   std::this_thread::sleep_for(std::chrono::milliseconds(500));
18   teleBook[na] = tele;
19   std::cout << "  ... ENDING UPDATE " << na << '\n';
20 }
21
22 void printNumber(const std::string& na){
23   std::shared_lock<std::shared_timed_mutex> readerLock(teleBookMutex);
24   std::cout << na << ": " << teleBook[na];
25 }
26
27 int main(){
28
29   std::cout << '\n';
30
31   std::thread reader1([]{ printNumber("Scott"); });
32   std::thread reader2([]{ printNumber("Ritchie"); });
33   std::thread w1([]{ addToTeleBook("Scott", 1968); });
34   std::thread reader3([]{ printNumber("Dijkstra"); });
35   std::thread reader4([]{ printNumber("Scott"); });
36   std::thread w2([]{ addToTeleBook("Bjarne", 1965); });
37   std::thread reader5([]{ printNumber("Scott"); });
38   std::thread reader6([]{ printNumber("Ritchie"); });
39   std::thread reader7([]{ printNumber("Scott"); });
40   std::thread reader8([]{ printNumber("Bjarne"); });
41
42   reader1.join();
43   reader2.join();
44   reader3.join();
reader4.join();
reader5.join();
reader6.join();
reader7.join();
reader8.join();
w1.join();
w2.join();

std::cout << '\n';

std::cout << "\nThe new telephone book" << '\n';
for (auto teleIt: teleBook){
  std::cout << teleIt.first << " : " << teleIt.second << '\n';
}

std::cout << '\n';

}
```

问题在于第24行的调用 `teleBook[na]` 可能会修改电话簿。你可以通过将读取线程 `reader8` 放在其他读取线程前面来引发数据竞争。我在C++研讨会上把这个程序用作一种练习。练习内容是找出数据竞争。大约10%的参与者在5分钟内发现了数据竞争。

## 11.1.2 最小化可变数据的共享

出于性能和安全性两方面的原因，你应该最小化可变数据的共享。安全性主要涉及数据竞争。本段我将重点讨论性能，正确性问题将在接下来的最佳实践部分讨论。

在“计算向量的和”一章中，我进行了一项详尽的性能研究：我能够以多快的速度对 `std::vector` 的值求和？

这是单线程求和的关键部分。

### 单线程求和

```cpp
...
constexpr long long size = 100000000;

std::cout << '\n';

std::vector<int> randValues;
randValues.reserve(size);

// random values
std::random_device seed;
std::mt19937 engine(seed());
std::uniform_int_distribution<> uniformDist(1, 10);

const unsigned long long sum = std::accumulate(randValues.begin(),
                                               randValues.end(), 0);
...
```

之后，我在四个线程上执行求和。一开始我天真地使用了一个共享的求和变量。

### 使用共享变量的多线程求和

```cpp
...
void sumUp(unsigned long long& sum, const std::vector<int>& val,
           unsigned long long beg, unsigned long long end){
  for (auto it = beg; it < end; ++it){
    std::lock_guard<std::mutex> myLock(myMutex);
    sum += val[it];
  }
}
...
```

通过使用原子求和变量做了一点优化。

### 使用原子变量的多线程求和

```cpp
...
void sumUp(std::atomic<unsigned long long>& sum, const std::vector<int>& val,
           unsigned long long beg, unsigned long long end){
    for (auto it = beg; it < end; ++it){
        sum.fetch_add(val[it]);
    }
}
...
```

而我的性能提升来自在本地计算部分和。

### 使用局部变量的多线程求和

```cpp
...
void sumUp(unsigned long long& sum, const std::vector<int>& val,
           unsigned long long beg, unsigned long long end){
    unsigned long long tmpSum{};
    for (auto i = beg; i < end; ++i){
        tmpSum += val[i];
    }
    std::lock_guard<std::mutex> lockGuard(myMutex);
    sum += tmpSum;
}
...
```

这些性能数据令人印象深刻，也给出了明确的指示：你共享的状态越少，从核心中获得的性能就越多。

Linux 上各种求和方式的性能

| 单线程 | std::lock_guard | 原子 | 局部求和 |
| --- | --- | --- | --- |
| 0.07 秒 | 3.34 秒 | 1.34 秒 | 0.03 秒 |

## 11.1.3 最小化等待

你可能听说过阿姆达尔定律¹。它预测了使用多个处理器时你能获得的理论最大加速比。该定律非常简单：如果 p 是你的代码中可并发运行的比例，那么你获得的最大加速比为 $\frac{1}{1-p}$。因此，如果你的代码中 90% 可以并发运行，你最多只能获得 10 倍加速：$\frac{1}{1-p} = \frac{1}{1-0.9} = \frac{1}{0.1} = 10$。

换个角度看，如果你因为使用锁而不得不串行运行 10% 的代码，那么你最多也只能获得 10 倍加速。当然，这里我假设你可以使用无限的处理资源。

下图明确展示了阿姆达尔定律的一个直接后果。

![](img/d61a6c83410484053b8892275d2fcc4f_552_0.png)

作者：Daniels220，来自英文维基百科，CC BY-SA 3.0，https://commons.wikimedia.org/w/index.php?curid=6678551

最优核心数在很大程度上取决于代码的并行部分。例如：如果代码中有 50% 是并行的，那么使用 16 个核心即可达到峰值性能；使用更多核心并不会让程序更快。如果代码中有 95% 是并行的，那么使用 2048 个核心可以达到峰值性能。

¹ https://en.wikipedia.org/wiki/Amdahl%27s_law

## 11.1.4 优先使用不可变数据

数据竞争是指至少两个线程同时访问一个共享变量，并且至少有一个线程试图修改该变量的情况。这个定义使问题显而易见：数据竞争的一个必要条件是可变的共享状态。下图清楚地说明了我的观点。

**可变？**

| 共享？ | 否 | 是 |
| --- | --- | --- |
| **否** | OK | OK |
| **是** | OK | 数据竞争 |

*可变且共享的状态*

如果你拥有不可变数据，就不会发生数据竞争。你只需要保证这些不可变数据以线程安全的方式初始化。在“线程安全初始化”一章中，我介绍了四种保证这一点的方法，如下所示：

- 在创建线程之前进行早期初始化
- 常量表达式
- 函数 `std::call_once` 与标志 `std::once_flag` 结合使用
- 具有块作用域的静态变量

在 C++ 中，有两种典型的方式创建不可变数据：`const` 和 `constexpr`。`const` 是一种运行时技术，而 `constexpr` 保证值在编译时初始化，因此是线程安全的。甚至用户自定义类型也可以在编译时初始化。

### 11.1.4.1 用户自定义类型

对于其实例应在编译时创建的用户自定义类型，存在一些限制。

`constexpr` 构造函数

- 只能使用常量表达式调用。
- 不能使用异常处理。
- 必须声明为 default 或 delete，或者函数体必须为空（C++11）。

constexpr 用户自定义类型

- 不能有虚基类。
- 要求每个基类对象和每个非静态成员在构造函数的初始化列表中或直接在类体内初始化。因此，所使用的每个构造函数（例如基类的构造函数）都必须是 constexpr 构造函数，并且所使用的初始化器必须是常量表达式。

cppreference.com¹ 提供了关于 constexpr 用户自定义类型的更多信息。为了将理论付诸实践，我定义了类 MyInt。MyInt 展示了刚才提到的要点，该类还拥有 constexpr 成员函数。

### 不可变的用户自定义类型

```cpp
// userdefinedTypes.cpp

#include <iostream>
#include <ostream>

class MyInt{
public:
    constexpr MyInt() = default;
    constexpr MyInt(int fir, int sec): myVal1(fir), myVal2(sec){}
    MyInt(int i){
        myVal1 = i - 2;
        myVal2 = i + 3;
    }

    constexpr int getSum() const { return myVal1 + myVal2; }

    friend std::ostream& operator<< (std::ostream &out, const MyInt& myInt){
        out << "(" << myInt.myVal1 << "," << myInt.myVal2 << ")";
        return out;
    }

private:
    int myVal1 = 1998;
    int myVal2 = 2003;

};

int main(){
```

¹ https://en.cppreference.com/w/cpp/language/constexpr


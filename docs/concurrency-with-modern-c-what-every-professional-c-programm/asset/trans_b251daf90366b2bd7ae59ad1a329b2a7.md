
```cpp
public:
    TeleBook(const std::string& teleBookFile_): teleBookFile(teleBookFile_){
        auto fileStream = openFile(teleBookFile);
        auto fileContent = readFile(std::move(fileStream));
        teleBook = createTeleBook(fileContent);
        std::cout << "teleBook.size(): " << teleBook.size() << '\n';
    }

    map get() const {
        std::lock_guard<std::mutex> lockTele(teleBookMutex);
        return teleBook;
    }

    int getNumber(const std::string& name) const {
        std::lock_guard<std::mutex> lockTele(teleBookMutex);
        return teleBook[name];
    }

    void setNewNumber(const std::string& name) {
        std::lock_guard<std::mutex> lockTele(teleBookMutex);
        teleBook[name]++;
    }

private:

    std::ifstream openFile(const std::string& myFile){
        std::ifstream file(myFile, std::ios::in);
        if (!file){
            std::cerr << "Can't open file " + myFile + "!" << '\n';
            exit(EXIT_FAILURE);
        }
        return file;
    }

    std::string readFile(std::ifstream file){
        std::stringstream buffer;
        buffer << file.rdbuf();
        return buffer.str();
    }

    map createTeleBook(const std::string& fileCont){
        map teleBook;

        std::regex regColon(":");
        std::regex_token_iterator fileContIt(fileCont.begin(), fileCont.end(),
                                        regColon, -1);
        const std::regex_token_iterator fileContEndIt;

        std::string entry;
        std::string key;
        int value;
        while (fileContIt != fileContEndIt) {
            entry = *fileContIt++;
            auto comma = entry.find(",");
            key = entry.substr(0, comma);
            value = std::stoi(entry.substr(comma + 1, entry.length() - 1));
            teleBook[key] = value;
        }
        return teleBook;
    }
};

std::vector<std::string> getRandomNames(const map& teleBook) {

        std::vector<std::string> allNames;
        for (const auto& pair: teleBook) allNames.push_back(pair.first);

        std::random_device randDev;
        std::mt19937 generator(randDev());

        std::shuffle(allNames.begin(), allNames.end(), generator);

        return allNames;
}

void getNumbers(const std::vector<std::string>& randomNames, TeleBook& teleBook) {
        for (const auto& name: randomNames) teleBook.getNumber(name);
}

int main() {

        std::cout << '\n';

        // get the filename
        const std::string myFileName = "tele.txt";
        TeleBook teleBook(myFileName);

        std::vector<std::string> allNames = getRandomNames(teleBook.get());
        std::vector<std::string> tenthOfAllNames(allNames.begin(),
                allNames.begin() + allNames.size()/10);

auto start = std::chrono::steady_clock::now();

auto futReader0 = std::async(std::launch::async,
        [&]{ getNumbers(allNames, teleBook); });
auto futReader1 = std::async(std::launch::async,
        [&]{ getNumbers(allNames, teleBook); });
auto futReader2 = std::async(std::launch::async,
        [&]{ getNumbers(allNames, teleBook); });
auto futReader3 = std::async(std::launch::async,
        [&]{ getNumbers(allNames, teleBook); });
auto futReader4 = std::async(std::launch::async,
        [&]{ getNumbers(allNames, teleBook); });
auto futReader5 = std::async(std::launch::async,
        [&]{ getNumbers(allNames, teleBook); });
auto futReader6 = std::async(std::launch::async,
        [&]{ getNumbers(allNames, teleBook); });
auto futReader7 = std::async(std::launch::async,
        [&]{ getNumbers(allNames, teleBook); });
auto futReader8 = std::async(std::launch::async,
        [&]{ getNumbers(allNames, teleBook); });
auto futReader9 = std::async(std::launch::async,
        [&]{ getNumbers(allNames, teleBook); });

auto futWriter = std::async(std::launch::async, [&]{
  for (const auto& name: tenthOfAllNames) teleBook.setNewNumber(name);
});

futReader0.get(), futReader1.get(), futReader2.get(), futReader3.get(),
futReader4.get(), futReader5.get(), futReader6.get(), futReader7.get(),
futReader8.get(), futReader9.get(), futWriter.get();

std::chrono::duration<double> duration = std::chrono::steady_clock::now()
    - start;

std::cout << "Process time: " << duration.count() << " seconds" << '\n';

std::cout << '\n';
}
```

让我从 TeleBook 类的构造函数（第 25 - 30 行）开始。它打开文件，读取内容，并创建电话簿。getRandomNames 函数（第 86 - 97 行）生成一个任意的

## 12.4.2 Windows (cl.exe)

### 12.4.2.1 独占锁定

```text
C:\Users\rainer>exclusiveLockingTelebook.exe

teleBook.size(): 88799
Process time: 0.121072 seconds

C:\Users\rainer>
```

初始电话簿

### 12.4.2.2 共享锁定

```text
C:\Users\rainer>sharedLockingTelebook.exe

teleBook.size(): 88799
Process time: 0.217009 seconds

C:\Users\rainer>
```

初始电话簿

老实说，Windows 上的数字让我很惊讶，因为共享锁定在 Windows 上比独占锁定慢两倍。看起来，将 std::shared_lock 和 std::lock_guard 与 std::shared_timed_mutex 一起使用是一种重量级操作，因此共享并不划算。

## 12.5 避免漏洞

不要将数据结构的内部实现传递给客户端。内部实现可以通过引用或指针传递给外部世界。将任意可调用对象传递给数据结构会打开一个漏洞，这个漏洞难以且具有挑战性地被发现。

### 接口中的漏洞

```cpp
1  // lockDouble.cpp
2
3  #include <future>
4  #include <iostream>
5  #include <mutex>
6
7  class LockDouble {
8  public:
9      double get() const {
10         std::lock_guard<std::mutex> lockDoubleGuard(lockDoubleMutex);
11         return lockDouble;
12     }
13
14     void set(double val) {
15         std::lock_guard<std::mutex> lockDoubleGuard(lockDoubleMutex);
16         lockDouble = val;
17     }
18
19     template <typename Func>
20     void apply(Func func){
21         std::lock_guard<std::mutex> lockDoubleGuard(lockDoubleMutex);
22         func(lockDouble);
23     }
24
25
26  private:
27     double lockDouble{};
28     mutable std::mutex lockDoubleMutex;
29
30  };
31
32  int main(){
33
34     LockDouble lck1;
35
36     auto fut1 = std::async([&lck1]{ lck1.set(20.11); });
37     auto fut2 = std::async([&lck1]{ std::cout << lck1.get() << '\n'; });
38
39     double* loophole = nullptr;
40     lck1.apply([&loophole](double& d) mutable { loophole = &d; });
41     *loophole = 11.22;
42
43     auto fut3 = std::async([&lck1]{ std::cout << lck1.get() << '\n'; });
}
```

LockDouble 类有一个干净的接口。对变量 lockDouble 的每次访问都由放入 std::lock_guard 中的同一个互斥锁 lockDoubleMutex 保护。成员函数 get 返回一个副本，而不是对 lockDouble 的非 const 引用。如果成员函数 get 返回对 lockDouble 的非 const 引用，客户端就很容易产生数据竞争。

```cpp
double& get() {
    std::lock_guard<std::mutex> lockDoubleGuard(lockDoubleMutex);
    return lockDouble;
}
...
LockDouble lck;
lck.set(22.11);
double& d = lck.get();
d = 11.22;
```

当然，问题在于引用 d 可以修改本应由互斥锁 lockDoubleMutex 保护的 lockDouble。我认为这个问题很容易发现。

第 19 - 23 行的成员函数 apply 打开了这个漏洞。我在第 40 行创建了一个返回对 lockDouble 引用的 lambda 函数。表达式 *loophole = 11.22 在没有同步的情况下修改了 lockDouble 的值。当然，这会造成数据竞争。屏幕截图显示了非同步访问 lockDouble 的影响。

![](img/d61a6c83410484053b8892275d2fcc4f_593_0.png)

同步和非同步访问 lockDouble

ThreadSanitizer¹ 明确地展示了数据竞争。

![](img/d61a6c83410484053b8892275d2fcc4f_594_0.png)

使用 ThreadSanitizer 检测数据竞争

## 12.6 争用

并发客户端请求是很少使用还是经常使用你的数据结构？当争用较低时，像锁这样简单的同步原语通常就足够快了。使用原子操作这样复杂且具有挑战性的解决方案可能有些过犹不及。在采用高级解决方案之前，你应该先进行测量。为了了解锁的成本有多高，让我做一个简单的测试。

现在，我可以长话短说。我曾在“计算向量的和”一章中做过这个测试。我用 1 到 10 之间的一亿个任意但均匀分布² 的数字填充了一个 std::vector。然后我以各种方式计算了这些数字的和。其中两种方式对本节尤其有趣。

### 12.6.1 无同步的单线程求和

首先，我展示直接了当的基于范围的 for 循环来计算总和。

¹ https://github.com/google/sanitizers/wiki/ThreadSanitizerCppManual

² https://en.wikipedia.org/wiki/Uniform_distribution_(continuous)

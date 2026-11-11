
### 10.1.5 优点和缺点

在我给出主动对象模式的一个最小实现之前，先说明它的优点和缺点。

- **优点：**
  - 同步仅在主动对象的线程上需要，而在客户端线程上不需要。
  - 客户端（用户）与服务器（实现者）之间清晰分离。同步方面的挑战由实现者一侧承担。
  - 由于请求的异步执行，系统的吞吐量得到提升。调用处理密集型的成员函数不会阻塞整个系统。
  - 调度器可以实现多种策略来执行待处理的请求。若如此，作业的执行顺序可以与其入队顺序不同。
- **缺点：**
  - 如果请求过于细粒度，主动对象模式的性能开销（例如代理、激活列表和调度器）可能会过大。
  - 由于调度器的调度策略以及操作系统的调度，调试主动对象模式往往相当棘手。尤其当作业的执行顺序与其入队顺序不同时，更是如此。

### 10.1.6 实现

下面的示例给出了主动对象模式的一个简化实现。特别地，我没有为主动对象上的方法请求定义一个应由代理和服务者实现的接口。此外，调度器在被请求时执行下一个作业，而主动对象的 run 成员函数负责创建线程。

涉及的类型 `future<vector<future<pair<bool, int>>>>` 往往相当冗长。为了提高可读性，我大量使用了 using 声明（第 16 - 37 行）。

```cpp
// activeObject.cpp
#include <algorithm>
#include <deque>
#include <functional>
#include <future>
#include <iostream>
#include <memory>
#include <mutex>
#include <numeric>
#include <random>
#include <thread>
#include <utility>
#include <vector>

using std::async;
using std::boolalpha;
using std::cout;
using std::deque;
using std::distance;
using std::for_each;
using std::find_if;
using std::future;
using std::lock_guard;
using std::make_move_iterator;
using std::make_pair;
using std::move;
using std::mt19937;
using std::mutex;
using std::packaged_task;
using std::pair;
using std::random_device;
using std::sort;
using std::thread;
using std::uniform_int_distribution;
using std::vector;

class IsPrime {
public:
    pair<bool, int> operator()(int i) {
        for (int j = 2; j * j <= i; j++) {
            if (i % j == 0) return make_pair(false, i);
        }
        return make_pair(true, i);
    }
};

class ActiveObject {
public:

    future<pair<bool, int>> enqueueTask(int i) {
        IsPrime isPrime;
        packaged_task<pair<bool, int>(int)> newJob(isPrime);
        auto isPrimeFuture = newJob.get_future();
        auto pair = make_pair(move(newJob), i);
        {
            lock_guard<mutex> lockGuard(activationListMutex);
            activationList.push_back(move(pair));
        }
        return isPrimeFuture;
    }

    void run() {
        vector<jthread> allServers;
        // only one thread because the activation list is the bottleneck
        for (int n = 0; n < 1; ++n) {
            allServers.emplace_back([this] {
                while (!runNextTask());
            });
        }
    }

private:

    bool runNextTask() {
        lock_guard<mutex> lockGuard(activationListMutex);
        auto empty = activationList.empty();
        if (!empty) {
            auto myTask = std::move(activationList.front());
            activationList.pop_front();
            myTask.first(myTask.second);
        }
        return empty;
    }

    deque<pair<packaged_task<pair<bool, int>(int)>, int >> activationList;
    mutex activationListMutex;
};

vector<int> getRandNumbers(int number) {
    random_device seed;
    mt19937 engine(seed());
    uniform_int_distribution<> dist(1000000, 1000000000);
    vector<int> numbers;
    for (long long i = 0; i < number; ++i) numbers.push_back(dist(engine));
    return numbers;
}

future<vector<future<pair<bool, int>>>> getFutures(ActiveObject& activeObject,
                                                    int numberPrimes) {
101    return async([&activeObject, numberPrimes] {
102        vector<future<pair<bool, int>>> futures;
103        auto randNumbers = getRandNumbers(numberPrimes);
104        for (auto numb : randNumbers) {
105            futures.push_back(activeObject.enqueueTask(numb));
106        }
107        return futures;
108    });
109 }
110
111 int main() {
112
113     cout << boolalpha << '\n';
114
115     ActiveObject activeObject;
116
117     // a few clients enqueue work concurrently
118     auto client1 = getFutures(activeObject, 1998);
119     auto client2 = getFutures(activeObject, 2003);
120     auto client3 = getFutures(activeObject, 2011);
121     auto client4 = getFutures(activeObject, 2014);
122     auto client5 = getFutures(activeObject, 2017);
123
124     // give me the futures
125     auto futures = client1.get();
126     auto futures2 = client2.get();
127     auto futures3 = client3.get();
128     auto futures4 = client4.get();
129     auto futures5 = client5.get();
130
131     // put all futures together
132     futures.insert(futures.end(), make_move_iterator(futures2.begin()),
133                     make_move_iterator(futures2.end()));
134
135     futures.insert(futures.end(), make_move_iterator(futures3.begin()),
136                     make_move_iterator(futures3.end()));
137
138     futures.insert(futures.end(), make_move_iterator(futures4.begin()),
139                     make_move_iterator(futures4.end()));
140
141     futures.insert(futures.end(), make_move_iterator(futures5.begin()),
142                     make_move_iterator(futures5.end()));
143
144     // run the promises
146 activeObject.run();
147
148 // get the results from the futures
149 vector<pair<bool, int>> futResults;
150 futResults.reserve(futures.size());
151 for (auto& fut: futures) futResults.push_back(fut.get());
152
153 sort(futResults.begin(), futResults.end());
154
155 // separate the primes from the non-primes
156 auto prIt = find_if(futResults.begin(), futResults.end(),
157     [](pair<bool, int> pa){ return pa.first == true; });
158
159 cout << "Number primes: " << distance(prIt, futResults.end()) << '\n';
160 cout << "Primes:" << '\n';
161 for_each(prIt, futResults.end(), [](auto p){ cout << p.second << " "; });
162
163 cout << "\n\n";
164
165 cout << "Number no primes: " << distance(futResults.begin(), prIt) << '\n';
166 cout << "No primes:" << '\n';
167 for_each(futResults.begin(), prIt, [](auto p){ cout << p.second << " "; });
168
169 cout << '\n';
170
171 }
```

首先，这个示例的整体思路是客户端可以并发地将作业入队到激活列表。服务者的工作是判断哪些数是素数，而激活列表是主动对象的一部分。主动对象在一个单独的线程上运行入队到激活列表中的作业，客户端可以请求结果。

下面是细节。五个客户端通过 getFutures 函数将工作入队到 activeObject（第 119 - 123 行）。getFutures 接收 activeObject 和 numberPrimes。会生成 numberPrimes 个介于 1000000 和 1000000000 之间的随机数（第 103 行；范围见第 93 行），并将它们推入返回值：vector<future<pair<bool, int>>。future<pair<bool, int>> 保存一个 bool 和一个 int。这个 bool 表示该 int 是否为素数。让我们更仔细地看第 105 行：futures.push_back(activeObject.enqueueTask(numb))。这个调用会触发将一个新作业入队到激活列表（第 58 行）。对激活列表的所有调用都必须受到保护。激活列表是一个由 promise 组成的 deque（第 86 行）：deque<pair<packaged_task<pair<bool, int>(int)>, int>>。每个 promise 在被调用时执行函数对象 isPrime（第 38 - 46 行）。返回值是一个由 bool 和 int 组成的 pair。这个 bool 表示该 int 数字是否为素数。

现在，工作包已经准备好。让我们开始计算。所有客户端在第 126 - 130 行返回其关联 future 的句柄。将所有 future 放在一起（第 133 - 143 行）让我的工作更轻松。

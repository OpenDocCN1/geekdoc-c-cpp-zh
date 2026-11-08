
```cpp
void main_program() {
    std::thread th{ &task1 };
    try {
        std::vector data{ 0,1,2 };
        data.at(666);              // triggers out_of_range
    } catch(std::runtime_error& ex) { // does not match out_of_range
        /*...*/                    // handle specific error here
    } catch(...) {
        th.join();
        throw;                     // continue error handling outside
    }
    th.join();                     // waits after Okay or specific error
}

int main() {
    try {
        main_program();
    } catch(...) {
        std::cout << "An error has occurred\n";
    }
}
```

现在，`th` 实例的生命周期与可能出错的运算分离开来。在示例中，我区分两类异常：一类是“我需要在本地处理特定情况”的 `std::runtime_error`；另一类是其他所有异常……这类异常我并不预期在本地发生，但知道或假定会在更外层被处理——这就是为什么在重要的 `th.join()` 之后用 `throw;` 重新抛出，交给外层处理。我尽可能晚地调用 `join()`，因为该调用会一直等待线程中的运算结束（该调用阻塞）。如果我提前调用，比如在启动后立即调用，那就无法并行执行了。

使用 `jthread` 就简单多了！因为等待发生在析构函数中，即使在异常情况下也是如此：

```cpp
// https://godbolt.org/z/87dZEGf3d
void mainProgram() {
    std::jthread th{ &task1 };
    std::vector data{ 0,1,2 };
    data.at(666);              // triggers out_of_range
}
```

`main()` 函数保持不变。尽管 `data.at(666)` 抛出异常，`jthread` 仍会执行到底，因为 `th` 的析构函数包含 `join()`。因此，你会在控制台上先看到 `fib(40)=102334155`，然后看到 `An error has occurred`。

## “jthread”的析构函数

`jthread` 的析构函数做两件事：

-   在线程函数的 `stop_token` 上调用 `request_stop()`。
-   使用 `join()` 等待线程函数结束。

这意味着，当你的 `jthread` 变量（比如 `t`）离开作用域时，其析构函数会被调用。如果你的线程函数没有 `stop_token` 作为参数，线程将继续运行直到结束，尽管它很可能应该被停止。

因此，你应该始终给线程函数一个 `stop_token` 作为参数，并时不时用 `stop_requested()` 检查是否应停止。即使你从未在外部调用 `request_stop()`，析构函数也会调用它。

## 29.1.5 向线程函数传递参数

如果必须为每次不同的 `fib` 调用都编写一个单独的函数来设置参数 `n` 再调用 `fib`，那将非常不实用。你也可以在启动线程时直接传递参数。为此，只需在 `thread` 的初始化器中添加所需的参数即可。

```cpp
// https://godbolt.org/z/bMdrWrd4c
#include <iostream>
#include <thread>
using std::cout; using std::endl;

long fib(long n) { return n<=1 ? n : fib(n-1)+fib(n-2); }
void runFib(long n) {
    auto r = fib(n);
    cout << "fib("<<n<<")=" << r << endl;
}
long ack(long m, long n) { // Ackermann function
    if(n==0) return n+1;
    if(m==0) return ack(m-1, 1);
    return ack(m - 1, ack(m, n-1));
}
void runAck(long m, long n) {
    auto r = ack(m, n);
    cout << "ack("<<m<<','<<n<<")=" << r << endl;
}

int main(){
    std::jthread f40{ runFib, 40 };
    std::jthread f41{ runFib, 41 };
    std::jthread f42{ runFib, 42 };

    f40.join(); f41.join(); f42.join();

    std::jthread a1{ runAck, 4, 0 };
    std::jthread a2{ runAck, 4, 1 };
    std::jthread a3{ runAck, 2, 700 };
    std::jthread a4{ runAck, 3, 10 };
}
```

**清单 29.3** 在构造函数中向线程函数添加参数。

你可以简单地额外传递一个或多个参数给 `jthread` 的构造函数。

> **阿克曼函数与斐波那契**
>
> 在本书中，我经常以不同变体使用 `fib(n)` 函数（计算第 *n* 个斐波那契数）作为计算的示例。第 *n* 个斐波那契数是第 *n* - 1 个和第 *n* - 2 个斐波那契数之和。前几个数是 1, 1, 2, 3, 5, 8, 13, 21——数列以此延续。
>
> 我喜欢使用它，原因有二：第一，这个函数可以用一行代码写出；第二，它能让计算机忙上一阵子。对于 `fib(40)`，计算机已经需要几秒钟来计算；`fib(45)` 则成了耐心的考验。不过，只有当你像我这里一样天真地*递归*编写时才会如此。多花点功夫，你也可以写出高效的函数，如清单 29.3 所示。但对于线程示例，我并不想这样做。
>
> 更极端的是*阿克曼*函数。它有两个参数，增长极其迅速，尤其是当第一个参数 *m* 增大时。该函数最初是为了展示自动计算的极限而设计的，因此非常适合我的线程示例。它的数值不如斐波那契数那么直观，除了规模迅速增长之外，也不太有意思。
>
> 为节省篇幅，接下来我将假定 `ack` 和 `runAck` 函数已定义。

### 参数总是被复制

参数在线程启动之前会被复制到线程中。因此，不会存储引用。于是，每个线程都会创建新的字符串。

```cpp
// https://godbolt.org/z/fbnbKzrs1
#include <iostream>
#include <thread>
#include <chrono>
using namespace std::chrono; // seconds, suffix s

void delayPrint(seconds s, const std::string& msg) {
    std::this_thread::sleep_for(s);
    std::cout << msg << std::endl;
}
int main() {
    std::jthread m1{ delayPrint, 1s, "On your marks" };
    std::jthread m2{ delayPrint, 2s, std::string{"set"} };
    std::string go = "go";
    std::jthread m3{ delayPrint, 3s, go };
}
```

**清单 29.4** 参数被复制到线程中。

尽管 `go` 可以作为局部变量被引用，并且 `delayPrint` 的参数 `msg` 是 `const string&`，但 `go` 仍然会先被复制，再传递给线程函数 `delayPrint`。这确保了即使你在 `m3` 上调用 `detach()` 并离开其作用域，线程函数那个可能很重要的引用参数依然存在。

和往常一样，在使用原始指针时需要格外小心。因为这里在传递给线程函数之前只复制了指针，当然不会复制它所指向的内容。这样做的结局会很糟糕。

```cpp
// https://godbolt.org/z/hvq5dbzde
#include <iostream>
#include <thread>
#include <chrono>
using namespace std::chrono; // seconds, suffix s

void delayPrint(seconds s, const char* msg) {  // ⚠ raw pointer
    std::this_thread::sleep_for(s);
    std::cout << msg << std::endl;             // ⚠ this won't work
}

void run() {
    const char risk[] = "This won't end well...";
    std::jthread t{ delayPrint, 1s, risk };    // ⚠ raw pointer
    t.detach();
    // here the scope of 'risk' is left
}
int main() {
    run();
    std::this_thread::sleep_for(2s);           // wait another 2 seconds
}
```

**清单 29.5** 使用原始指针作为参数时要小心。

这里，一旦退出 `run()`，`risk` 就被销毁了。`msg` 指针仍然指向它原来的位置，也就是一个无效区域；结果是未定义行为。

### 强制引用参数

然而，在某些情况下，你需要的是引用，而复制参数可能不切实际或根本不可能。这时可以用 `std::ref` 来强制引用。

```cpp
// https://godbolt.org/z/GnsWYyecv
#include <iostream>
#include <thread>
#include <chrono>
using namespace std::chrono; // seconds, suffix s

struct State {
    int counter;
};

void showState(const State& state) {
    for(auto i : {5,4,3,2,1}) {
        std::cout << "counter: " << state.counter << std::endl;
        std::this_thread::sleep_for(1s);
    }
}

int main() {
    State state { 4 };
    std::jthread th{showState, std::ref(state)}; // remains reference to state
    std::this_thread::sleep_for(1s);
    state.counter = 501;
    std::this_thread::sleep_for(1s);
    state.counter = 87;
    std::this_thread::sleep_for(1s);
    state.counter = 2;
}
```

**清单 29.6** 使用 `ref` 强制引用。

这里的局部变量 `state` 作为引用被传递给新线程，并且始终保持引用。不会创建副本，正如你所见，`main` 中对 `state.counter` 的更改也会影响 `showState`。否则，输出应该一直是 `counter: 4`，而不是下面这样：

```text
counter: 4
counter: 501
counter: 87
counter: 2
counter: 2
```


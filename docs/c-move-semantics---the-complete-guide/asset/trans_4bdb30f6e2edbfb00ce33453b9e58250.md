

因此，通过引用迭代共享指针集合的集合要便宜得多：

```
std::vector<std::shared_ptr<...>> coll;
...
for (auto sp : coll) {      // expensive
    ...
}
...
for (const auto& sp : coll) { // cheap
    ...
}
```

关于移动语义，因此最好移动共享指针而不是复制它们。例如，不要这样实现：

```
std::shared_ptr<int> lastPtr;                 // init shared pointer that does not own anything
while (...) {
    auto ptr{std::make_shared<int>(getValue())};  // init shared pointer that owns new int
    ...
    lastPtr = ptr;                               // expensive (note: ptr no longer used)
}                                              // ptr destroyed, lastPtr is the only owner
```

最好这样实现：

```
std::shared_ptr<int> lastPtr;                 // init shared pointer that does not own anything
while (...) {
    auto ptr{std::make_shared<int>(getValue())};  // init shared pointer that owns new int
    ...
    lastPtr = std::move(ptr);                    // cheap
}                                              // ptr destroyed, lastPtr is the only owner
```

因此，具有共享指针成员的对象在对象被移动时将失去对这些成员指向的资源的拥有权。这对性能有好处，但可能会创建无效的已移动-from状态。因此，你应该仔细检查具有 std::shared_ptr<> 类型成员的已移动-from对象的状态。

## 15.4.2 Move Semantics for std::unique_ptr<>

类模板 std::unique_ptr<> 实现了独占拥有的概念。类型系统确保在任何时候只能有一个对象的所有者。诀窍是使用类型系统来禁用复制唯一指针的任何尝试。因为此检查是在编译时完成的，所以这种方法在运行时不会引入任何显著的性能开销。

你可以在源函数中创建一个唯一的指针并将其返回给调用者：

lib/uniqueptr1.cpp

```
#include <iostream>
#include <string>
#include <memory>
```

```
std::unique_ptr<std::string> source()
{
    static long id{0};

    // create string with new and let ptr own it:
    auto ptr = std::make_unique<std::string>("obj" + std::to_string(++id));
    ...
    return ptr;        // transfer ownership to caller
}

int main()
{
    std::unique_ptr<std::string> p;
    for (int i = 0; i < 10; ++i) {
        p = source();    // p gets ownership of the returned object
                         // (previously returned object of source() is deleted)
        std::cout << *p << '\n';
        ...
    }
} // last-owned object of p is deleted
```

与已移动-from类型的通常做法一样，要将所有权传递给接收函数，你只能使用 std::move() 传递它：

```
std::vector<std::unique_ptr<std::string>> coll;
std::unique_ptr<std::string> up;
...
coll.push_back(up);            // ERROR: copying disabled
coll.push_back(std::move(up)); // OK, moves ownership into new element of coll
```

如果你将唯一指针传递给可能接收函数的潜在接收函数，该函数按引用接收参数，你就不知道所有权是否已被移动。是否移动所有权取决于函数的实现。在这种情况下，你可以使用 operator bool() 再次检查状态：

```
std::unique_ptr<std::string> up;
...
sink(std::move(up)); // might move ownership to sink()
if (up) {            // does it still have the ownership?
    ...
}
```

或者，你可以确保所有权已消失（资源已释放）：

```
std::unique_ptr<std::string> up;
...
sink(std::move(up)); // might move ownership to sink()
up.reset();          // ensure ownership is gone (resource deleted)
```

## 15.5 Move Semantics for IOStreams

IOStreams 在 C++98 中引入，作为可从中读取或写入的东西的抽象（标准 I/O、文件，甚至字符串）。早期的设计决策是不可能复制这些对象（复制表示打开文件的对象意味着什么，有两个句柄指向同一个文件或复制文件，以及如何同步访问？）。

然而，自 C++11 以来，移动语义允许我们移动 IOStream 对象并使用临时流。

### 15.5.1 Moving IOStream Objects

考虑以下示例：

lib/outfile.cpp

```
#include <iostream>
#include <fstream>
#include <stream>

std::ofstream openToWrite(const std::string& name)
{
    std::ofstream file(name);            // open a file to write to
    if (!file) {
        std::cerr << "can't open file '" << name << "'\n";
        std::exit(EXIT_FAILURE);
    }
    return file;                         // return ownership (open file)
}

void storeData(std::ofstream fstrm)      // takes ownership of file (but this might change)
{
    fstrm << 42 << '\n';
}                                        // closes the file

int main()
{
    auto outFile{openToWrite("iostream.tmp")};  // open file
    storeData(std::move(outFile));               // store data

    // better ensure that the file is closed:
    if (outFile.is_open()) {
        outFile.close();
    }
}
```

这里，函数 openToWrite() 打开并返回一个输出文件流：

```
std::ofstream openToWrite(const std::string& name)
{
    std::ofstream file(name);        // open a file to write to
    ...
    return file;                     // return ownership (open file)
}
```

我们使用返回值来初始化 outFile 并将其传递给 storeData()：

```
auto outFile{openToWrite("iostream.tmp")};  // open file
storeData(std::move(outFile));               // store data
```

因为 storeData() 按值接收参数，所以它接收打开文件的所有权。因此，在 storeData() 结束时，文件将被关闭：

```
void storeData(std::ofstream fstrm)  // takes ownership of file (but this might change)
{
    ...
}                                         // closes the file
```

然而，storeData() 也可能按引用接收参数，这意味着它不一定接收所有权。在这种情况下，你可能希望之后再次检查传递的参数 outFile 的状态：

```
// better ensure that the file is closed:
if (!outFile.is_closed()) {
    outFile.close();
}
```

调用 outFile.close() 通常足够，但如果文件已被关闭，则会设置文件流的 failbit。

### 15.5.2 Using Temporary IOStreams

自 C++11 以来，IOStreams 库还提供了用于接收右值引用的函数重载，这使我们能够接收临时对象。例如：

```
std::string s = "hello, world";
std::ofstream("fstream1.tmp") << s << '\n';          // OK since C++11
```

你甚至可以以这种方式将字符串文字写入流（这在 C++11 之前就可以编译，但使用 operator<<(const void*) 写入字符串文字的地址）：

```
std::ofstream("fstream1.tmp") << "hello, world\n";   // correct since C++11
                                                       // (wrote address before)
```

以同样的方式，你可以使用临时字符串流解析给定的字符串：

```
std::string name, firstname, lastname;
...
name = "Tina Turner";
std::istringstream{name} >> firstname >> lastname;    // OK since C++11
```

```
threads.push_back(std::thread{doThat, std::move(someArg)});
...

// wait for all threads to end:
for (auto& t : threads) {
    t.join();
}
```

这里，我们启动两个线程并将它们放入所有正在运行的线程的集合中：

```
std::vector<std::thread> threads;    // better std::jthread since C++20

std::string someArg{"black lives matter"};
threads.push_back(std::thread{doThis, someArg});
threads.push_back(std::thread{doThat, std::move(someArg)});
```

我们通过声明 std::thread 类型（或更好，自 C++20 起为 std::jthread）的对象并将临时对象移动到 threads 中来启动线程。在可调用对象（函数、lambda、函数对象）的参数后面，我们可以传递额外的参数，这些参数在线程启动时传递给可调用对象。默认情况下，线程类的构造函数会复制这些参数。使用 std::move()，我们在这里切换到移动语义。因此，doThis() 接收传递字符串 someArg 的副本，而 doThat() 接收字符串的移动值。

最后，我们等待所有线程结束（使用 std::thread 时避免核心转储是必要的）：

```
// wait for all threads to end:
for (auto& t : threads) {
    t.join();
}
```

### 15.6.2 Futures, Promises, and Packaged Tasks

对于在两个线程之间同步交换（返回）值的一些辅助类型，也使用了仅可移动类型（futures、promises 和 packaged tasks 都是仅可移动的）。

考虑以下示例：

lib/future.cpp

```
#include <iostream>
#include <string>
#include <vector>
#include <thread>
#include <future>

void getValue(std::promise<std::string> p)
{
```


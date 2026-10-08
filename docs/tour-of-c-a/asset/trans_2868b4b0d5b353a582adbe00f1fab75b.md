

```cpp
void f(vector<double>& v); // Il函数：对 v 进行操作
```

```cpp
struct F {
    vector<double>& v; // Il函数对象：对 v 进行操作
    F(vector<double>& v, double vv) :v(vv) {}
    void operator()(); // Ill运算符：$7.3.2
};
```

```cpp
int main() {
    vector<double> some_vec(1, 2, 3, 4, 5, 6, 7, 8, 9);
    vector<double> vec2(10, 11, 12, 13, 14);
    thread t1(f, some_vec); // Il f(some_vec) 在另一个线程中执行
    thread t2(F(vec2)); // Il F(vec2) 在另一个线程中执行
}
```

F(vec2) 将参数保存到 F 中的 vector 中。F 现在可以使用 vec2，并且希望在它执行期间没有其他任务接受 vec2。通过按值传递 vec2 则会消除这种风险。

使用 `{ref(some_vec)}` 的初始化使用了一个线程变长模板构造函数，该构造函数可以接受任意序列的参数 ($8.4)。`ref` 是来自 `<functional>` 的一个类型函数，遗憾的是，它需要告诉变长模板将 `some_vec` 视为引用而非对象。如果没有 `ref()`，`some_vec` 将按值传递。编译器会检查在给定后续参数的情况下是否调用了第一个参数，并构建必要的函数对象以传递给线程。因此，如果 `F::operator()` 和 `f` 执行相同的算法，那么处理这两个任务的方式是等价的：在两种情况下，都为线程构造了一个执行所需的函数对象。

## 18.2.2 返回结果

在示例 §18.1 中，我通过非 const 引用引用传递参数。只有当我预计任务会修改所引用数据的值时，我才会这样做 ($1.7)。这是一种返回结果的隐晦方法，但并不罕见。不那么晦涩的技术是通过 const 引用传递输入数据，并将存放结果的位置作为单独的参数传递：

点击此处查看代码图像

```cpp
void f(const vector<double>& v, double* res); // Il 来自 v 的输入，将结果存放在 *res 中
```

```cpp
class F {
public:
    F(const vector<double>& vv, double* p) :v(vv), res(p) // Il 将结果存放在 *res 中
    void operator()();
private:
    const vector<double>& v; // Il 输入源
    double* res; // Il 输出目标
};
```

```cpp
double g(const vector<double>&); // Il 使用返回值
```

```cpp
void user(vector<double>& vec1, vector<double> vec2, vector<double> vec3) {
    double res1;
}
```

```cpp
double res2;
double res3;
```

```cpp
thread t1 ({f(vec1),&res1}); // f 在另一个线程中执行
thread t2({F(vec2,&res2)}); // F(vec2,&res2)() 在另一个线程中执行
thread t3 ({&](){ res3 = g(vec3); }); // 通过引用捕获局部变量
```

```cpp
t1.join(); // 使用结果前 join
t2.join();
t3.join();

cout << res1 << ' ' << res2 << ' ' << res3 << " \n";
```

}, `cref(vec1)` 为 vec1 创建一个 const 引用作为 t1 的参数。

这种方法是有效的，而且这种技术非常常见，但我认为通过引用返回结果并不特别优雅，因此我在 §18.5.1 中会回到这个话题。

## 18.3 共享数据

有时任务需要共享数据。在这种情况下，必须对访问进行同步，以便一次只有一个任务可以访问。经验丰富的程序员会识别出这是一个简化（例如，许多任务同时读取数据没有问题），但请考虑如何确保一次只有一个任务可以访问给给对象。

## 18.3.1 互斥锁与锁

互斥锁（mutex，“互斥访问对象”）是线程间通用数据共享的关键元素。线程使用 `lock()` 操作获取互斥锁：

点击此处查看代码图像

```cpp
mutex m;
int sh;

void f() {
  scoped_lock lock(m); // 获取互斥锁
  sh += 7; // 操作共享数据
 // 隐式释放互斥锁
```

这里使用的锁类型是 `scoped_lock<mutex>` (§7.2.3)。`scoped_lock` 构造函数通过调用 `m.lock()` 获取互斥锁。如果另一个线程已经获取了互斥锁，该线程将等待（“阻塞”），直到另一个线程完成。一旦线程获得了对共享数据的访问权限，`scoped_lock` 会释放互斥锁（调用 `m.unlock()`）。当互斥锁被释放时，等待它的线程将执行（“被唤醒”）。互斥和锁定设施可以在 `<mutex>` 中找到。

注意 RAII 使用 (§6.3)。使用资源句柄（如 `scoped_lock` 和 `unique_lock` (§18.4)）比显式锁定和解锁互斥锁更简单更安全。

共享数据与互斥锁之间的对应关系取决于：程序员必须知道哪个互斥锁应该对应哪个数据。显然，这是容易出错的，同样明显的是，我们试图通过各种语言手段使对应关系变得清晰。例如：

```cpp
class Record {
public:
    mutex rm;
    // ...
}
```

不需要天才也能猜到，对于名为 `rec` 的 `Record`，你应该在访问 `rec` 之前获取 `rec.mutex`，尽管注释或更好的命名可能对读者有所帮助。

同时访问多个资源以执行某些操作并不罕见。这可能导致死锁。例如，如果 thread1 获取了 mutex1 并尝试获取 mutex2，而 thread2 获取了 mutex2 并尝试获取 mutex1，那么它们一个都无法继续执行。`scoped_lock` 通过允许我们同时获取多个锁来提供帮助：

点击此处查看代码图像

```cpp
void f() {
    scoped_lock lock {mutex1,mutex2,mutex3}; // 获取所有三个锁
    // ... 操作共享数据
} // 释放所有互斥锁
```

这个 `scoped_lock` 只会在获取所有互斥锁参数后发生，并且在等待互斥锁时永远不会阻塞（“进入睡眠”）。`scoped_lock` 的析构函数确保在线程离开作用域时释放互斥锁。

通过共享数据进行通信是非常底层的。特别是，程序员必须设计方法来了解哪些操作是有效的且尚未被各种任务完成。在这方面，使用共享数据优于“调用和返回”的概念。另一方面，有些人坚信共享互斥锁比复制参数和返回值更高效。当涉及大量数据时，情况确实如此，但锁定和解锁是相对昂贵的操作。另一方面，现代机器非常擅长复制数据，尤其是廉价数据，而人们为了“效率”不经思考地使用共享数据进行通信，最好还没有经过测量。

基础互斥锁允许一个线程一次访问数据。共享数据最常见的方式之一是在许多读者和一个写入者之间共享。这种“读写锁”模式由 `shared_mutex` 支持。读者将以“共享”方式获取互斥锁以便他人也能访问，而写入者将要求专用访问。例如：

点击此处查看代码图像

```cpp
shared_mutex mx; // 可以共享的互斥锁
void reader() {
    scoped_lock lock {mx}; // 与其他读者共享访问
    // ... 读取 ...
}
```

```cpp
void writer() {
    unique_lock lck{mx}; // 需要专用（唯一）访问
    // ... 写入 ...
}
```

## 18.3.2 原子变量

`mutex` 是一种涉及系统的重量级机制。它允许在无数据竞态的情况下执行任意工作。然而，对于极少量的工作，有一种更简单廉价的机制：原子变量。例如，这里是双检查锁定的一种简单变体：

点击此处查看代码图像

```cpp
mutex mut;
atomic<bool> init_x; // Il 初始为 false
use X; // Il 需要复杂的初始变量
if (!init_x) {
    lock_guard lck(mut);
    if (!init_x) {
        // ... 对进行复杂的初始化 ...
        init_x = true;
    }
}
```

`atomic` 为我们避免了大部分对昂贵 `mutex` 的使用。如果 `init_x` 不是原子的，初始化将频繁失败，导致神秘且难以发现的错误，因为在 `init_x` 上存在数据竞态。

在这里，我使用 `lock_guard` 而不是 `scoped_lock`，是因为我只需要一个 `mutex`，所以简单的锁（`lock_guard`）就足够了。

## 18.4 等待事件

有时，“线程”需要等待某些事件，例如另一个线程完成任务或经过某些时间。使用位于 `<chrono>` 中的时间设施，我可以这样写：

点击此处查看代码图像

```cpp
using namespace chrono; // Il 见 $16.2.1
auto t0 = high_resolution_clock::now();
this_thread::sleep_for(milliseconds(20));
auto t1 = high_resolution_clock::now();
cout << duration_cast<nanoseconds>(t1-t0).count() << " nanoseconds passed\n";
```


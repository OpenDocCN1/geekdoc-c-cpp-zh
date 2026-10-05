

## 828 C++ 简介

它不能被复制。特别地，它不提供拷贝构造函数或拷贝赋值函数。
然而，正如我们稍将看到的，允许将所有权从一个 `unique_ptr` 对象转移到另一个。
例如：

```cpp
auto p1(make_unique<int>(10));
std::cout << *p1; // 输出 10。
unique_ptr<int> p2; // 可以指向整数的 unique_ptr。
unique_ptr<int> p3(p1); // 编译错误。
p2 = p1; // 编译错误。
```

尝试复制对象会导致编译错误。当将它按值传递给函数时情况也是如此。例如：

```cpp
int main()
{
    ...
unique_ptr<double> p1;
    g(p1);
}
void g(unique_ptr<double> p2)
{
}
```

当调用 `g(p1)` 时，因为 `p1` 是按值传递的，尝试复制会导致编译错误。如何修复它？通过传递引用使得不产生拷贝。例如，程序显示什么？

```cpp
#include <iostream> // 示例 25.9
#include <memory>
using namespace std;

void g(unique_ptr<double>& p2);

int main()
{
    auto p1(make_unique<double>(1.2));
    g(p1);
    cout << *p1 << '\n';
    return 0;
}

void g(unique_ptr<double>& p2)
{
    cout << *p2 << '\n';
    *p2 = 3.4;
}
```

程序显示 1.2 和 3.4。注意，`unique_ptr` 对象不能被复制这一规则有一个例外。我们可以复制一个即将被销毁的 `unique_ptr` 对象。例如，编译器允许从函数返回的 `unique_ptr` 对象赋值给另一个对象：

```cpp
#include <iostream> // 示例 25.10
#include <memory>
using namespace std;

unique_ptr<double> f();

int main() {
    auto p1 = f();
    cout << *p1 << '\n';
    return 0;
}
```

```cpp
unique_ptr<double> f() {
    auto p2 = make_unique<double>();
    *p2 = 1.2;
    return p2; /* 我们可以避免声明 p2 并直接写入；
    return make_unique<double>(1.2); */
}
```

当 `f()` 返回时，`p1` 获得了 `p2` 原本拥内存的所有权。编译器允许此操作是有逻辑的，因为它知道 `p2` 是一个局部变量，将被销毁，不会有两个对象指向同一块内存。内会在 `p1` 销毁时释放。程序显示 1.2。

让我们将 `f()` 改返回普通指针并比较这两种方法：

```cpp
void g() {
    double* p1;
    p1 = f();
    // 如果我们忘记 delete p1; 就会产生内存泄漏。
}
```

```cpp
double* f() {
    double* p2 = new double();
    *p2 = 1.2;
    return p2;
}
```

`g()` 负责释放 `f()` 中分配的内存。如果我们忘记释放它，就会产生内存泄漏。特别地，当 `f()` 返回时，`p1` 将销毁，它指向的内存不会被释放。如果我们把 `g()` 改为返回 `p1`，那么内存应该由调用 `g()` 的函数释放，依此类推。使用 `unique_ptr`，我们不需要担心内存的释放，因为内会在它销毁的对象处释放。

正如所说，我们不能将一个 `unique_ptr` 复制给另一个。然而，如果我们想将所有权转移到 `unique_ptr` 对象并在另一个位置再次使用该对象，可以使用 `move()` 函数。例如：

```cpp
int main() {
    unique_ptr<double> p1, p2;
    auto p3 = make_unique<double>();

    *p3 = 3.4;
    p1 = move(p3); /* 我们使用 move() 将所有权从 p1 转移到 p2。
    正如提到的，如果我们写 p2 = p1; 将会导致编译错误。 */
    p2 = move(p1); // 我们将 p3 的所有权转移到 p1。
    cout << *p3 << '\n'; // 操作
    cout << *p2 << '\n';
    return 0;
}
```

程序显示 3 和 1。注意，当所有权转移时，程序员有责任不要使用指针（例如 `p3`）访问内存，否则执行过程中会出现问题。让我们看另一个使用 `unique_ptr` 管理为许多元素分配内存的示例。将其与普通指针对比：

```cpp
class T {
private:
  int *p;
public:
  T(int num) {p = new int[num];}
  ~T() {delete[] p;}
};
int main() {
  T t(100);
}
```

使用普通指针（例如 `p`）时，不应忘记释放内存，否则会导致内存泄漏。特别地，如果我们使用 `unique_ptr`，就不需要担心这些问题。将类改为：

```cpp
class T {
private:
  unique_ptr<int> p;
public:
  T(int num) : p(make_unique<int>(num)) {} // C++14 语法
  T(int num) : p(new int[num]) {} // 旧版语法
};
```

在 `unique_ptr` 的声明中，我们放入数据。与普通指针相比，为了管理元素可以使用索引符号（例如 `p[0]=10`）。当 `t` 销毁时，`delete[]` 将调用以释放内存。我们不需要这样做；智能指针会为我们做。这简化了事情并防止了内存泄漏。当然，永远不要忘记 `vector`，这比普通指针或 `unique_ptr` 对象灵活得多。我认为这足够获得一个概念。更多信息可以查阅标准库。

## 25 命名空间、类型转换和智能指针

### shared_ptr 类型

与 `unique_ptr` 类似，创建一个 `shared_ptr` 对象时，我们将指针指向的类型放在内部。例如：

```cpp
shared_ptr<int> p1;
shared_ptr<vector<int>> p2; // p2 可以指向整数向量。
shared_ptr<string> p3("test"); // 这段代码输出 test。
```

`shared_ptr` 类型用于我们想要在 `shared_ptr` 对象之间管理内存所有权的情况。即 `shared_ptr` 对象管理相同的内存。事实上这意味着它的作用。例如：

```cpp
#include <iostream> // 示例 25.11
#include <memory>
using std::shared_ptr;
using std::cout;

int main() {
    shared_ptr<int> p1(new int);
    shared_ptr<int> p2;
    shared_ptr<int> p3(new int[10]);

    *p1 = 10;
    p2 = p1;
    p3[0] = 100; // 从 C++17 开始支持索引。
    cout << *p1 << '\n';
    return 0;
}
```

通过语句 `p2 = p1`，`p1` 和 `p2` 对象管理相同的内存。因此程序输出 20。`shared_ptr` 如何工作？它有一个引用计数器，每当 `shared_ptr` 对象指向同一块内存时，计数器就会增加。例如，当使用 `shared_ptr` 对象来初始化一个新的时（例如 `shared_ptr<int> p4(p1)`）；或者在赋值中使用时（例如 `p4 = p1`）。当按值传递给函数时，计数器也会增加。例如：

```cpp
void f() {
    shared_ptr<int> p(new int);
    g(p);
}
```

```cpp
void g(shared_ptr<int> sp) {
    ...
}
```

因为参数按值传递，所以计数器变为 2。当 `g()` 结束时，局部变量 `sp` 被销毁，计数器变为 1。

当将新值赋给 `shared_ptr` 指针或 `shared_ptr` 被销毁时（例如超出作用域），计数器减一。当它变为零时，即最后一个 `shared_ptr` 对象销毁时，它指向的内存会被释放。例如：

```cpp
shared_ptr<string> p(new string);
shared_ptr<string> q(new string);
p = q; // 现在 p 指向相同的内存
```

注意，如果用普通指针编写内容，原始内存不会被释放。例如：

```cpp
string *p = new string;
string *q = new string;
```

如果我们想在一步内分配并初始化内存，可以使用 `make_shared<T>()`。事实上，为了效率，建议返回一个指向分配内存的 `shared_ptr`。例如：

```cpp
shared_ptr<int> p1 = make_shared<int>(10);
shared_ptr<int> p2 = make_shared<int>(20);
shared_ptr<vector<int>> p3 = make_shared<vector<int>>(10);

p3[0] = 100; // 从 C++17 开始支持索引。
cout << *p1 << '\n';
return 0;
```

通过语句 `p2 = p1`，`p1` 和 `p2` 对象管理相同的内存。因此程序输出 20。
`shared_ptr` 如何工作？它有一个引用计数器，每当 `shared_ptr` 对象指向同一块内存时，计数器就会增加。例如，当使用 `shared_ptr` 对象来初始化一个新的时（例如 `shared_ptr<int> p4(p1)`）；或者在赋值中使用时（例如 `p4 = p1`）。当按值传递给函数时，计数器也会增加。例如：

```cpp
void f() {
    shared_ptr<int> p(new int);
    g(p);
}
```

```cpp
void g(shared_ptr<int> sp) {
    ...
}
```

因为参数按值传递，计数器变为 2。当 `g()` 结束时，局部变量 `sp` 被销毁，计数器变为 1。

### weak_ptr 类型

`weak_ptr` 是一种指向由 `shared_ptr` 对象管理的内存的智能指针。`weak_ptr` 与 `shared_ptr` 的关联不会增加引用计数。也就是说，当最后一个 `shared_ptr` 对象销毁时，它指向的内存会被释放，无论存在多少个关联的 `weak_ptr` 对象。事实上这意味着它的作用。当 `weak_ptr` 使用该指针时，我们可以先检查内存是否仍然可以被管理，然后访问它。让我们看一个示例：

```cpp
#include <iostream> // 示例 25.13
#include <memory>
using namespace std;

int main() {
    shared_ptr<int> p1 = make_shared<int>(10);
    weak_ptr<int> w1 = p1;
    if (w1.lock()) {
        cout << *w1.lock() << '\n';
    }
    p1.reset();
    if (w1.lock()) {
        cout << *w1.lock() << '\n';
    } else {
        cout << "memory is released" << '\n';
    }
    return 0;
}
```


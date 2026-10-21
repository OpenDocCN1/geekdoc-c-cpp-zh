

在 C++11 和 C++14 中，你必须按值或按引用传递 this：

```cpp
class C {
private:
std::string name;
public:
...
void foo() {
auto l1 = [this] { std::cout << name << '\n'; }; // OK
auto l2 = [] { std::cout << name << '\n'; }; // OK
auto l3 = [&] { std::cout << name << '\n'; }; // OK
...
}
};
```

然而，这里的问题在于，即使拷贝 this，捕获的仍然是底层对象的引用（因为只拷贝了指针）。如果 lambda 的生命周期超过了调用该成员函数的对象的生命周期，这就会成为问题。一个关键的示例是，lambda 定义了新线程的任务，而该线程应该使用对象自身的拷贝，以避免任何并发或生命周期问题。另一个原因可能只是传递带有当前状态的对象副本。

自 C++14 起就有了一种变通方法，但可读性和效果都不太好：

```cpp
class C {
private:
std::string name;
public:
...
void foo() {
auto l1 = [thisCopy=*this] { std::cout << thisCopy.name << '\n'; };
...
}
};
```

例如，程序员在同时使用 = 或 & 捕获其他对象时，仍然可能会意外地使用 this：

```cpp
auto l1 = [&, thisCopy=*this] {
thisCopy.name = "new";
std::cout << name << '\n'; // OOPS: still the old name
};
```

从 C++17 开始，你可以通过捕获 *this 来显式请求捕获当前对象的拷贝：

```cpp
class C {
private:
std::string name;
public:
...
}
```

```cpp
void foo() {
    auto l1 = [*this] { std::cout << name << '\n'; };
    ...
};
```

也就是说，捕获 *this 意味着当前对象的一个拷贝被存储在 lambda 定义的闭包对象中。

你仍然可以将捕获 *this 与其他捕获方式结合使用，只要在处理 this 时不产生矛盾：

```cpp
auto l2 = [&, *this] { ... }; // OK

auto l3 = [this, *this] { ... }; // ERROR
```

下面是一个完整的示例：

```cpp
#include <iostream>
#include <string>
#include <thread>

class Data {
private:
    std::string name;
public:
    Data(const std::string& s) : name(s) {
    }
    auto startThreadWithCopyOfThis() const {
        // start and return new thread using this after 3 seconds:
        using namespace std::literals;
        std::thread t([*this] {
            std::this_thread::sleep_for(3s);
            std::cout << name << '\n';
        });
        return t;
    }
};

int main() {
    std::thread t;
    {
        Data d{"c1"};
        t = d.startThreadWithCopyOfThis();
        // d is no longer valid
    }
    t.join();
}
```

该 lambda 捕获 *this 的一个拷贝，这意味着传递的是 d 的副本。因此，即使线程可能在 d 的析构函数被调用之后才使用传入对象，也不会产生问题。

如果我们使用 [this]、[=] 或 [&] 捕获 this，线程将遭遇未定义行为，因为在传递给线程的 lambda 中打印 name 时，lambda 会使用已销毁对象的成员。

## 6.3 通过 const 引用捕获

使用新的库工具，你现在还可以通过 const 引用捕获对象。

## 6.4 后记

constexpr lambda 最初由 Faisal Vali、Ville Voutilainen 和 Gabriel Dos Reis 在 http://wg21.link/n4487 中提出。最终接受的标准文本由 Faisal Vali、Jens Maurer 和 Richard Smith 在 http://wg21.link/p0170r1 中拟定。

在 lambda 中捕获 *this 最初由 H. Carter Edwards、Christian Trott、Hal Finkel、Jim Reus、Robin Maffeo 和 Ben Sander 在 http://wg21.link/p0018r0 中提出。最终接受的标准文本由 H. Carter Edwards、Daveed Vandevoorde、Christian Trott、Hal Finkel、Jim Reus、Robin Maffeo 和 Ben Sander 在 http://wg21.link/p0180r3 中拟定。

# 第7章

# 新的属性及属性特性

自 C++11 起，就可以指定属性（启用或禁用警告的正式注解）。C++17 引入了新的属性。此外，属性现在可以在更多的地方使用，并带来了一些额外便利。

## 7.1 属性 [[nodiscard]]

新属性 [[nodiscard]] 可用于在函数返回值未被使用时促使编译器发出警告（但编译器并非必须发出警告）。

[[nodiscard]] 通常应用于在未使用返回值时提示行为不当。行为不当可能包括：

-   内存泄漏，例如未使用返回的已分配内存
-   意外或非直观的行为，例如未使用返回值时得到不同/意外的行为
-   不必要的开销，例如在未使用返回值时调用了一个空操作

下面是一些使用该属性有用的示例：

-   分配资源且必须由另一个函数调用释放的函数应标记为 [[nodiscard]]。一个典型示例是分配内存的函数，例如 malloc() 或分配器的成员函数 allocate()。
-   然而，请注意某些函数可能返回一个值，但意味着不需要进行补偿调用。例如，程序员调用 C 函数 realloc() 并传入零字节大小来释放内存，这样就不必保存返回值以便稍后调用 free()。因此，将 realloc() 标记为 [[nodiscard]] 会适得其反。
-   一个很好的函数示例是 std::async()（C++11 引入），当不使用其返回值时，其行为会不直观地改变。std::async() 在后台异步启动一个功能，并返回一个句柄，可用于等待所启动功能的结束（并访问任何返回值或异常）。然而，当返回值未被使用时，调用会变成同步调用，因为未使用的返回值的析构函数会立即被调用，等待所启动功能结束。因此，不使用返回值会静默地与调用 std::async() 的整个目的相矛盾。当 std::async() 被标记为 [[nodiscard]] 时，编译器可以对此发出警告。
-   另一个示例是成员函数 empty()，它检查对象（容器/字符串）是否没有元素。程序员经常调用这个函数来“清空”容器（移除所有元素）：

```
cont.empty();
```

这种对 empty() 的错误应用通常可以通过未使用其返回值来检测到。因此，相应地标记该成员函数：

```
class MyContainer {
    ...
    public:
        [[nodiscard]] bool empty() const noexcept;
    ...
};
```

有助于检测这种逻辑错误。

如果出于任何原因你不想使用标记为 [[nodiscard]] 的返回值，你可以将返回值强制转换为 void：

```
(void)coll.empty();  // disable [[nodiscard]] warning
```

注意，如果函数被覆盖，函数声明中的属性不会被继承：

```
struct B {
    [[nodiscard]] int* foo();
};

struct D : B {
    int* foo();
};
```

```
B b;
b.foo();        // warning
(void)b.foo();  // no warning
```

```
D d;
d.foo();        // no warning
```

因此，你必须再次用 [[nodiscard]] 标记派生成员函数（除非在派生类中不使用返回值是有意义的）。

像往常一样，你可以将应用于函数的属性放在所有声明说明符之前或函数名之后：

```
class C {
    ...
    [[nodiscard]] friend bool operator== (const C&, const C&);
    friend bool operator!= [[nodiscard]] (const C&, const C&);
```

};

将属性放在 friend 和 bool 之间或 bool 和 operator== 之间是不正确的。

尽管该语言特性是在 C++17 中引入的，但标准库中尚未使用它。在该库中应用此特性的提案来得太晚，未能赶上 C++17。因此，该特性的关键动机之一——将其添加到 std::async() 的声明中——尚未实现。不过，对于上面讨论的所有示例，相应的修复将在下一个 C++ 标准中到来（参见 http://wg21.link/p0600r1 提案，已为 C++20 接受）。

然而，为了使你的代码更具可移植性，你应该使用 [[nodiscard]]，而不是使用非可移植的手段（例如 gcc 和 clang 的 [[gnu: warn_unused_result]] 或 Visual C++ 的 _Check_return_）来相应地标记函数。

在定义 operator new() 时，你应该用 [[nodiscard]] 标记这些函数，例如在定义头文件以跟踪所有 new 调用时就是这样做的。

## 7.2 属性 [[maybe_unused]]

新属性 [[maybe_unused]] 可用于避免编译器因未使用名称或实体而发出警告。

该属性可应用于类、使用 typedef 或 using 的类型定义、变量、非静态数据成员、函数、枚举类型或枚举项（枚举值）的声明。

一个应用场景是给参数命名，但（不一定）使用它：

```
void foo(int val, [[maybe_unused]] std::string msg)
{
#ifdef DEBUG
    log(msg);
#endif
    ...
}
```

另一个示例是拥有一个未使用的成员：

```
class MyStruct {
    char c;
    int i;
    [[maybe_unused]] char makeLargerSize[100];
    ...
};
```

注意，你不能将 [[maybe_unused]] 应用于语句。因此，你不能直接用 [[maybe_unused]] 来抵消 [[nodiscard]]：

```
[[nodiscard]] void* foo();
```

```
int main()
```


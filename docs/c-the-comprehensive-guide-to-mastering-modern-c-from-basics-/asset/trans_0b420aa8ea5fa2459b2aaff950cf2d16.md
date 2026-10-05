
在这里你看到了所谓的 Meyers 单例模式的实现。*单例*（singleton）是一种在每次使用时都能始终获取类相同实例的方法。这些使用可能来自程序的不同部分，如这里的 `func()` 和 `main()` 所示；因为它们都使用 `getKeyboard()` 函数，所以它们接收的是相同的 `Keyboard&` 引用，因此是同一个对象。

单例模式在多线程程序中特别流行。例如，假设你的程序有多个*线程*（同时运行的程序段），并且每个线程都想从键盘读取数据——为此，它们需要一个 `Keyboard` 类。`Keyboard` 类建立了与实际连接到计算机的键盘的连接。如果它始终是同一个键盘，将会非常有帮助。这正是示例中 `getKeyboard()` 函数应该提供的。

```cpp
Keyboard& getKeyboard() {
    cout << " * getKeyboard()\n";
    static Keyboard keyboard{}; // static local variable
    return keyboard;
}
```

**列表 13.6** Meyers 单例。

在 `getKeyboard()` 中，你看到了静态局部变量 `keyboard`。与*全局*静态变量不同，它并不是在程序启动时（甚至更早）初始化的，而是在第一次通过定义处时精确初始化的。

与非静态局部变量不同，静态变量在离开块时不会被清除。这里的块是 `getKeyboard()` 函数。`keyboard` 变量在重新进入时仍然存在，并且不会重新初始化，而是被重用。

单例设计模式有许多变体，甚至有更多的实现方式，各自有优缺点。有些程序员甚至认为单例本身就是一种糟糕的实践（一种“反模式”）。虽然由于这种讨论超出了本书的范围，但事实确实是，你不应该滥用单例设计模式。

具体到使用静态局部变量实现单例的方法：Meyers 单例模式的优点是实现简单，缺点是无法提供对多个 `Keyboard` 实例的完全保护。你仍然可以使用公共构造函数创建你自己的 `Keyboard{}`。如果你发现这是一个显著缺点，可以通过稍微修改接口来解决这个问题。

静态局部变量的使用在多线程环境下也是安全的：保证只有一个线程会初始化该变量。

## 13.8 "inline namespace"

定义命名空间的最后一种方法与 `inline` 一起使用。如如下列表所示，你可以创建一个**内联命名空间**（inline namespace）。

```cpp
// https://godbolt.org/z/115M1csEE
#include <iostream>
namespace mylib {
    namespace v1 {
        int version() { return 1; }
    }
    inline namespace v2 { // current version
        int version() { return 2; }
    }
}

int main() {
    std::cout << "Version " << mylib::version() << "\n"; // Output: 2
    std::cout << "Version " << mylib::v1::version() << "\n"; // Output: 1
    std::cout << "Version " << mylib::v2::version() << "\n"; // Output: 2
}
```

**列表 13.7** 内联命名空间的标识符也会进入其周围的命名空间。

在 namespace 之前使用 **inline**，你打开了一个普通的命名空间。此外，所有标识符也被包含在周围的命名空间。通过这种方式，你可以将最新的行为封装在**内联命名空间**中，使其成为默认行为。你可以在**列表 13.7** 的 `mylib::version()` 中看到这一点。

如果用户需要旧行为，他们可以显式访问内部命名空间，这里是 `mylib::v1::version()`。

如果用户显式请求，在内部命名空间 `mylib::v2::version()` 中也可以使用新版本。

标准库提供了内联命名空间的更多示例。你可以在第 28 节第 28.4.2 节找到列表。例如，`std::literals` 和 `std::literals::string_literals` 都是内联的。要包含 `string_literals` 中的 `operator""`，你可以使用以下 `...` 选项的其中之一：

```cpp
// direct addressing:
    using namespace std::string_literals;
    auto str = "abc"s;
// use inline namespace string_literals:
    using namespace std::literals;
    auto str = "abc"s;
// use both inline namespaces:
    using std::operator""s;
    auto str = "abc"s;
```

## 13.9 间歇回顾

因为命名空间、`using` 和 `static` 之间可能会产生很多困惑，我将在这里回顾各种使用场景。为了完备性，我还会包含使用 `using` 声明的类型别名。

| 语言元素 | 说明 |
| :--- | :--- |
| namespace xyz {...} | 新的命名空间 xyz |
| namespace {...} | 匿名命名空间；所有标识符均为文件作用域 |
| inline namespace XYZ {...} | 嵌入命名空间 |
| static global variable | 文件局部变量 |
| static free function | 文件局部函数 |
| static data field | 类所有实例间共享的数据字段 |
| static method | 无需特定实例即可调用的方法 |
| static local variable | 周期超出作用域的变量 |
| using namespace xyz | 导入命名空间 xyz 中的所有标识符 |

| 语言元素 | 说明 |
| :--- | :--- |
| using xyz::abc | 从命名空间 xyz 导入标识符 abc |
| using new = old; | 为类型 old 引入类型别名 new |

表 13.1 语言元素的变体

## 13.10 "const"

`const` 关键字用于指定一个值不能被改变。它可以用于许多地方：变量、参数、返回类型和成员函数。在 C++ 中，它被用来指示对象是不可变的。

`const` 的使用在多线程环境下也是安全的：保证常量对象不会被任何线程修改。然而，你必须小心 `const` 的的位置。例如，指向常量的指针与常量指针是不同的。

- const int* ptr: 指向常量型整数的指针
- int* const ptr: 指向整数的常量指针
- const int* const ptr: 指向常量型整数的常量指针

下表说明了 `const` 的用法：

| 语法 | same |
| :--- | :--- |
| const int* ptr | 指针指向的值是常量的 |
| int* const ptr | 指针本身是常量的 |
| const int* const ptr | 值和指针都是常量的 |

## 13.10.1 Const 参数

你已经在第 4 节第 4.2 节中学过，你可以为参数标记 `const`，这通常发生在通过引用传递参数时：

```cpp
void print(const vector<int>& primes) {
    for(auto prime : primes) {
        cout << prime << " ";
    }
}
```

参数 `primes` 不能被修改。任何修改操作如 `primes[7] = 4` 或 `primes.push_back(12)` 都会导致编译错误。对于类和自定义类型，通常选择 `const MyClass& arg` 作为传递方法，因为参数不需要复制。

在 `MyClass arg` 的情况下，它会被复制。你可以在函数内部安全地修改 `arg`——因为它是副本，更改不会影响调用者外部的原始对象——但复制大对象的开销很大。

如果避免复制是值得的，最好使用 `const&`。`&` 避免了复制，而 `const` 防止了意外修改外部对象。

对于内置类型的情况与类的情况无异。然而，它们的复制成本可以忽略不计，这就是为什么很少看到 `const int& const double&`。规则与类相同。编译器会防止对值进行更改：

```cpp
void nonsensicalParameter(const int& arga, const double& argb) {
    arga = 7; // Assignment to constant
}
```

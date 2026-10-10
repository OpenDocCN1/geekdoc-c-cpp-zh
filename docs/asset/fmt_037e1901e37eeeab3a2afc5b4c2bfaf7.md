
```cpp
struct Data {
    // 赋值函数
    Data& operator=(Data copy) { // 按值
        copy.swap(*this);
        return *this;
    }

    void swap(Data& other) { // 成员函数
        using std::swap;
        swap(*this, other);
    }

    friend void swap(Data& a, Data& b); // 全局函数
};
```

`swap` 函数很有用。为了与容器良好协作，最好也提供 `swap` 函数。

RAII 意味着在创建对象——资源时，其初始化也被同步完成。在 C++ 中，这发生在构造函数中。在退出构造函数时，始终留下一个有效的对象是非常重要的。

这意味着，特别是即使发生错误，也不会留下一个无效的对象。如果在构造函数中初始化对象时发生错误，你不能留下半创建的数据结构或仍在阻塞的资源。

有效的一个方面是，关联的析构函数在任何情况下都能独立完全移除对象并释放所有仍然存在的资源。结合起来，这非常有效地实现了基于栈的资源管理。

## 17.2.1 一个 C 语言示例

典型的 C API 通常会将管理任务转移到使用该 API 的代码中。文件对象或数据库连接必须通过对称的调用来打开和关闭。字体、画笔或音视频解码器的句柄需要被获取并显式地释放。如果没有调用释放函数——无论是由于不可预见的事件还是仅仅是遗忘——相关的资源将不会被释放。文件保持打开状态；数据库连接未关闭；画笔和字体的句柄会耗尽。

相应地，在 C 语言中，通常使用特殊的返回值来指示错误。为了指示客户端应该停止使用该资源，许多函数使用特定的错误代码。例如，`mktime()` 在发生错误时返回 `-1` 而不是请求的转换结果。你必须检查 `malloc()` 的返回值是否为空指针。

通常，检查中的错误是极少被预期的结果。人们可能会省略这种检查，因为这种情况“反正根本不会发生”。这样一来，你只能希望这段代码运行在安全至型的环境中。{ 42 }

正由于这种情况很少被预料，我们遇到了异常的情况：在 C++ 世界中，可以使用异常来处理此类错误。不需要检查返回值，因为构造函数必须让对象处于有效状态。如果构造函数通过异常退出，编译器将释放预分配的内存。如果异常通过栈上的多个构造函数（当前函数调用列表）向上传递且没有被匹配的 `catch` 捕获，那么所有之前的构造都将被撤销。只有当构造函数完全执行完毕后，对象才被视为有效的且完全创建的。

一个小型、精简的仅用于封装字符缓冲器的示例类可能如下列表所示。

```cpp
// https://godgodbolt.org/z/9eeG575Wz
struct Buffer {
    const char *data;
    explicit Buffer(unsigned sz) : data(new char[sz]) {}
    ~Buffer() { delete data; }
    Buffer(const Buffer&) = delete;
    Buffer& operator=(const Buffer&) = delete;
};
```

### 列表 17.5 一个 RAII 字符缓冲区类。

应该提到的是——正如“叠猫有十六种方法”的理念，同样的任务使用 `unique_ptr<char[]>` 可能会更好地完成；这只是一个简单的示例。

在 C 语言中，这通常涉及 `malloc`，并且（谨慎或偏执的{43 }）程序员需要检查返回值以查看内存是否分配正确。如果不是，必须以某种方式终止进程。在 C++ 中，`new` 始终返回一个有效指针或抛出 `bad_alloc` 异常。因此构造函数有两个可能的结果；[ 44 ]

- 数据内存已分配，指针是有效的。缓冲区对象被认为正确创建，如果需要清理，析构函数会执行此操作。

- 未分配内存；异常离开了构造函数。因此，缓冲区被认为未创建，没有留下已分配的资源。因为对象没有创建，在任何情况下都不会调用析构函数——即使数据未初始化，从而导致 `delete[]` 极其危险。这种情况永远不会发生。

通过 `= delete` 删除的方法确保了缓冲区不会被意外复制并导致整个数据结构被释放多次：使用 `unique_ptr` 的另一个原因。

## 17.2.2 拥有原始指针

在复杂的对象层次结构中，你还必须准备好对象变量（成员变量）的初始化因异常失败。即使你没有用 `catch` 处理并吞掉它们，而是实际上想让异常传递通过，你可能需要在异常离开当前构造函数之前撤销任何之前的初始化。

与之前的 `Buffer` 类不同，`StereoImage` 的情况并不简单。

```cpp
// https://godbolt.org/z/TK3yTv1EM
struct StereoImage {
    Image *left, *right;
    StereoImage()
        : left(new Image),
        right(new Image) // 危险！
    {}
    ~StereoImage() {
        delete left;
        delete right;
    }
};
```

### 列表 17.6 如果 "right" 抛出异常，“left" 将发生泄漏。

如果这里 `right` 的创建因异常失败，已经为 `left` 分配的内存将不会被释放。因为构造函数是通过异常退出的，`StereoImage` 被视为未创建，其析构函数不会被调用。编译器可以通过调用其析构函数来撤销 `left` 的成功初始化，但这是一个没有析构函数的原始指针！需要另一种机制——带有重新抛出的 `catch`块，或者对 `StereoImage` 的字段使用原始指针以外的其他类型。

以下列表提供了如何避免这种漏洞的一个示例（众多示例之一）。

```cpp
// https://godbolt.org/z/cs4eEEGrf
#include <memory> // unique_ptr
struct Image {
    /* ... */
};
struct StereoImage {
    std::unique_ptr<Image> left, right;
    StereoImage()
        : left(new Image),
        right(new Image)
    {}
};
```

### 列表 17.7 用于“StereoImage”的正确 RAII。

如果 `right` 的初始化因异常失败，那么 `StereoImage`——像之前一样被视为未创建。`StereoImage` 的析构函数不会被调用。然而，`left` 现在有了一个功能完整的析构函数，编译器可以调用它。

通过 `= delete` 删除的方法确保了缓冲区不会被意外复制并导致整个数据结构被释放多次：使用 `unique_ptr` 的另一个原因。

以下列表提供了如何避免这种漏洞的一个示例（众多示例之一）。

通过 `= delete` 删除的方法确保了缓冲区不会被意外复制并导致整个数据结构被释放多次：使用 `unique_ptr` 的另一个原因。

通过 `= delete` 删除的方法确保了缓冲区不会被意外复制并导致整个数据结构被释放多次：使用 `unique_ptr` 的另一个原因。

通过 `= delete` 删除的方法确保了缓冲区不会被意外复制并导致。

这同样适用于所有类型的资源：文件句柄、套接字、互斥量等。

可以将整个 SQLite API 转换为 C++但那是一项巨大的工程。此外，肯定有人为 SQLite 这样流行的 API 做过这件事。希望他们在发生变化时会维护它。

正确的是，人们不想引入另一个依赖项。较小的解决方案可能足够了。将此类代码转换为 RAII 的简单方法是将资源封装在类中。

```cpp
// https://godbolt.org/z/n7Grhh1
#include <sqlite3.h>
#include <string>
#include <stdexcept>

class DbWrapper {
  sqlite3 *db_;
public:
  // 获取资源
  DbWrapper(const string& dbname)
    : db_(nullptr)
  {
    const int errCode = sqlite3_open(dbname.c_str(), &db_);
    if(errCode)
        throw std::runtime_error("Error opening");
  }

  // 释放资源
  DbWrapper() {
    if (db_) sqlite3_close(db_);
  }

  // 访问资源
  sqlite3* operator() { return db_; }

  // 禁止拷贝和赋值
  DbWrapper(const DbWrapper&) = delete;
  DbWrapper& operator=(const DbWrapper&) = delete;
};
```

```cpp
void dbExec(const string &dbname, const string &sql) {
    DbWrapper db(dbname);
    const int errCode = sqlite3_exec(*db, sql.c_str(), nullptr, nullptr, nullptr);
    if(errCode)
        throw std::runtime_error("Error SQL-Exec.");
}
```

### 列表 17.9 带简单 RAII 的 C API。

有了这个包装器，可以在 `sqlite3_exec` 后抛出异常而没有任何问题。当离开 `db` 的范围时——无论是通过异常还是正常——析构函数都会被调用——从而执行 `sqlite3_close()`。

如果在构造函数中发生异常，对象被视为未创建，因此带有 `sqlite3_close()` 的析构函数不会被调用。一个良好的、简单的 RAII 解决方案。

## 17.2.4 并不一定都是异常

虽然在本章讨论 RAII 时我主要处理异常，但 RAII 并不一定与异常的触发绑定。你只需要记住重要的原则，而在处理异常时，陷阱尤为存在。

在不使用 `throw` 的情况下实现 RAII 是完全可能的，转而让用户在构造后检查初始化的成功与否——例如通过转换为 `bool`。

```cpp
// https://githubbolt.org/z/c8xfM1nEa
#include <string>
#include <sqlite3.h>
```

```cpp
class DbWrapper {
    sqlite3 *db_;
public:
    DbWrapper(const std::string& dbname)
        : db_(nullptr) {
        const int errCode = sqlite3_open(dbname.c_str(), &db_);
        if(errCode != nullptr) { // 标记为“未成功”
        }
    }
```

```cpp
sqlite3* operator*() { return db_; };

explicit operator bool() const {
    return db_ != nullptr; // 评估标记
}
```

```cpp
~DbWrapper() {
    if(db_) sqlite3_close(db_);
    // ... 其他部分同上 ...
}
```

```cpp
bool DbExec(const std::string& dbname, const std::string& sql) {
    DbWrapper db( dbname);
    if(db) { // 初始化是否成功
        const int errCode =
        sqlite3_exec(*db, sql.c_str(), nullptr, nullptr, nullptr);
        if(errCode) {
            return false;
        }
    }
    return (bool)db;
}
```

**Listing 17.10** 带有简单 RAII 的 C API，不使用 throw。

至关重要的是，你能够在析构函数中撤销构造函数的所有活动——无论初始化是否成功。在这里通过 `db_ = nullptr` 和析构函数中的检查得以实现。通过 `operator bool()` 的帮助，也可以从外部检查初始化是否成功。在示例中，这也被标记为 `explicit`。在标准库中，例如，流（streams）就是这样工作的——稍后会详细介绍。

同样重要的是，确保所有创建对象的方式都必须留下一个有效的实例。在标准库中，`ostream` 就是这样一个例子：

- `ostream` 创建了一个指向尚未指定的文件的数据流。

- `ostream {"file.txt"}` 在可能的情况下打开该文件。

在任何情况下，析构函数都可以再次清理流。操作（例如通过 `<<`）如果打开文件出错，在第二种变体中以 `void` 结束。因此，在使用它之前，快速用 `if(os)` 检查流是否真的已经准备好写入了。这里的关键在于，`os` 可以被赋值、稍后打开，最重要的是，在任何情况下都能被正确清理。

## 17.2.5 多重构造函数

作为替代设计决策，在发生错误时，可以在 `ostream os("file.txt")` 变体中抛出异常。因此，你必须使用 C 模式：首先检查返回值。这经常被遗忘记，从而导致在下一个 `<<` 处产生意外。

有时，建议进一步偏离纯粹的 RAII 教则。

## 17.2.6 多阶段初始化

通常，在多个阶段中初始化对象更好。典型的 GUI 窗口 API 使用这种方式是：在第一步——在构造函数中——创建不可见的元素；而在 `init()` 方法中进行实际可视化。在这两个阶段之间，窗口和组件被链接在一起并嵌入布局管理器中，并且通常会执行进一步的动态任务。

但无论只执行了构造函数而没有执行 `init`，还是两者都执行了，析构函数都必须能够完全清理对象。

## 17.2.7 在需要的地方定义

几乎直接从 RAII 推导出，人们应该尽可能晚地定义变量并在必要时尽定义——即尽可能靠近实际使用处。

这里的例外当然是紧凑循环，在循环中人们可能想通过使用临时对象来替换昂贵的构造函数调用。然而，在此时你不应该低估编译器和标准库；在紧凑循环中的短字符串可能*仅仅是*不理想的，但在更大的循环中，字符串完全可以在需要的地方被定义。基础数据类型（如 `int` 等）在任何情况下都会被编译器优化掉。

## 17.2.8 不带异常的 "new"

在某些情况下，不应忽略没有 `bad_alloc` 异常确实可能是明智且理想的。例如，某些环境和编译器必须完全管理异常。这在嵌入式和实时领域很常见，尽管这种特殊处理在近年来有所减少。有时你会发现这里无法抛出任何异常——例如，因为你编写了自己的内存管理，或者你确切知道内存请求不会失败。

为了此目的，你可以使用一种特殊形式的 `new` 来强制 `nullptr` 行为。

```cpp
// https://godbolt.org/s/s8Ko4ETs
#include <new>
#include <iostream>
std::string *ps = new (std::nothrow) std::string();
if(ps == nullptr) {
    std::cerr << "Memory allocation failed\n";
    return _ERROR;
}
```

### Listing 17.11 Noth-new 不抛出 "bad_alloc"，但返回 nullptr

某些情况下，不应忽略没有 `bad_alloc` 异常确实可能是明智且理想的。例如，某些环境和编译器必须完全管理异常。这在嵌入式和实时领域很常见，尽管这种特殊处理在近年来有所减少。有时你会发现这里无法抛出任何异常——例如，因为你编写了自己的内存管理，或者你确切知道内存请求不会失败。

为了此目的，你可以使用一种特殊形式的 `new` 来强制 `nullptr` 行为。

一种在节点中存储数据的树的结构。树应该是面向用户的接口，而节点本质上只应该作为数据持有者。

`unique_ptr<Node>` 是 `Node` 的容器，在第 20 章中有详细解释。由于 `Tree` 应该持有任意数据，我将 `Tree` 和 `Node` 写为类模板。因此，你将能够编写类似于 `vector<int>` 的 `Tree<int>`。你将在第 23 章学习到它的具体工作原理。


- **异常** `bad_alloc`

  内存未被分配；异常会离开构造函数。因此，缓冲区被视为未创建，也不会遗留任何已分配的资源。由于对象未被创建，析构函数在任何情况下都不会被调用——即使数据未初始化，因而 `delete[]` 会极其危险。这种情况绝不会发生。

使用 `= delete` 移除的方法确保缓冲区不会被意外复制，进而导致整个内部数据结构被多次释放：这也是使用 `unique_ptr` 的另一个原因。

### 17.2.2 拥有原始指针

在复杂的对象层次结构中，不要忘记，你还必须为对象变量（*成员变量*）的初始化可能因异常而失败做好准备。即使你不使用 catch 处理并吞掉它们，而是实际上想让异常继续传递，你也可能需要在异常离开当前构造函数之前撤销之前的任何初始化。

与前面的 `Buffer` 类不同，`StereoImage` 的情况就没那么简单了。

```cpp
// https://godbolt.org/z/TK3vTv1EM
struct StereoImage {
    Image *left, *right;
    StereoImage()
      : left(new Image)
      , right(new Image) // Danger!
    { }
    ~StereoImage() {
        delete left;
        delete right;
    }
};
```

**代码清单 17.6** 如果“right”抛出异常，“left”会发生泄漏。

如果这里创建 `right` 时因异常失败，那么已经为 `left` 分配的内存将不会被释放。由于构造函数因异常退出，`StereoImage` 被视为未创建，其析构函数也不会被调用。编译器可以通过调用 `left` 的析构函数来撤销其成功的初始化，但这是一个没有析构函数的原始指针！需要另一种机制——带重新抛出的 catch，或者为 `StereoImage` 的字段使用原始指针以外的其他东西。

下面的代码清单给出了如何避免此漏洞的一个示例（众多示例之一）。

```cpp
// https://godbolt.org/z/cs4eEEGrf
#include <memory> // unique_ptr
struct Image {
    /* ... */
};
struct StereoImage {
    std::unique_ptr<Image> left, right;
    StereoImage()
        : left(new Image)
        , right(new Image)
    { }
};
```

**代码清单 17.7** 针对“StereoImage”的正确 RAII。

如果 `right` 的初始化因异常失败，那么 `StereoImage`——和之前一样——被视为未创建。`StereoImage` 的析构函数不会被调用。然而，`left` 现在有一个功能完整的析构函数，编译器可以在栈展开期间调用它。而这反过来会释放 `left` 的内存。

这里的原始指针占用资源内存。这同样适用于所有类型的资源：*文件句柄*、*套接字*、*互斥量*、*信号量*等。

### 17.2.3 从 C 到 C++

正如本章开头所指出的，C++ 开发者也会频繁使用 C API。通常，这涉及通过该 API *请求*和*释放*资源。例如，如果你使用 SQLite 无服务器数据库接口，那么一个简化的代码片段可能如下面的代码清单所示。

```cpp
// https://godbolt.org/z/hG3jPGYv (uses sqlite library)
#include <string>
#include <stdexcept>
#include <sqlite3.h> // library
using std::string; using std::runtime_error;

void dbExec(const string &dbname, const string &sql) {
    sqlite3 *db;
    int errCode = sqlite3_open(dbname.c_str(), &db); // acquire
    if(errCode) {
        throw runtime_error("Error opening the DB.");
    }
    errCode = sqlite3_exec(db, sql.c_str(), nullptr, nullptr, nullptr);
    if(errCode) {
        throw runtime_error("SQL Exec Error.");        // ✘ not good!
    }
    errCode = sqlite3_close(db);                 // release
}
```

**代码清单 17.8** C++ 代码中的 C API。

这里，`database` 资源通过 `sqlite3_open()` 获取，通过 `sqlite3_close()` 释放，并在其间通过 `sqlite3_exec()` 进行操作。当然，因异常退出函数并不是一个好主意：

- 第一个异常是正确的，因为如果 `sqlite3_open()` 未成功，就不需要调用 `sqlite3_close()`。
- 然而，第二个异常会阻止调用 `sqlite3_close()`，资源会被阻塞——或者至少不会被释放——这根据资源类型的不同会产生不同的影响。

当然，可以把整个 SQLite3 API 转换为 C++ API，但这肯定是一项巨大的工程。此外，对于像 SQLite3 这样流行的 API，肯定已经有人完成了这项工作。希望当 C API 发生变化时，他们也能维护它。

理所当然，人们不想引入另一个依赖。更小的解决方案可能也足够了。将此类代码转换为 RAII 代码的一种简单标准方法，是把资源包装在一个包装类中。

```cpp
// https://godbolt.org/z/n7Grhh1GM
#include <sqlite3.h>
class DbWrapper {
    sqlite3 *db_;
public:
    // acquire resource
    DbWrapper(const string& dbname)
        : db_{nullptr}
    {
        const int errCode = sqlite3_open(dbname.c_str(), &db_);
        if(errCode)
            throw runtime_error("Error opening"); // prevents sqlite3_close
    }

    // release resource
    ~DbWrapper() {
        sqlite3_close(db_);                     // release
    }

    // access Resource
    sqlite3* operator*() { return db_; }
    // No copy or assignment
    DbWrapper(const DbWrapper&) = delete;
    DbWrapper& operator=(const DbWrapper&) = delete;
};

void dbExec(const string &dbname, const string &sql) {
    DbWrapper db{ dbname };
    const int errCode = sqlite3_exec(*db, sql.c_str(), nullptr,
        nullptr, nullptr);
    if(errCode)
        throw runtime_error("Error SQL-Exec."); // now it works!
}
```

**代码清单 17.9** 使用简单 RAII 的 C API。

有了这个包装器，在 `sqlite3_exec` 之后抛出异常也不会有任何问题。当离开 `db` 的作用域时——无论是通过异常还是正常离开——析构函数都会被调用——因此也会调用 `sqlite3_close()`。

如果构造函数中发生异常，对象会被视为未创建，因此不会调用包含 `sqlite3_close()` 的析构函数。这是一个良好而简单的 RAII 解决方案。

通过两行带有 `= delete` 的代码，我们防止了意外的赋值和拷贝，否则会导致同一资源 `db_` 被多次释放。

5 更准确地说，文档指出应该这样做，但并非必须。我们将此示例视为资源管理中常见情况的代表，在这种情况下，只有在请求成功时才应进行清理。

### 17.2.4 并不一定非得是异常

尽管在本章讨论 RAII 时我主要处理异常，但 RAII 并不一定与异常的触发绑定。你只需要回想那些重要原则，而陷阱在处理异常时尤其存在。

完全可以在不使用 `throw` 的情况下实现 RAII，而改为让用户在构造之后检查初始化是否成功——例如，通过转换为 `bool`。

```cpp
// https://godbolt.org/z/c8xfM1nEa
#include <string>
#include <sqlite3.h>

class DbWrapper {
    sqlite3 *db_;
public:
    DbWrapper(const std::string& dbname)
        : db_(nullptr)
    {
        const int errCode = sqlite3_open(dbname.c_str(), &db_);
        if(errCode) db_ = nullptr;  // mark as not successful
    }

    sqlite3* operator()() { return db_; }

    explicit operator bool() const {
        return db_ != nullptr;      // evaluate the mark
    }
    ~DbWrapper() {
        if(db_) sqlite3_close(db_);
    }
    // ... Rest as before ...
};

bool dbExec(const std::string &dbname, const std::string &sql) {
    DbWrapper db { dbname };
    if(db) {                         // check for successful initialization
        const int errCode = sqlite3_exec(*db, sql.c_str(), nullptr, nullptr, nullptr);
        if(errCode)
            return false;           // still correct RAII
    }
    return (bool)db;
}
```

**代码清单 17.10** 使用简单 RAII、不使用 throw 的 C API。

关键在于，你能够在析构函数中撤销构造函数的所有活动——无论初始化是否成功。这里通过 `db_ = nullptr` 和析构函数中的检查来确保这一点。借助 `operator bool()`，也可以从外部检查初始化是否成功。在示例中，还用 `explicit` 标记了这一点。例如，在标准库中，流就是这样工作的——但后面会详细说明。

### 17.2.5 多个构造函数

同样重要的是，要确保创建对象的所有方式都必须留下一个有效的实例。在标准库中，`ostream` 就是一个例子：

- `ostream` os 创建一个指向尚未指定文件的数据流。
- `ostream` os {"file.txt"} 打开文件（如果可能）。


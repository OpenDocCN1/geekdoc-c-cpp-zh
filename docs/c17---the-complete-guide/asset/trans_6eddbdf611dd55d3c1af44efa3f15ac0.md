

## 第27章：多线程与并发

请注意，由于类模板参数推导，声明 `lg` 时无需指定互斥量的类型。

此示例用法等价于以下代码，自 C++11 起即可调用：

```cpp
// lock both issue lists:
{
    std::lock(allIssuesMx, openIssuesMx);    // lock with deadlock avoidance
    std::lock_guard<std::mutex> lg1(allIssuesMx, std::adopt_lock);
    std::lock_guard<std::mutex> lg2(openIssuesMx, std::adopt_lock);
    ...  // manipulate both allIssues and openIssues
}
```

因此，如果传递多个互斥量，`scoped_lock` 的构造函数会使用可变参数的便捷函数 `lock(...)`，该函数保证调用不会导致死锁（标准指出：“必须使用诸如尝试并回退之类的死锁避免算法，但具体的算法未指定，以避免过度限制实现”）。

如果仅向 `scoped_lock` 的构造函数传递一个互斥量，它就简单地锁定该互斥量。因此，在只有一个互斥量的 `scoped_lock` 中，构造函数参数的作用类似于 `lock_guard`。它甚至定义了成员 `mutex_type`，而对于多个互斥量则未定义。¹ 因此，你可以用 `scoped_lock` 替换所有 `lock_guard` 的使用。

如果未传递互斥量，锁保护将不起作用。

请注意你也可以采用多个锁：

```cpp
// lock both issue lists:
{
    std::lock(allIssuesMx, openIssuesMx);    // Note: deadlock avoidance algorithm used
    std::scoped_lock lg{std::adopt_lock, allIssuesMx, openIssuesMx};
    ...  // manipulate both allIssues and openIssues
}
```

然而，请注意，采用已锁定互斥量的构造函数现在将 `adopt_lock` 参数放在前面。²

### 27.1.2 std::shared_mutex

C++14 添加了 `std::shared_timed_mutex` 以支持读写锁，其中多个线程可以并发读取值，而偶尔会有线程更新该值。然而，在某些平台上，不支持定时锁的互斥量可以实现得更高效。因此，现在引入了类型 `std::shared_mutex`（自 C++11 起 `std::mutex` 已存在，同时还有 `std::timed_mutex`）。

`std::shared_mutex` 在头文件 `<shared_mutex>` 中定义，并支持以下操作：

如果 `is_always_lock_free` 对原子类型返回 true，则 `is_lock_free()` 对该类型的任何对象都返回 true：

```cpp
if constexpr(std::atomic<T>::is_always_lock_free) {
  assert(std::atomic<>{}.is_lock_free()); // never fails
}
```

该值对应于 C++17 之前必须使用的宏。例如，`std::atomic<int>::is_always_lock_free` 的值为 true 当且仅当 `ATOMIC_INT_LOCK_FREE` 的值为 2（表示“总是”）：

```cpp
if constexpr(std::atomic<int>::is_always_lock_free) {
  // ATOMIC_INT_LOCK_FREE == 2
  ...
}
else {
  // ATOMIC_INT_LOCK_FREE == 0 || ATOMIC_INT_LOCK_FREE == 1
  ...
}
```

用静态成员替换宏的原因是为了提供更强的类型安全并支持在复杂的通用代码中使用这些检查（例如使用 SFINAE）。

请记住，`std::atomic<>` 也可以用于可平凡复制的类型。因此，你也可以检查自己的结构在使用原子时是否需要锁。例如：

```cpp
template<auto SZ>
struct Data {
  bool set;
  int values[SZ];
  double average;
};

if constexpr(std::atomic<Data<4>>::is_always_lock_free) {
  ...
}
else {
  ...
}
```

### 27.3 缓存行大小

程序有时需要处理缓存行大小：

- 一方面，为并发考虑，不同线程访问的不同对象不应属于同一缓存行。否则，当对象并发访问时，缓存行的内存需要在不同线程之间同步。
- 另一方面，你的目标可能是将多个对象放在同一缓存行中，这样访问第一个对象时可以直接访问其他对象，而无需在缓存中加载它们。

为此，C++ 标准库在头文件 `<new>` 中引入了两个内联变量：

```cpp
namespace std {
    inline constexpr size_t hardware_destructive_interference_size;
    inline constexpr size_t hardware_constructive_interference_size;
}
```

这些对象具有以下实现定义的值：

- `hardware_destructive_interference_size` 是在不同线程可能并发访问的两个对象之间推荐的最小偏移，以避免因同一 L1 缓存行受影响而导致性能下降。
- `hardware_constructive_interference_size` 是将两个对象放置在同一 L1 缓存行内的推荐最大连续内存大小。

这两个值只是提示，因为理想值可能取决于具体架构。这些常量是编译器在处理生成代码支持的各种平台时可以提供的最佳值。因此，如果你知道更好，请使用特定值，但使用这些值总比为支持多平台的代码假设任何固定的大小要好。

这两个值都至少为 `alignof(std::max_align_t)`。该值通常相同。然而，从语义上讲，它们代表使用不同对象的不同目的，因此你应按如下方式相应使用它们：

- 如果你想用不同线程访问两个不同的（原子）对象：

  ```cpp
  struct Data {
      alignas(std::hardware_destructive_interference_size) int valueForThreadA;
      alignas(std::hardware_destructive_interference_size) int valueForThreadB;
  };
  ```

- 如果你想用同一线程访问两个不同的（原子）对象：

  ```cpp
  struct Data {
      int valueForThreadA;
      int otherValueForTheThreadA;
  };

  // double-check we have best performance due to shared cache line:
  static_assert(sizeof(Data) <= std::hardware_constructive_interference_size);

  // ensure objects are properly aligned:
  alignas(sizeof(Data)) Data myDataForAThread;
  ```

因此，使用 Request 时，离开作用域将根据是否抛出异常而 `commit()` 或 `rollback()`：

```cpp
{
Request r1{...}; // usually destructor calls commit()
...
if (...) {
throw ...; // let destructor call rollback()
}
...
} // calls commit() in the good case and rollback() on exception
```

然而，此 API 对以下用例不起作用：如果我们在已经处理异常时创建一个新的 Request 对象，该请求将始终 `rollback()`，即使在其使用期间未（进一步）发生异常：

```cpp
try {
...
}
catch (...) {
Request r2{...};
...
} // calls rollback() even if without any additional exception in the catch clause
```

新的标准库函数 `uncaught_exceptions()`（注意名称末尾多了一个 s）解决了这个问题。不同于返回是否正在处理异常，它返回当前未处理的（嵌套）异常的数量。这使我们能够判断出（即使在处理异常时）是否引发了额外的异常。

```cpp
class Request {
private:
...
int initialUncaught{std::uncaught_exceptions()};
public:
...
~Request() {
if (std::uncaught_exceptions() > initialUncaught) {
rollback();
}
else {
commit();
}
}
};
```

现在两个示例场景都能正常工作：

```cpp
try {
    Request r1{...}; // usually destructor calls commit()
    ...
    if (...) {
        throw ...; // let destructor call rollback()
    }
    ...
} // calls commit() in the good case and rollback() on exception
catch (...) {
    Request r2{...};
    ...
} // calls commit() if no additional exception
```

这里，`r2` 的构造函数用 1 初始化 `initialUncaught`，因为我们已在 `catch` 子句内处理异常。然而，当 `r2` 的析构函数被调用且未引发额外异常时，`initialUncaught` 仍为 1，因此会调用 `commit()`。只有在 `catch` 子句内引发第二个未处理异常时，`std::uncaught_exceptions()` 才会返回 2。结果是，`r2` 的析构函数将调用 `rollback()`。

请参阅 `lib/uncaught.cpp` 获取完整示例。

旧的 API `std::uncaught_exception()`（末尾没有 s）自 C++17 起已弃用，不应再使用。

### 28.2 共享指针改进

C++17 为共享指针添加了一些改进。

请注意，此外成员函数 `unique()` 已被弃用。

#### 28.2.1 对原始 C 数组共享指针的特殊处理

自 C++17 起，你可以显式为数组实例化共享指针，以确保析构器调用 `delete[]`（自 C++11 起 `unique` 指针已可实现）。现在你可以简单地调用：

```cpp
std::shared_ptr<std::string[]> p{new std::string[10]};
```

而不是：

```cpp
std::shared_ptr<std::string> p{new std::string[10], std::default_delete<std::string>()};
```

或：

```cpp
std::shared_ptr<std::string> p{new std::string[10], [](std::string* p) { delete[] p; }};
```

以数组形式实例化后，API 也略有变化：你必须使用 `operator[]` 而不是 `operator*`（与原始数组的 `unique` 指针相同）：

```cpp
std::shared_ptr<std::string> ps{new std::string};
*ps = "hello"; // OK
```

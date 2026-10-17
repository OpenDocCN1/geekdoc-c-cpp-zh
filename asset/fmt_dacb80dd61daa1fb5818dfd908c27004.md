
template<typename T>

class initializer_list { // §iso.18.9 public:

using value_type = T;

using reference = const T&; using const_reference = const T&; using size_type = size_t;

using iterator = const T*;

using const_iterator = const T*;

initializer_list() noexcept;

// note const: initializer_list elements are immutable

size_t size() const noexcept; // number of elements const T* begin() const noexcept; // first element const T* end() const noexcept; // one-past-last element };

template<typename T>

const T* begin(initializer_list<T> lst) noexcept { return lst.begin(); }

template<typename T>

const T* end(initializer_list<T> lst) noexcept { return lst.end(); }

```

不幸的是，`initializer_list` 没有提供下标运算符。如果你想使用 `[]` 而不是 `*`，请对指针进行下标：

```cpp
void f(initializer_list<int> lst)
{
    for(int i=0; i<lst.size(); ++i)
        cout << lst[i] << '\n'; // error const int* p = lst.begin();
    for(int i=0; i<lst.size(); ++i)
        cout << p[i] << '\n'; // OK
}
```

自然地，`initializer_list` 也可以被 range `for` 使用。例如：

```cpp
void f2(initializer_list<int> lst) {
    for (auto x : lst)
        cout << x << '\n'; }
```

## 30.3.2 Rangefor 支持

rangefor 语句被映射为使用迭代器的 for 语句，如 §9.5.1 中所述。在 `<iterator>` 中，标准库为内置数组以及提供成员 `begin()` 和 `end()` 的每种类型提供了 `std::begin()` 和 `std::end()` 函数；参见 §33.3。所有标准库容器（例如，`vector` 和 `unordered_map`）以及字符串都支持使用 rangefor 进行迭代；容器适配器（如 `stack` 和 `priority_queue`）不支持。容器头文件，例如 `<vector>`，包含 `<initializer_list>`，因此用户很少需要直接包含它。

# 30.4 错误处理

标准库是在近 40 年的时间内开发的组件。因此，它们的风格和错误处理方法并不一致：

+   - C 风格库由函数组成，其中许多函数通过设置 `errno` 来指示发生了错误；参见 §13.1.2 和 §40.3。
+   - 许多在元素序列上操作的算法返回指向最后一个元素之后迭代器的迭代器以指示“未找到”或“失败”；参见 §33.1.1。
+   - I/O 流库依赖于每个流中的状态来反映错误，并且可能会（如果用户请求）抛出异常来指示错误；参见 §38.3。
+   - 一些标准库组件，例如 `vector`、`string` 和 `bitset`，会抛出异常来指示错误。

标准库的设计使得所有设施都遵守“基本保证” (§13.2)；也就是说，即使抛出异常，也不会泄漏资源（如内存），也不会破坏标准库类的不变量。

## 30.4.1 异常

一些标准库设施通过抛出异常来报告错误：标准库异常（继续）

| Component | Exception |
|---|---|
| bitset | Throws invalid_argument, out_of_range, overflow_error |
| iostream | Throws |

ios_base::failure if exceptions are enabled
regex Throws regex_error
string Throws length_error, out_of_range
vector Throws out_of_range

### 第 30.4.1 节 异常 869
标准库异常（续）

| Facility | Exception thrown |
|---|---|
| `new T` | Throws `bad_alloc` if it cannot allocate memory for a `T` |
| `dynamic_cast<T>(r)` | Throws `bad_cast` if it cannot convert the reference `r` to a `T` |
| `thread` | Throws `system_error` |
| `call_once()` | Throws `system_error` |
| `mutex` | Throws `system_error` |
| `condition_variable` | Throws `system_error` |
| `async()` | Throws `system_error` |
| `packaged_task` | Throws `future_error` |
| `future` and `promise` | Throws `future_error` |

这些异常可能出现在直接或间接使用这些设施的任何代码中。此外，任何操作可能抛出异常的对象都必须假定会抛出（该）异常，除非已采取措施避免。 例如，`packaged_task` 如果它被要求执行的函数抛出异常，就会抛出异常。

除非你知道没有任何设施以可能抛出异常的方式使用，否则最好始终在某处捕获标准库异常层次结构的根类之一（如 `exception`）以及任何异常（`...`） (§13.5.2.3)，例如在 `main()` 中。

#### 30.4.1.1 标准 `exception` 层次结构

不要抛出内置类型，如 `int` 和 C 风格字符串。相反，抛出专门定义为用作异常的对象。
这个标准异常类的层次结构提供了一种异常分类：

+   - `exception`
+     - `logic_error`
+     - `runtime_error`
+       - `length_error`
+       - `domain_error`
+       - `out_of_range`
+       - `invalid_argument`
+     - `future_error`
+     - `bad_exception`
+     - `bad_cast`
+     - `bad_alloc`
+     - `bad_typeid`
+     - `range_error`


overflow_error underflow_error system_error
bad_array_new_length ios_base::failure

该层次结构试图为标准库所定义的异常之外的情况提供一个框架。逻辑错误（logic error）原则上可以在程序开始执行之前，或通过测试函数和构造函数的参数来捕获。运行时错误（run-time error）则是所有其他错误。system_error 在 §30.4.3.3 中描述。
标准库异常层次结构的根是 `exception` 类：

```cpp
class exception {

public:

exception();

exception(const exception&);

exception& operator=(const exception&);

virtual ~exception();

virtual const char* what() const;

};
```

what() 函数可用于获取一个字符串，该字符串旨在指示导致异常的某种错误信息。程序员可以通过从标准库异常类派生来定义自己的异常，如下所示：

```cpp
struct My_error : runtime_error {

My_error(int x) :runtime_error{"My_error"}, interesting_value{x} { }

int interesting_value;

};
```

并非所有异常都属于标准库异常层次结构。但标准库抛出的所有异常都来自该异常层次结构。

除非你确信没有设施会被以可能抛出异常的方式使用，否则最好在某个地方捕获所有异常。例如：

```cpp
int main()

try {

// ...

}

catch (My_error& me) { // a My_error happened

// we can use me.interesting_value and me.what() }

catch (runtime_error& re) { // a runtime_error happened

// we can use re.what()

}

catch (exception& e) { // some standard-library exception happened

// we can use e.what()

}

catch (...) { // Some unmentioned exception happened

// we can do local cleanup

}
```

与函数参数类似，我们使用引用来避免切片问题（§17.5.1.4）。

### 30.4.1.2 异常传播

在 `<exception>` 中，标准库提供了使异常传播对程序员可用的设施：

第30.4.1.2节 异常传播 871

### 异常传播（§iso.18.8.5）

`exception_ptr` 用于指向异常的一种未指定类型

`ep=current_exception() ep` 是一个指向当前异常的 `exception_ptr`；如果当前没有活动异常，则指向无异常；noexcept

`rethrow_exception(ep)` 重新抛出 `ep` 所指向的异常；`ep` 包含的指针不得为 `nullptr`；noreturn（§12.1.7）

`ep=make_exception_ptr(e) ep` 是指向异常 `e` 的 `exception_ptr`；noexcept

一个 `exception_ptr` 可以指向任何异常，而不仅仅是 `exception` 层次结构中的异常。可以把 `exception_ptr` 看作一个智能指针（类似 `shared_ptr`），只要 `exception_ptr` 指向某个异常，它就会让该异常保持存活。这样，我们就可以将指向某个异常的 `exception_pointer` 从捕获该异常的函数中传出，并在其他地方重新抛出。特别是，`exception_ptr` 可用于实现异常在不同于捕获线程的另一个线程中被重新抛出。这正是 `promise` 和 `future`（§42.4）所依赖的。对 `exception_ptr` 使用 `rethrow_exception()`（从不同线程）不会引入数据竞争。

`make_exception_ptr()` 可以实现为：

```cpp
template<typename E>

exception_ptr make_exception_ptr(E e) noexcept;

try {

throw e;

}

catch(...) {

return current_exception();

}
```

`nested_exception` 是一个类，用于存储从调用 `current_exception()` 获得的 `exception_ptr`：

### nested_exception（§iso.18.8.6）

`nested_exception ne {};` 默认构造函数：`ne` 持有一个指向 `current_exception()` 的 `exception_ptr`；noexcept

`nested_exception ne {ne2};` 拷贝构造函数：`ne` 和 `ne2` 都持有指向存储异常的一个 `exception_ptr`

`ne2=ne` 拷贝赋值：`ne` 和 `ne2` 都持有指向存储异常的一个 `exception_ptr`

`ne.~nested_exception()`

析构函数；虚函数  
重新抛出 `ne` 存储的异常；  
如果 `ne` 中没有存储异常，则调用 `terminate()`；noreturn

`ep = ne.nested_ptr()`  
`throw_with_nested(e)`  
`ep` 是指向 `ne` 存储异常的 `exception_ptr`；noexcept。抛出一个派生自 `nested_exception` 和 `e` 类型的异常；`e` 不得派生自 `nested_exception`；noreturn

`rethrow_if_nested(e) dynamic_cast<const nested_exception&>(e).rethrow_nested();`  
`e` 的类型必须派生自 `nested_exception`。`nested_exception` 的预期用途是作为某个类的基类，该类的异常处理程序用来传递一些关于错误局部上下文的信息，同时携带一个指向导致该处理程序被调用的异常的 `exception_ptr`。例如：

```cpp

struct My_error : runtime_error {

  My_error(const string&);

  // ...

};

void my_code() {

  try {

    // ...

  }

  catch (...) {

    My_error err {"something went wrong in my_code()"};

    // ...

    throw_with_nested(err);

  }

}

```

现在，`My_error` 的信息连同持有指向所捕获异常的 `exception_ptr` 的 `nested_exception` 一起被传递（重新抛出）。  
在调用链的更上层，我们可能想查看嵌套异常：

```cpp

void user()

{

  try { my_code();

  }

  catch(My_error& err) {

    // ... clear up My_error problems ...

    try { rethrow_if_nested(err); // re-throw the nested exception, if any

    }

    catch (Some_error& err2) {

```

```

// ... clear up Some_error problems ...

}

}

}

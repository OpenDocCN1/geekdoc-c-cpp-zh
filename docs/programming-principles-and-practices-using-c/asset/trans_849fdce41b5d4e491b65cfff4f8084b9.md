

当我们需要恰好两个元素且不关心定义具体类型时，我们会使用 **pair**（对组）。如果需要零个或多个元素，我们可以使用来自 `<tuple>` 的 **tuple**（元组）：

```cpp
template <typename... Types>
struct tuple {
    explicit constexpr tuple(const Types& ...);    // construct from N values
    template<typename... Atypes>
    explicit constexpr tuple(const Atypes&& ...); // construct from N values
    // . . . copy and move operations . . .
};

template <class... Types>
constexpr tuple<Types...> make_tuple(Types&&...);      // construct tuple
                                                        // from N values
```

**tuple** 的实现使用了一种超出本书范围的特性，即可变参数模板。那些省略号（. . .）指的就是这个特性。然而，我们可以像使用 **pairs**（对组）一样大量使用 **tuples**（元组）。例如：

```cpp
auto t0 = make_tuple();              // no elements
auto t1 = make_tuple(123.456);       // one element of type double
auto t2 = make_tuple(123.456, 'a');  // two elements of types double and char
auto t3 = make_tuple(12,'a',string{"How?"});  // three elements of types int,
                                               // char, and string
```

**tuple** 可以包含许多元素，因此我们不能仅仅使用 **first** 和 **second** 来访问它们。相反，使用一个函数 **get**：

```cpp
auto d = get<0>(t1);   // the double
auto n = get<0>(t3);    // the int
auto c = get<1>(t3);    // the char
auto s = get<2>(t3);    // the string
```

**get** 的下标是作为模板参数提供的。正如示例所示，**tuple** 的下标从 0 开始。

元组主要用于通用编程。

## B.6.4 initializer_list

在 `<initializer_list>` 中，我们找到了 **initializer_list**（初始化列表）的定义：

```cpp
template<typename T>
class initializer_list {
public:
    initializer_list() noexcept;

    size_t size() const noexcept;  // number of elements
    const T* begin() const noexcept; // first element
    const T* end() const noexcept;  // one-past-last element

    // ...
};
```

当编译器看到一个包含 `X` 类型元素的 `{}` 初始化列表时，该列表被用来构造一个 `initializer_list<X>`（§14.2.1, §18.2）。不幸的是，`initializer_list` 不支持下标运算符（`[]`）。

## B.6.5 资源管理指针

内置指针并不表示它是否代表其所指向对象的所有权。这可能会使编程变得非常复杂（§19.5）。资源管理指针 `unique_ptr` 和 `shared_ptr` 在 `<memory>` 中定义，用于解决这个问题：

-   `unique_ptr`（§19.5.4）表示独占所有权；一个对象只能有一个 `unique_ptr`，当该 `unique_ptr` 被销毁时，对象也会被删除。
-   `shared_ptr` 表示共享所有权；一个对象可以有多个 `shared_ptr`，当最后一个 `shared_ptr` 被销毁时，对象也会被删除。

### unique_ptr<p>（简化版）

| 操作 | 描述 |
| :--- | :--- |
| `unique_ptr up {};` | 默认构造函数：`up` 持有 `nullptr`。 |
| `unique_ptr up (p);` | `up` 持有 `p`。 |
| `unique_ptr up (up2);` | 移动构造函数：`up` 持有 `up2` 的 `p`；`up2` 持有 `nullptr`。 |
| `up.~unique_ptr()` | 删除 `up` 持有的指针。 |
| `p=up.get()` | `p` 是 `up` 持有的指针。 |
| `p=up.release()` | `p` 是 `up` 持有的指针；`up` 持有 `nullptr`。 |
| `up.reset(p)` | 删除 `up` 持有的指针；`up` 持有 `p`。 |
| `up=make_unique<X>(args)` | `up` 持有 `new<X>(args)`（C++14）。 |

通常的指针操作，如 `*`、`->`、`==` 和 `<`，可以用于 **unique_ptrs**。此外，可以定义 **unique_ptr** 使用不同于普通 **delete** 的删除动作。

### shared_ptr<p>（简化版）

| 操作 | 描述 |
| :--- | :--- |
| **shared_ptr sp {};** | 默认构造函数：**sp** 持有 **nullptr**。 |
| **shared_ptr sp (p);** | **sp** 持有 **p**。 |
| **shared_ptr sp (sp2);** | 拷贝构造函数：**sp** 和 **sp2** 都持有 **sp2 的 p**。 |
| **shared_ptr sp (move(sp2));** | 移动构造函数：**sp** 持有 **sp2 的 p**；**sp2** 持有 **nullptr**。 |
| **sp.~shared_ptr()** | 如果 **sp** 是该指针的最后一个 **shared_ptr**，则删除 **sp** 持有的指针。 |
| **sp = sp2** | 拷贝赋值：如果 **sp** 是引用其指针的最后一个共享指针，则删除该指针；**sp** 和 **sp2** 都持有 **sp2 的 p**。 |
| **sp = move(sp2)** | 移动赋值：如果 **sp** 是引用其指针的最后一个共享指针，则删除该指针；**sp** 持有 **sp2 的 p**；**sp2** 持有 **nullptr**。 |
| **p=sp.get()** | **p** 是 **sp** 持有的指针。 |
| **n=sp.use_count()** | 有多少 **shared_ptrs** 引用 **sp** 持有的指针？ |
| **sp.reset(p)** | 如果 **sp** 是引用其指针的最后一个共享指针，则删除该指针；**sp** 持有 **p**。 |
| **sp=make_shared<X>(args)** | **sp** 持有 **new<X>(args)**。 |

通常的指针操作，如 `*`、`->`、`==` 和 `<`，可以用于 **shared_ptrs**。此外，可以定义 **shared_ptr** 使用不同于普通 **delete** 的删除动作。

还有一种 **weak_ptr** 用于打破 **shared_ptrs** 的循环引用。

# B.7 输入/输出流

I/O 流库提供文本和数值的格式化和非格式化的缓冲输入/输出。I/O 流设施的定义位于 `<iostream>`、`<ostream>` 等头文件中；参见 §B.1.1。

**ostream** 将带类型的对象转换为字符（字节）流：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_1201_0.png)

**istream** 将字符（字节）流转换为带类型的对象：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_1201_1.png)

**iostream** 是一种可以既作为 **istream** 又作为 **ostream** 的流。图中的缓冲区是“流缓冲区”（**streambufs**）。如果你需要定义从 **iostream** 到新类型设备、文件或内存的映射，请在专家级教科书中查找它们。

有三个标准流：

**标准 I/O 流**

| 流 | 描述 |
| :--- | :--- |
| **cout** | 标准字符输出（通常默认是屏幕） |
| **cin** | 标准字符输入（通常默认是键盘） |
| **cerr** | 标准字符错误输出（无缓冲） |

## B.7.1 I/O 流层次结构

**istream** 可以连接到输入设备（例如，键盘）、文件或 **string**。类似地，**ostream** 可以连接到输出设备（例如，文本窗口）、文件或 **string**。I/O 流设施组织在一个类层次结构中：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_1202_0.png)

可以通过构造函数或 **open()** 调用来打开流：

**流类型**

| 类型 | 描述 |
| :--- | :--- |
| `stringstream(m)` | 创建一个具有模式 **m** 的空字符串流。 |
| `stringstream(s,m)` | 创建一个包含 **字符串 s** 且模式为 **m** 的字符串流。 |
| `fstream()` | 创建一个稍后打开的文件流。 |
| `fstream(s,m)` | 以模式 **m** 打开名为 **s** 的文件，并创建一个指向该文件的文件流。 |
| `fs.open(s,m)` | 以模式 **m** 打开名为 **s** 的文件，并让 **fs** 引用该文件。 |
| `fs.is_open()` | **fs** 是否已打开？ |

对于文件流，文件名是一个 C 风格字符串。你可以以几种模式之一打开文件：

**流模式**

| 模式 | 描述 |
| :--- | :--- |
| `ios_base::app` | 追加（即，添加到文件末尾） |
| `ios_base::ate` | “位于末尾”（打开并定位到末尾） |
| `ios_base::binary` | 二进制模式——注意系统特定的行为 |
| `ios_base::in` | 用于读取 |
| `ios_base::out` | 用于写入 |
| `ios_base::trunc` | 将文件截断为 0 长度 |

在每种情况下，打开文件的确切效果可能取决于操作系统，如果操作系统无法满足以特定方式打开文件的请求，结果将是一个不处于 **good()** 状态的流。

一个例子：

```cpp
void my_code(ostream& os);    // my code can use any ostream

ostringstream os;              // o for “output”
ofstream of("my_file");
if (!of) error("couldn't open 'my_file' for writing");
my_code(os);                   // use a string
my_code(of);                   // use a file
```

参见 §11.3。

## B.7.2 错误处理

**iostream** 可以处于四种状态之一：

**流状态**

| 状态 | 描述 |
| :--- | :--- |
| **good()** | 操作成功。 |
| **eof()** | 遇到了输入结束（“文件末尾”）。 |
| **fail()** | 发生了意外事件（例如，我们要查找数字但找到了 `'x'`）。 |
| **bad()** | 发生了意外且严重的事件（例如，磁盘读取错误）。 |

通过使用 **s.exceptions()**，程序员可以请求 **iostream** 在从 **good()** 变为其他状态时抛出异常（参见 §10.6）。

在不处于 **good()** 状态的流上尝试的任何操作都没有效果；它是一个“无操作”（no op）。

**iostream** 可以作为条件使用。在这种情况下，如果 **iostream** 的状态是 **good()**，则条件为真（成功）。这是读取值流的常见惯用做法的基础：

```cpp
for (X buf; cin>>buf; ) {  // buf is an “input buffer” for holding one value of type X
  // ... do something with buf, ...
}
// we get here when >> couldn't read another X from cin
```


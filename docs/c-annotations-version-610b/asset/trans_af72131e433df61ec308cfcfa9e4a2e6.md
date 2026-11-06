
在这种说法中，**C++** 引用应被视为*左值引用*（使用记法 `typename &`）。它们可以与*右值引用*（使用记法 `typename &&`）相对照。

理解右值引用的关键在于*匿名变量*。匿名变量没有名称，这正是编译器在有选择时自动将其与左值引用关联起来的区分特征。在介绍一些 C++11 之前没有的有趣新构造之前，让我们先看看左值引用的一些有区分性的应用。以下函数返回一个临时（匿名）值：

```cpp
int intVal()
{
    return 5;
}
```

尽管 `intVal` 的返回值可以赋给一个 `int` 变量，但这需要一次复制操作；当函数不返回 `int` 而是返回某个大型对象时，这种复制可能变得代价过高。*引用*或*指针*也不能用来接收匿名返回值，因为该返回值不会存活到那之后。因此下面的写法是非法的（如编译器所指出的）：

```cpp
int &ir = intVal();        // fails: refers to a temporary
int const &ic = intVal();  // OK: immutable temporary
int *ip = &intVal();       // fails: no lvalue available
```

显然，无法修改 `intVal` 返回的临时值。但现在考虑下一个函数：

```cpp
void receive(int &value)
{
    cout << "int value parameter\n";
}
void receive(int &&value)
{
    cout << "int R-value parameter\n";
}
```

并从 main 中调用此函数：

```cpp
int main()
{
    receive(18);
    int value = 5;
    receive(value);
    receive(intVal());
}
```

该程序产生以下输出：

```text
int R-value parameter
int value parameter
int R-value parameter
```

它表明，在接收匿名 int 作为参数的所有情况下，编译器都会选择 `receive(int &&value)`。注意这包括 `receive(18)`：值 18 没有名称，因此调用 `receive(int &&value)`。在内部，它实际上使用一个临时变量来存储 18，如下面修改 `receive` 的示例所示：

```cpp
void receive(int &&value)
{
    ++value;
    cout << "int R-value parameter, now: " << value << '\n';
        // displays 19 and 6, respectively.
}
```

将 `receive(int &value)` 与 `receive(int &&value)` 进行对比，与 `int &value` 不是 const 引用无关。如果使用 `receive(int const &value)`，会得到相同的结果。总之：如果向函数传递匿名值，编译器会选择使用右值引用的重载函数。

不过，如果将 `void receive(int &value)` 替换为 `void receive(int value)`，编译器就会遇到问题。当面临值参数和引用参数（左值或右值）之间的选择时，它无法作出决定，并报告歧义。在实际场景中这不是问题。右值引用被加入语言，正是为了能够区分两种形式的引用：具名值（使用左值引用）和匿名值（使用右值引用）。

正是这种区分使得*移动语义*和*完美转发*的实现成为可能。此时还无法充分讨论*移动语义*的概念（但更深入的讨论见第 9.7 节），不过完全可以说明其基本思想。

考虑这样的情况：一个函数返回一个 `struct Data`，其中包含指向动态分配字符的指针。此外，该结构体定义了一个成员函数 `copy(Data const &other)`，它接受另一个 `Data` 对象并将另一个对象的数据复制到当前对象中。`struct Data` 的（部分）定义可能如下所示<sup>a</sup>：

```cpp
struct Data
{
    char *text;
    size_t size;
    void copy(Data const &other)
    {
        text = strdup(other.text);
        size = strlen(text);
    }
};
```

<sup>a</sup>致细心的读者：在本例中，使用 `Data::copy()` 导致的内存泄漏应被忽略

接下来，函数 `dataFactory` 和 `main` 定义如下：

```cpp
Data dataFactory(char const *txt)
{
    Data ret = {strdup(txt), strlen(txt)};
    return ret;
}

int main()
{
    Data d1 = {strdup("hello"), strlen("hello")};

    Data d2;
    d2.copy(d1);                       // 1 (see text)

    Data d3;
    d3.copy(dataFactory("hello"));     // 2
}
```

在 (1) 处，`d2` 适当地接收了 `d1` 文本的一份副本。但在 (2) 处，`d3` 接收的是 `dataFactory` 函数返回的临时对象中所存文本的一份副本。由于该临时对象在调用 `copy()` 之后不再存在，会观察到两个相关且令人不快的结果：

- 返回值是一个临时对象：它存在的唯一理由就是将其数据传递给 `d3`。现在 `d3` 复制了临时对象的数据，这显然有些多余。
- 临时 `Data` 对象在调用 `copy()` 之后丢失了。不幸的是，其动态分配的数据也随之丢失，导致内存泄漏。

在这类情况下，应使用*右值引用*。通过用一个成员 `copy(Data &&other)` 重载 `copy` 成员，编译器能够区分情况 (1) 和 (2)。现在它在情况 (1) 中调用最初的 `copy()` 成员，在情况 (2) 中调用新定义的重载 `copy()` 成员：

```cpp
struct Data
{
    char *text;
    size_t size;
    void copy(Data const &other)
    {
        text = strdup(other.text);
    }
    void copy(Data &&other)
    {
        text = other.text;
        other.text = 0;
    }
};
```

注意，重载的 `copy()` 函数只是将 `other.text` 指针移动到当前对象的 `text` 指针，然后将 `0` 重新赋给 `other.text`。`struct Data` 突然变成了*移动感知*的，并实现了*移动语义*，从而消除了前面所示方法的缺点：

- 不再进行深拷贝（情况 (1) 中需要深拷贝），而是简单地将指针值移动到其新所有者；
- 由于 `other.text` 不再指向动态分配的内存，内存泄漏得以避免。

用于 `*this` 的*右值引用*以及通过右值初始化类对象，尚未得到 `g++` 编译器的支持。

## 3.3. C 的更多扩展

### 3.3.3 强类型枚举（C++11）

在 `C++` 中，枚举值实际上是 `int` 值，从而绕过了类型安全。例如，不同枚举类型的值可以比较是否（不）相等，尽管要通过 `(static)` 类型转换。

当前 `enum` 类型的另一个问题在于，其值并不局限于 `enum` 类型名本身，而是局限于定义该枚举的作用域。因此，同一作用域中的两个枚举不能具有相同的值。

在 `C++11` 标准中，这些问题通过定义*枚举类*得到解决。*枚举类*可以如下例所示定义：

```cpp
enum class SafeEnum
{
    NOT_OK,      // 0, by implication
    OK        = 10,
    MAYBE_OK   // 11, by implication
};
```

枚举类默认使用 int 值，但使用 : type 记法可以轻松更改所用的值类型，如下所示：

```cpp
enum class CharEnum: unsigned char
{
    NOT_OK,
    OK
};
```

要使用枚举类中定义的值，还必须提供其枚举名。例如，OK 未定义，而 CharEnum::OK 已定义。

使用数据类型说明（注意其默认为 int），就可以使用枚举类的前向声明。例如：

```cpp
enum Enum1;                 // Illegal: no size available
enum Enum2: unsigned int;  // Legal in C++11: explicitly declared type

enum class Enum3;          // Legal in C++11: default int type is used
enum class Enum4: char;    // Legal in C++11: explicitly declared type
```

### 3.3.4 初始化列表（C++11）

C 语言将初始化列表定义为用花括号括起来的值列表，这些值本身可能又包含初始化列表。在 C 中，这些初始化列表通常用于初始化数组和结构体。

C++ 在 C++11 标准中扩展了这一概念，引入了类型 `initializer_list<Type>`，其中 `Type` 由初始化列表中所用值的类型名替换。C++ 中的初始化列表与 C 中的对应物一样是递归的，因此也可以用于多维数组、结构体和类。

与 C 中一样，初始化列表由用花括号括起来的值列表组成。但与 C 不同的是，函数可以定义初始化列表参数。例如：

```cpp
void values(std::initializer_list<int> iniValues)
{
}
```

像 values 这样的函数可以如下调用：

```cpp
values({2, 3, 5, 7, 11, 13});
```

初始化列表作为一个参数出现，该参数是用花括号括起来的值列表。由于初始化列表的递归性质，也可以传递二维的值序列，如下例所示：

```cpp
void values2(std::initializer_list<int> iniValues)
{
}
```

```cpp
values2({{1, 2}, {2, 3}, {3, 5}, {4, 7}, {5, 11}, {6, 13}});
```

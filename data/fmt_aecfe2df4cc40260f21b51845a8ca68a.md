
```cpp
copy(source.begin(), source.end(), inserter(destination, destination.begin()));
```

插入适配器要求存在两种类型：

- `using value_type = Data`，其中 `Data` 是提供 `push_back`、`push_front` 或 `insert` 成员的类所存储的数据（例如：`using value_type = std::string`）；
- `using const_reference = const &value_type`

专注于 `back_inserter`，该迭代器期望一个支持 `push_back` 成员的容器。插入器的 `operator()` 调用容器的 `push_back` 成员。任何支持 `push_back` 成员的类对象都可以作为参数传递给 `back_inserter`，只要其接口提供了：

```cpp
using const_reference = DataType const &
```

示例：

```cpp
#include <iostream>
#include <algorithm>
#include <iterator>
using namespace std;

class Insertable
{
    public:
        using value_type = int;
        using const_reference = int const &;

        void push_back(int const &)
    };

int main()
{
    int arr[] = {1};
    Insertable insertable;

    copy(arr, arr + 1, back_inserter(insertable));
}
```

## 18.2.3. iostream 对象的迭代器

`istream_iterator<Type>` 可用于为 `istream` 对象定义一组迭代器。`istream_iterator` 的通用形式为：

```cpp
istream_iterator<Type> identifier(istream &in);
```

## 18.2. 迭代器 (ITERATORS)

这里，`Type` 是从 `istream` 流读取的数据元素的类型。它被用作迭代器中的“起始”（begin）。`Type` 可以是任何与 `istream` 对象结合定义了 `operator>>` 的类型。

默认构造函数用作结束迭代器（end-iterator），对应于流的结束。例如：

```cpp
istream_iterator<string> endOfStream;
```

在定义起始迭代器时指定的流对象在默认构造函数未被提及。

使用 `back_inserter` 和 `istream_iterator` 适配器，可以轻松地将流中的所有字符串存储在容器中。示例（使用匿名 `istream_iterator` 适配器）：

```cpp
#include <iostream>
#include <iterator>
#include <string>
#include <vector>
#include <algorithm>

int main()
{
    vector<string> vs;

    copy(istream_iterator<string>(cin), istream_iterator<string>(),
         back_inserter(vs));

    for (
        vector<string>::const begin = vs.begin(), end = vs.end();
        begin != end; ++begin
    ) 
        cout << +begin << ' ' << '\n';
}
```

### 18.2.3.1 'istambuf' 对象的迭代器

输入迭代器也适用于 `streambuf` 对象。

为了从支持输入操作的 `streambuf` 对象读取内容，可以使用 `istambuf_iterators`，它支持与 `istream_iterator` 相同的操作。与后者迭代器类型不同，`istambuf_iterator` 有三个构造函数：

- `istream_iterator<Type>`:

  使用默认 `istambuf_iterator` 构造函数创建迭代器范围的结束迭代器。它代表了从 `streambuf` 提取 `Type` 类型值时的流结束条件。

- `istambuf_iterator<Type>(streambuf *)`:

  在定义 `istream_iterator` 时，可以使用一个指向 `streambuf` 的指针。它代表迭代器范围的起始。

- `istreambuf_iterator<Type>{istream`:

  在定义 `istreambuf_iterator` 时也可以使用 `istream`。它访问 `istream` 的 `streambuf`，并且报告迭代器范围的起始迭代器。

在第 18.2.4 节中提供了一个同时使用 `istambuf_iterators` 和 `ostreambuf_iterators` 的示例。

### 18.2.4 'ostream' 对象的迭代器

可以使用 `ostream_iterator<Type>` 适配器将 `ostream` 传递给期望输出迭代器（OutputIterator）的算法。定义 `ostream_iterators` 有两种构造可用：

```cpp
ostream_iterator<Type> identifier(ostream &outStream);
ostream_iterator<Type> identifier(ostream &outStream, char const *delim);
```

`Type` 是应该插入到 `istream` 中的数据元素的类型。在定义 `ostream` 迭代器时，它可以是任何定义了 `operator<` 的类型。后一个构造函数可以使用分隔符字符串分隔 `Type` 元素。第一个构造不使用任何删除器。

示例展示了如何使用 `istream_iterators` 和 `ostream_iterator` 将信息从一个文件复制到另一个。一个微妙之处在于，你可能想使用 `in.unset(ios::skips)`。它被用于清除 `ios::skip` 标志。结果是运算符直接返回空白字符，文件按字符进行复制。这里是该程序：

```cpp
#include <iostream>
#include <algorithm>
#include <iterator>
using namespace std;

int main()
{
   cin.unset(ios::skips);
   copy(istream_iterator<char>(cin), istream_iterator<char>(),
        ostream_iterator<char>(cout));
   }
```

### 18.2.4.1 'ostream' 对象的迭代器

输出迭代器也适用于 `streambuf` 对象。

为了向支持输出操作的 `streambuf` 对象写入内容，可以使用 `ostreambuf_iterators`，它支持与 `istream_iterator` 相同的操作。`ostreambuf_iterators` 有两个构造函数：

- `ostreambuf_iterator<Type>(streambuf *)`:

  指向 `streambuf` 的指针可以在定义 `istream_iterator` 时使用。它代表迭代器范围的起始。

- `istreambuf_iterator<Type>{ostream`:

  在定义 `istreambuf_iterator` 时也可以使用 `ostream`。它访问 `ostream` 的 `streambuf`，并且报告迭代器范围的起始迭代器。

在第 18.2.4 节中提供了一个同时使用 `istreambuf_iterators` 和 `ostreambuf_iterators` 的示例。

*(注：原文此处存在大量文本重复和逻辑混乱，翻译已根据上下文进行了对齐处理)*

```cpp
#include <iostream>
#include <algorithm>
#include <iterator>
using namespace std;

int main()
{
   cin.unset(ios::skips);
   copy(istream_iterator<char>(cin), istream_iterator<char>(),
        ostream_iterator<char>(cout));
   }
```

- 在第 18.2.4 节中提供了一个同时使用 `istreambuf_iterators` 和 `ostreambuf_iterators` 的示例。

*(注：原文此处存在大量文本重复和逻辑混乱，翻译已根据上下文进行了对齐处理)*

### 18.3 'unique_ptr' 类

在类本节介绍的 `unique_ptr` 类之前，必须包含 `<memory>` 头文件。

当使用指针访问动态分配内存时，需要严格的内存管理以防止内存泄漏。当引用动态内存的指针超出作用域时，动态内存将变得不可访问，程序会导致内存泄漏。程序员必须确保在指针变量超出作用域之前，将动态内存返回内存池。当指针变量指向动态分配的值或对象时，将指针变量定义为 `std::unique_ptr` 对象，内存管理将大大简化。

`unique_ptr` 是伪装指针。由于它们是对象，在超出作用域时会调用析构函数。它们会自动删除所指向的动态内存。`unique_ptr`（以及类似的 `shared_ptr`，见第 18.4 节）被称为智能指针。

`unique_ptr` 有几个特殊特性：

- 当将 `unique_ptr` 赋值给另一个时，使用的是移动语义。如果内存不可，编译将失败。相反，如果编译成功，则使用的容器或通用算法将使用 `unique_ptr`。这里有一个示例：

```cpp
std::unique_ptr<int> up1(new int);
std::unique_ptr<int> up2(up1); // 编译错误
```

第二个定义编译失败，因为 `unique_ptr` 的拷贝构造函数是私有的（赋值运算符也是如此）。但 `unique_ptr` 具有从右值引用初始化和赋值的机制：

```cpp
class unique_ptr
// 接口部分显示
{
```

## 18.3. 'UNIQUE_PTR' 类

```cpp
public:
    unique_ptr(unique_ptr &&tmp); // 右值绑定到此处
private:
    unique_ptr(const unique_ptr &other);
};
```

在下一个示例中，使用了移动语义，并且它可以正确编译：

```cpp
unique_ptr<int> cp(unique_ptr<int>(new int));
```

- `unique_ptr` 对象应该指向动态分配的内存，因为只有动态分配的内存才能被删除。

- 不允许多个 `unique_ptr` 对象指向同一块分配的内存。`unique_ptr` 的接口设计就是为了防止这种情况的发生。一旦 `unique_ptr` 对象离开作用域，它将删除它所指向的内存，立即将任何其他指向该分配内存的对象变为变为野指针（wild pointer）。

- 当类 `Derived` 派自 `Base` 时，新分配的 `Derived` 对象可以赋值给 `unique_ptr<Base>`，而无需为 `Base` 定义虚析构函数。`unique_ptr` 对象返回的 `Base` 指针可以简单地静态转换为 `Derived`，此时 `Derived` 的析构函数也会被调用，`unique_ptr` 的定义还提供了一个删除函数（deleter）。这在下面的示例所示：

```cpp
class Base {
};
class Derived : public Base
{
    public:
        // 假设 Derived 有一个成员 void process()
        static void deleter(Base *bp);
};
void Derived::deleter(Base *bp)
{
    delete static_cast<Derived *>(bp);
}
int main() {
    unique_ptr<Base, void (*)(Base*)> bp(new Derived, &Derived::deleter);
        static_cast<Derived *>(bp.get())->process(); // OK!
}
// // 这里调用了 -Derived：没有多态
```

`unique_ptr` 类提供了几个成员函数来访问指针本身，或者让 `unique_ptr` 指向另一块内存。这些成员函数（`unique_ptr` 构造函数）将在后续章节中介绍。

`unique_ptr` 也可以与容器和（泛型）算法一起。它们可以正确地析构任何类型的对象，因为它们的构造函数接受可自定义的删除器。此外，数组也可以由 `unique_ptr` 处理。

### 18.3.1 定义 'unique_ptr' 对象

有三种定义 `unique_ptr` 对象的方法。每种定义都包含尖括号之间常用的 `<type>` 标识符：

- 默认构造函数创建一个不指向特定内存块的 `unique_ptr` 对象。它的指针被初始化为 0（零）；

```cpp
unique_ptr<type> identifier;
```

这种形式将在第 18.3.2 节中讨论。

- 移动构造函数初始化一个 `unique_ptr` 对象。在使用移动构造函数后，其 `unique_ptr` 参数不再指向动态分配的内存，其指针数据被变为空指针；

```cpp
unique_ptr<type> identifier(another unique_ptr for type);
```

这种形式将在第 18.3.3 节中讨论。

- 最常用的形式将 `unique_ptr` 对象初始化为传递给对象构造函数的动态分配内存块。可以选择提供删除器。可以将接收 `unique_ptr` 指针作为参数的（自由）函数或函数对象传递给删除器。它被返回到动态内存的公共池（如果指针等于零，则什么都不做）。

```cpp
unique_ptr<type> identifier(new-expression [, deleter]);
```

这种形式将在第 18.3.4 节中讨论。

### 18.3.2 创建普通的 'unique_ptr'

`unique_ptr` 的默认构造函数定义了一个不指向特定内存块的 `unique_ptr`。

```cpp
unique_ptr<type> identifier;
```

由 `unique_ptr` 对象控制的指针被初始化为 0（零）。虽然 `unique_ptr` 对象本身不是指针，但它的值可以与 0 进行比较。例如：

```cpp
unique_ptr<int> ip;

if (!ip)
    cout << "0-pointer with a unique_ptr object\n";
```

或者，可以使用成员函数 `get`（参见第 18.3.5 节）。

### 18.3.3 移动另一个 'unique_ptr'

`unique_ptr` 可以使用该类型的 `unique_ptr` 对象的右值引用进行初始化：

```cpp
unique_ptr<type> identifier(other unique_ptr object);
```

使用了移动构造函数，例如在下面的示例中：

```cpp
void mover(unique_ptr<string> &&param)
{
    unique_ptr<string> tmp(move(param));
}
```

## 18.3. 'UNIQUE_PTR' 类

类似地，也可以使用赋值运算符。`unique_ptr` 对象可以被赋值给相同类型的临时 `unique_ptr` 对象（再次使用了移动语义）。例如：

```cpp
#include <iostream>
#include <memory>
#include <string>

using namespace std;

int main() {
    unique_ptr<string> hello1( new string("Hello world") );
    unique_ptr<string> hello2( move(hello1) );
    unique_ptr<string> hello3;

    hello3 = move(hello2);
    cout << //hello1 << '\n' << 将导致段错误
         << hello2 << '\n' << 相同
         << hello3 << '\n';
}
// 显示: 
Hello world
```

### 18.3.4 指向对象的 'unique_ptr'

`unique_ptr` 的默认构造函数定义了一个不指向特定内存块的 `unique_ptr`。

```cpp
unique_ptr<type> identifier;
```

由 `unique_ptr` 对象控制的指针被初始化为 0（零）。虽然 `unique_ptr` 对象本身不是指针，但它的值可以与 0 进行比较。例如：

```cpp
unique_ptr<int> ip;

if (!ip)
    cout << "0-pointer with a unique_ptr object\n";
```

或者，可以使用成员函数 `get`（参见第 18.3.5 节）。

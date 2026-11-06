

代价非常小。实际工作由二元赋值运算符执行，如前所述。然而，该运算符是从具有如下原型的移动感知二元运算符调用的

```cpp
Binary operator+(Binary &&lhs, Binary const &rhs);
```

传统二元运算符的实现现在只包含两个步骤：

- 使用类的拷贝构造函数创建左侧操作数的副本；
- 调用移动感知二元运算符，将匿名副本作为其左侧操作数传入，并将其结果作为二元运算符的结果返回。

以下是类 `Binary` 针对 `operator+` 的传统二元赋值运算符和移动感知二元赋值运算符的声明与实现：

```cpp
class Binary
{
    public:
        Binary();
        Binary(int value);
        Binary(Binary &&tmp) = default;           // or roll your own

        Binary &operator+=(Binary const &other);   // see the text
};

Binary operator+(Binary const &lhs, Binary const &rhs)
{
    Binary tmp(lhs);
    return operator+(std::move(tmp), rhs);
}

Binary operator+(Binary &&lhs, Binary const &rhs)
{
    return lhs += rhs;
}
```

## 11.7 重载‘operator new(size_t)’

当 `operator new` 被重载时，它必须定义 `void *` 返回类型，并且其第一个参数必须是 `size_t` 类型。默认的 `operator new` 通常有一个参数，但重载版本可以定义多个参数。第一个参数没有显式指定，而是根据为其重载 `operator new` 的类的对象大小推导出来。本节讨论重载 `operator new`。重载 `new[]` 将在 11.9 节讨论。

可以定义多个版本的 `operator new`，只要每个版本定义自己独有的参数集即可。当重载的 `operator new` 成员必须动态分配内存时，它们可以使用全局 `operator new`，并应用作用域解析运算符 `::`。在下一个示例中，类 `String` 的重载 `operator new` 将动态分配的 `String` 对象的底层存储初始化为 0 字节：

```cpp
#include <cstddef>
#include <iosfwd>

class String
{
    std::string *d_data;

    public:
        void *operator new(size_t size)
        {
            return memset(::operator new(size), 0, size);
        }
        bool empty() const
        {
            return d_data == 0;
        }
};
```

上面的 `operator new` 用于以下程序，说明即使 `String` 的默认构造函数什么都不做，对象的数据也会被初始化为零：

```cpp
#include "string.h"
#include <iostream>
using namespace std;

int main()
{
    String *sp = new String;

    cout << boolalpha << sp->empty() << '\n';   // shows: true
}
```

在 `new String` 处发生了以下事情：

- 首先，调用 `String::operator new`，分配并初始化一个大小为 `String` 对象的内存块。
- 接着，指向该内存块的指针被传递给（默认的）`String` 构造函数。由于没有定义构造函数，构造函数本身什么也没做。

由于 `String::operator new` 将分配的内存初始化为零字节，因此分配的 `String` 对象的 `d_data` 成员在它开始存在时就已经被初始化为空指针。

到目前为止我们遇到的所有成员函数（包括构造函数和析构函数）都定义了一个（隐藏的）指针，指向它们应操作的对象。这个隐藏指针成为函数的 `this` 指针。

在下一个*伪 C++ 代码*示例中，显式展示了该指针，以说明使用 `operator new` 时发生了什么。第一部分直接定义一个 `String` 对象 `str`，示例的第二部分使用（重载的）`operator new`：

```cpp
String::String(String *const this);        // real prototype of the default
                                             // constructor

String *sp = new String;                     // This statement is implemented
                                             // as follows:

    String *sp = reinterpret_cast<String *>(
                    String::operator new(sizeof(String))
                 );
    String::String(sp);                       // initialization
```

在上面的片段中，成员函数被当作类 `String` 的*无对象*成员函数处理。这样的成员称为*静态成员函数*（参见第 8 章）。实际上，`operator new` 就是这样的静态成员函数。由于它没有 `this` 指针，因此无法访问它应为其提供内存的对象的数据成员。它只能分配并初始化所分配的内存，但不能按名称访问对象的数据成员，因为此时尚未定义数据对象布局。

分配之后，内存被（作为 `this` 指针）传递给构造函数以进行进一步处理。

`operator new` 可以有多个参数。第一个参数作为隐式参数初始化，并且始终是 `size_t` 参数。额外的重载运算符可以定义额外参数。一个有趣的额外 `operator new` 是*placement new*运算符。使用 placement new 运算符时，一块内存已经预留好，并使用类的一个构造函数来初始化该内存。重载 placement new 需要一个具有两个参数的 `operator new`：`size_t` 和 `char *`，指向已经可用的内存。`size_t` 参数被隐式初始化，但其余参数必须使用 `operator new` 的实参显式初始化。于是我们得到熟悉的 placement new 运算符使用语法形式：

```cpp
char buffer[sizeof(String)];        // predefined memory
String *sp = new(buffer) String;     // placement new call
```

在我们的类 `String` 中，placement new 运算符的声明如下：

```cpp
void *operator new(size_t size, char *memory);
```

它可以像这样实现（同时将 `String` 的内存初始化为 0 字节）：

```cpp
void *String::operator new(size_t size, char *memory)
{
    return memset(memory, 0, size);
}
```

也可以定义任何其他重载版本的 `operator new`。下面是一个示例，展示了一个重载 `operator new` 的使用和定义，它将对象地址立即存储到现有的指向 `String` 对象的指针数组中（假设该数组足够大）：

```cpp
// use:
String *next(String **pointers, size_t *idx)
{
    return new(pointers, (*idx)++) String;
}

// implementation:
void *String::operator new(size_t size, String **pointers, size_t idx)
{
    return pointers[idx] = ::operator new(size);
}
```

## 11.8 重载‘operator delete(void *)’

delete 运算符也可以被重载。事实上，每当 `operator new` 被重载时，重载 `operator delete` 都是良好的实践。

`operator delete` 必须定义一个 `void *` 参数。定义第二个 `size_t` 类型参数的第二个重载版本与重载 `operator new[]` 有关，将在 11.9 节讨论。

重载的 `operator delete` 成员返回 `void`。

“自制”的 `operator delete` 会在执行关联类的析构函数之后，删除动态分配的对象时被调用。因此，语句

```cpp
delete ptr;
```

中 `ptr` 是指向类 `String` 对象的指针，而该类重载了 `operator delete`，该语句是以下语句的简写：

```cpp
ptr->~String(); // call the class's destructor

          // and do things with the memory pointed to by ptr
String::operator delete(ptr);
```

重载的 `operator delete` 可以对 `ptr` 所指向的内存做任何它想做的事情。例如，它可以简单地删除它。如果这是首选做法，那么可以使用 `::` 作用域解析运算符调用默认的 delete 运算符。例如：

```cpp
void String::operator delete(void *ptr)
{
    // any operation considered necessary, then, maybe:
    ::delete ptr;
}
```

要声明上述重载的 `operator delete`，只需将以下行添加到类的接口中：

```cpp
void operator delete(void *ptr);
```

与 `operator new` 一样，`operator delete` 是静态成员函数（另见第 8 章）。

## 11.9 运算符‘new[]’和‘delete[]’

在 9.1.1、9.1.2 和 9.2.1 节中介绍了 `operator new[]` 和 `operator delete[]`。与 `operator new` 和 `operator delete` 一样，运算符 `new[]` 和 `delete[]` 也可以被重载。

由于既可以重载 `new[]` 和 `delete[]`，也可以重载 `operator new` 和 `operator delete`，因此在选择适当的运算符集合时应小心。应始终应用以下经验法则：

> 如果使用 `new` 分配内存，则应使用 `delete` 释放内存。如果使用 `new[]` 分配内存，则应使用 `delete[]` 释放内存。

默认情况下，这些运算符的行为如下：

- `operator new` 用于分配单个对象或原始值。对于对象，会调用对象的构造函数。
- `operator delete` 用于归还由 `operator new` 分配的内存。同样，对于类类型对象，会调用类的析构函数。
- `operator new[]` 用于分配一系列原始值或对象。如果分配一系列对象，则会调用类的默认构造函数来逐个初始化每个对象。


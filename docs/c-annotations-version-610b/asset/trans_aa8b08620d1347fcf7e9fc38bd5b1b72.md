
```cpp
std::string const &at(size_t idx) const;
size_t size() const;
};
```

构造函数的任务是初始化对象的数据成员。例如，其构造函数定义如下：

```cpp
Strings::Strings()
:
    d_string(0),
    d_size(0)
{}

Strings::Strings(char const *const *cStrings, size_t size)
:
    d_string(new string[size]),
    d_size(size)
{
    for (size_t idx = 0; idx != size; ++idx)
        d_string[idx] = cStrings[idx];
}
```

由于 `Strings` 类的对象会分配内存，显然需要一个析构函数。析构函数可能会也可能不会自动调用。规则如下：

- 析构函数*只*会为完全构造的对象调用。C++ 认为，一旦至少有一个构造函数正常完成，对象就完全构造了。过去要求的是构造函数（完成），但由于 C++11 支持构造函数委托，单个对象可以激活多个构造函数；因此说“至少一个构造函数”。其余规则只适用于完全构造的对象；
- 局部非静态对象的析构函数在执行流离开定义它们的块时自动调用；在函数外层块某处定义的对象，其析构函数在函数终止前调用。
- 静态或全局对象的析构函数在程序本身终止时调用。
- 动态分配的对象的析构函数由 `delete` 调用，使用对象地址作为操作数；
- 动态分配的对象数组的析构函数由 `delete[]` 调用，使用数组首元素地址作为操作数；
- 由定位 `new` 初始化的对象，其析构函数通过显式调用该对象的析构函数来激活。

析构函数的任务是确保所有由对象自身动态分配并仅由该对象控制的内存都被归还。因此，`Strings` 析构函数的任务将是删除 `d_string` 所指向的内存。其实现为：

```cpp
Strings::~Strings()
{
    delete[] d_string;
}
```

下一个示例展示了 `Strings` 的工作方式。在 process 中，创建了一个 `Strings` 存储，并显示其数据。它向 `main` 返回一个动态分配的 `Strings` 对象。一个 `Strings *` 接收所分配对象的地址，并再次删除该对象。随后又创建了另一个 `Strings` 对象，位于一个

### 9.2. 析构函数

```cpp
#include "strings.h"
using namespace std;

Strings::~Strings()
{
    cout << "Strings destructor called" << '\n';
}

int main()
{
    Strings *a = new Strings[2];

    cout << "Destruction with []'s" << '\n';
    delete[] a;

    a = new Strings[2];

    cout << "Destruction without []'s" << '\n';
    delete a;
}
/*
    Generated output:
Destruction with []'s
Strings destructor called
Strings destructor called
Destruction without []'s
Strings destructor called
*/
```

从生成的输出中我们可以看到，当使用 `delete[]` 时，各个 *Strings* 对象的析构函数都会被调用；而如果省略 `[]`，则只会调用第一个对象的析构函数。

相反，如果在应当调用 `delete` 的情况下调用了 `delete[]`，结果不可预测，程序很可能会崩溃。这种有问题的行为源于运行时系统存储已分配数组大小信息的方式（通常就在数组首元素*之前*）。如果只分配了单个对象，则数组特定信息不可用，但 `delete[]` 仍然假定它存在。因此，后一个运算符会在数组首元素之前的存储位置遇到虚假值。然后它会尽职地将在那里遇到的值解释为大小信息，通常导致程序失败。

如果没有定义析构函数，编译器会定义一个*平凡析构函数*。这个平凡析构函数确保组合对象的析构函数（以及如果类是派生类时的*基类*析构函数，参见第 13 章）被调用。这有严重的影响：分配内存的对象会造成内存泄漏，除非采取预防措施（通过定义合适的析构函数）。考虑以下程序：

```cpp
#include <iostream>
#include "strings.h"
using namespace std;

Strings::~Strings()
{
    cout << "Strings destructor called" << '\n';
}

int main()
{
    Strings **ptr = new Strings* [2];
    ptr[0] = new Strings[2];
    ptr[1] = new Strings[2];

    delete[] ptr;
}
```

这个程序完全不产生输出。为什么？变量 `ptr` 被定义为指向指针的指针。因此，动态分配的数组由指针变量组成，而指针属于基本类型。基本类型变量没有析构函数。因此只归还数组本身，不会调用任何 `Strings` 析构函数。

当然，我们不希望这样，而是要求 `ptr` 元素所指向的 `Strings` 对象也被删除。在这种情况下，我们有两个选项：

- 在 for 语句中访问 `ptr` 数组的所有元素，为数组的每个元素调用 `delete`。这一过程已在上一节演示。
- 围绕一个指针（例如指向某个类的对象，如 `Strings`）设计一个包装类。不是使用指向 `Strings` 对象指针的指针，而是使用指向包装类对象数组的指针。结果，`delete[] ptr` 会调用每个包装类对象的析构函数，进而为其 `d_strings` 成员调用 `Strings` 析构函数。示例：

```cpp
#include <iostream>
using namespace std;

class Strings    // partially implemented
{
    public:
        ~Strings();
};

inline Strings::~Strings()
{
    cout << "destructor called\n";
}

class Wrapper
{
    Strings *d_strings;

    public:
        Wrapper();
        ~Wrapper();
};

inline Wrapper::Wrapper()
:
    d_strings(new Strings())
{
}
inline Wrapper::~Wrapper()
{
    delete d_strings;
}

int main()
{
    delete[] new Strings *[4];  // memory leak: no destructor called
    cout << "================\n";
    delete[] new Wrapper[4];     // OK: 4 x destructor called
}
```

理论部分到此为止。在某些系统上，“内存不足”条件实际上可能永远不会达到，因为操作系统可能会在运行时支持系统有机会停止程序之前进行干预（另见此链接²）。

分配内存的标准 C 函数（如 strdup、malloc、realloc 等）在内存分配失败时不会触发 new 处理程序，在 C++ 程序中应避免使用。

### 9.3 赋值运算符

在 C++ 中，结构体和类类型对象可以像在 C 中那样直接赋予新值。对于非类类型数据成员，这种赋值的默认动作是从一个数据成员到另一个数据成员的直接逐字节复制。现在我们将使用以下简单的 `Person` 类：

```cpp
class Person
{
    char *d_name;
    char *d_address;
    char *d_phone;

public:
    Person();
    Person(char const *name, char const *addr, char const *phone);
    ~Person();
private:
    char *strdupnew(char const *src);   // returns a copy of src.
};

// strdupnew is easily implemented, here is its inline implementation:
inline char *Person::strdupnew(char const *src)
{
    return strcpy(new char [strlen(src) + 1], src);
}
```

`Person` 的数据成员被初始化为零，或初始化为传递给 `Person` 构造函数的 ASCII-Z 字符串的副本，使用 `strdup` 的某种变体。分配的内存最终由 `Person` 的析构函数归还。

现在考虑在以下示例中使用 `Person` 对象的后果：

```cpp
void tmpPerson(Person const &person)
{
    Person tmp;
    tmp = person;
}
```

以下是调用 `tmpPerson` 时发生的情况：

- 它期望一个 `Person` 的引用作为其参数 `person`。
- 它定义一个局部对象 `tmp`，其数据成员被初始化为零。
- `person` 所引用的对象被复制到 `tmp`：从 `person` 到 `tmp` 复制 `sizeof(Person)` 个字节。

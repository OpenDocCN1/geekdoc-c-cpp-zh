

```cpp
unique_ptr<type [, deleter_type]> identifier(new-expression
             [, deleter = deleter_type()]);
```

第二个（模板）参数（`deleter_type`）是可选的，可以指向一个自由函数或函数对象，由它负责销毁已分配的内存。例如，在分配了双重指针，并且销毁过程必须遍历每个嵌套指针以销毁已分配内存的情况下，会使用 deleter（见下文示例）。

下面是一个初始化指向字符串对象的 `unique_ptr` 的示例：

```cpp
unique_ptr<string> strPtr(new string("Hello world"));
```

传递给构造函数的参数是由 `operator new` 返回的指针。注意，`type` 中并未提及指针。`unique_ptr` 构造中使用的类型与 `new` 表达式中使用的类型相同。

下面是一个示例，展示如何使用显式定义的 deleter 删除动态分配的字符串指针数组：

```cpp
#include <iostream>
#include <string>
#include <memory>
using namespace std;

struct Deleter
{
    size_t d_size;
    Deleter(size_t size = 0)
      :
        d_size(size)
    {}
    void operator()(string **ptr) const
    {
        for (size_t idx = 0; idx < d_size; ++idx)
            delete ptr[idx];
        delete[] ptr;
    }
};
int main()
{
    unique_ptr<string *, Deleter> sp2(new string *[10], Deleter(10));

    Deleter &obj = sp2.get_deleter();
}
```

可以使用 `unique_ptr` 访问 `new` 表达式所分配对象可用的成员函数。可以像 `unique_ptr` 是指向动态分配对象的普通指针一样访问这些成员。例如，在下面的程序中，文本 ‘C++’ 被插入到单词 ‘hello’ 之后：

```cpp
#include <iostream>
#include <memory>
#include <cstring>
using namespace std;

int main()
{
    unique_ptr<string> sp(new string("Hello world"));
    cout << *sp << '\n';
    sp->insert(strlen("Hello "), "C++ ");
    cout << *sp << '\n';
}
/*
  Displays:
    Hello world
    Hello C++ world
*/
```

## 18.3.5 运算符和成员（C++11）

类 `unique_ptr` 提供以下运算符：

- `unique_ptr<Type> &operator=(unique_ptr<Type> &&tmp);`

    此运算符使用*移动语义*将右值 `unique_ptr` 对象所指向的内存转移给左值 `unique_ptr` 对象。因此，右值对象失去其指向的内存，并变成 0 指针。通过先使用 `std::move` 将其转换为右值引用，可以将现有的 `unique_ptr` 赋值给另一个 `unique_ptr`。示例：

    ```cpp
    unique_ptr<int> ip1(new int);
    unique_ptr<int> ip2;

    ip2 = std::move(ip1);
    ```

- `operator bool() const;`

    如果 `unique_ptr` 不指向内存（即其 `get` 成员，见下文，返回 0），则此运算符返回 false。否则返回 true。

- `Type &operator*();`

    此运算符返回对可通过 `unique_ptr` 对象访问的信息的引用。它像普通的指针解引用运算符一样工作。

- `Type *operator->();`

    此运算符返回指向可通过 `unique_ptr` 对象访问的信息的指针。此运算符允许你选择可通过 `unique_ptr` 对象访问的对象的成员。示例：

    ```cpp
    unique_ptr<string> sp(new string("hello"));
    cout << sp->c_str();
    ```

类 `unique_ptr` 支持以下成员函数：

- `Type *get();`

    返回指向由 `unique_ptr` 对象控制的信息的指针。它像 `operator->` 一样工作。可以检查返回的指针。如果它为零，则 `unique_ptr` 对象不指向任何内存。

- `Deleter &unique_ptr<Type>::get_deleter();`

    返回对 `unique_ptr` 所使用的 deleter 对象的引用。

- `Type *release();`

    返回指向可通过 `unique_ptr` 对象访问的信息的指针。同时，对象本身变成 0 指针（即其指针数据成员被转为 0 指针）。此成员可用于将可通过 `unique_ptr` 对象访问的信息转移给普通的 `Type` 指针。调用此成员后，动态分配内存的正确销毁由程序员负责。

- `void reset(Type *);`

    由 `unique_ptr` 对象控制的动态分配内存被归还到公共池；此后该对象控制传递给函数的参数所指向的内存。也可以不带参数调用，将对象变成 0 指针。此成员函数可用于将新分配的一块动态内存分配给 `unique_ptr` 对象。

- `void swap(unique_ptr<Type> &);`

    两个相同类型的 `unique_ptr` 被交换。

## 18.3.6 将 'unique_ptr' 对象用于数组（C++11）

当使用 `unique_ptr` 存储数组时，解引用运算符意义不大，但对于数组，`unique_ptr` 对象受益于索引运算符。单个对象 `unique_ptr` 与指向动态分配对象数组的 `unique_ptr` 之间的区别通过模板特化实现。

对于动态分配的数组，以下语法可用：

- 索引（`[]`）表示法用于指定智能指针控制一个动态分配的*数组*。示例：

    ```cpp
    unique_ptr<int[]> intArr(new int[3]);
    ```

- 索引运算符可用于访问数组的元素。示例：

    ```cpp
    intArr[2] = intArr[0];
    ```

在这些情况下，智能指针的析构函数调用 `delete[]` 而不是 `delete`。

## 18.3.7 遗留类 'auto_ptr'（已弃用）

（现已被 C++11 标准弃用的）智能指针类 `std::auto_ptr<Type>` 传统上由 C++ 提供。此类不支持移动语义，但当将一个 `auto_ptr` 对象赋值给另一个时，右侧对象会失去其信息。

类 `unique_ptr` 没有 `auto_ptr` 的缺点，因此现在使用 `auto_ptr` 已被弃用。`auto_ptr` 存在以下缺点：

- 它们不支持*移动语义*；
- 它们不应用于指向数组；
- 它们不能用作抽象容器的数据类型。

由于其缺点和可用的替代品，`auto_ptr` 类不再被 **C++ Annotations** 涵盖。现有软件应修改为使用智能指针（`unique_ptr` 或 `shared_ptr`），新软件应在适用时直接使用这些新的智能指针类型实现。

## 18.4 类 'shared_ptr'（C++11）

除了 `unique_ptr`，C++11 标准还提供了 `std::shared_ptr<Type>`，它是一种引用计数智能指针。在使用 `shared_ptr` 之前，必须包含 `<memory>` 头文件。

共享指针在其引用计数降为零后自动销毁其内容。

`shared_ptr` 支持复制和移动构造函数，以及标准和移动重载赋值运算符。

与 `unique_ptr` 一样，`shared_ptr` 可以指向动态分配的数组。

### 18.4.1 定义 'shared_ptr' 对象（C++11）

有四种定义 `shared_ptr` 对象的方法。每种定义都包含通常位于尖括号之间的 `<type>` 说明符：

- 默认构造函数简单地创建一个不指向特定内存块的 `shared_ptr` 对象。其指针被初始化为 0（零）：

    ```cpp
    shared_ptr<type> identifier;
    ```

    此形式在 18.4.2 节中讨论。

- 复制构造函数初始化一个 `shared_ptr`，使两个对象共享现有对象所指向的内存。复制构造函数还会递增 `shared_ptr` 的引用计数。示例：

    ```cpp
    shared_ptr<string> org(new string("hi there"));
    shared_ptr<string> copy(org);    // reference count now 2
    ```

- 移动构造函数使用临时 `shared_ptr` 的指针和引用计数初始化一个 `shared_ptr`。临时 `shared_ptr` 被变为 0 指针。现有 `shared_ptr` 的数据可以被移动到新定义的 `shared_ptr` 中（同时将现有 `shared_ptr` 变为 0 指针）。在下一个示例中，构造了一个临时匿名 `shared_ptr` 对象，然后用于构造 `grabber`。由于 `grabber` 的构造函数接收一个匿名临时对象，编译器使用 `shared_ptr` 的移动构造函数：

    ```cpp
    shared_ptr<string> grabber(shared_ptr<string>(new string("hi there")));
    ```

- 最常用的形式将 `shared_ptr` 对象初始化为传递给对象构造函数的动态分配内存块。可选地可以提供 deleter。可以传递一个（自由）函数（或函数对象），它接收 `shared_ptr` 的指针作为参数，作为 deleter。它应当将动态分配的内存归还到公共池（如果指针等于零则什么都不做）。

    ```cpp
    shared_ptr<type> identifier (new-expression [, deleter]);
    ```

    此形式在 18.4.3 节中讨论。

### 18.4.2 创建普通 'shared_ptr'（C++11）

`shared_ptr` 的默认构造函数定义一个不指向特定内存块的 `shared_ptr`：

```cpp
shared_ptr<type> identifier;
```


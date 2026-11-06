
- `operator delete[]` 用于删除先前由 `new[]` 分配的内存。如果先前分配的是对象，那么会为每个单独的对象调用析构函数。不过，当分配的是指向对象的指针时要小心。如果分配的是指向对象的指针，那么这些已分配指针所指向的对象的析构函数不会被自动调用。指针是原始类型，因此当它被归还到公共池时不会采取进一步操作。

### 11.9.1 重载 ‘new[]’

要在类中（例如在 String 类中）重载 `operator new[]`，请在类的接口中添加以下行：

```cpp
void *operator new[](size_t size);
```

该成员的 size 参数是隐式提供的，并由 C++ 运行时系统初始化为必须分配的内存量。与简单的单对象 operator new 一样，它应返回 void *。必须初始化的对象数量可以很容易地通过 size / sizeof(String) 计算出来（当然，在为另一个类重载 operator new[] 时，应将 String 替换为适当的类名）。重载的 new[] 可以使用例如默认的 operator new[] 或默认的 operator new 来分配原始内存：

```cpp
void *operator new[](size_t size)
{
    return ::operator new[](size);
    // alternatively:
    // return ::operator new(size);
}
```

在返回已分配的内存之前，重载的 operator new[] 有机会做一些特殊的事情。例如，它可以将内存初始化为零字节。

一旦定义了重载的 operator new[]，它就会自动用于如下语句：

```cpp
String *sp = new String[12];
```

与 operator new 一样，也可以定义 operator new[] 的其他重载。operator new[] 重载的一个机会是专门为对象数组重载 placement new。该运算符默认可用，但一旦定义了至少一个重载的 operator new[]，它就会变得不可用。实现 placement new 并不困难。下面是一个示例，它在返回之前将可用内存初始化为 0 字节：

```cpp
void *String::operator new[](size_t size, char *memory)
{
    return memset(memory, 0, size);
}
```

要使用这个重载运算符，必须再次提供第二个参数，如下所示：

```cpp
char buffer[12 * sizeof(String)];
String *sp = new(buffer) String[12];
```

### 11.9.2 重载 ‘delete[]’

要在 String 类中重载 `operator delete[]`，请在类的接口中添加以下行：

```cpp
void operator delete[](void *memory);
```

其参数被初始化为先前由 String::new[] 分配的内存块的地址。

实现 operator delete[] 时需要注意一些微妙之处。尽管 new 和 new[] 返回的地址指向已分配的对象，但在 new 和 new[] 返回的地址之前紧邻位置还有一个可用的 size_t 值。这个 size_t 值是已分配块的一部分，包含该块的实际大小。当然，对于 placement new 运算符来说，这并不成立。

当类定义了析构函数时，new[] 返回的地址之前的 size_t 值包含的不是已分配块的大小，而是调用 new[] 时指定的对象数量。通常这无关紧要，但在重载 operator delete[] 时，它可能成为有用的信息。在这些情况下，operator delete[] 接收到的不是 new[] 返回的地址，而是初始 size_t 值的地址。这是否有用并不清楚。到 delete[] 的代码执行时，所有对象都已经被销毁，因此 operator delete[] 只能用于确定销毁了多少个对象，但对象本身已经不能再使用了。

下面是一个示例，展示了最小 Demo 类中 operator delete[] 的这种行为：

```cpp
struct Demo
{
    size_t idx;
    Demo()
    {
        cout << "default cons\n";
    }
    ~Demo()
    {
        cout << "destructor\n";
    }
    void *operator new[](size_t size)
    {
        return ::operator new(size);
    }
    void operator delete[](void *vp)
    {
        cout << "delete[] for: " << vp << '\n';
        ::operator delete[](vp);
    }
};

int main()
{
    Demo *xp;
    cout << ((int *) (xp = new Demo[3]))[-1] << '\n';
    cout << xp << '\n';
    cout << "====================\n";
    delete[] xp;
}
// This program displays (your 0x?????? addresses might differ, but
// the difference between the two should be sizeof(size_t)):
// default cons
// default cons
// default cons
// 3
// 0x8bdd00c
// ====================
// destructor
// destructor
// destructor
// delete[] for: 0x8bdd008
```

为 String 类重载 operator `delete[]` 后，它将在如下语句中自动使用：

```cpp
delete[] new String[5];
```

operator `delete[]` 也可以使用额外的 `size_t` 参数进行重载：

```cpp
void operator delete[](void *p, size_t size);
```

这里 size 会自动初始化为 void *p 所指向的内存块的大小（以字节为单位）。如果定义了这个形式，那么就不应定义 void operator delete[](void *)，以避免歧义。后一种 operator delete[] 形式的示例如下：

```cpp
void String::operator delete[](void *p, size_t size)
{
    cout << "deleting " << size << " bytes\n";
    ::operator delete[](p);
}
```

可以定义 operator `delete[]` 的其他重载，但要使用它们，必须将它们作为静态成员函数显式调用（参见第 8 章）。示例：

```cpp
// declaration:
void operator delete[](void *p, ostream &out);
// usage:
String *xp = new String[3];
String::operator delete[](xp, cout);
```

### 11.9.3 ‘new[]’、‘delete[]’ 与异常

当执行 `new[]` 表达式时抛出异常，会发生什么？在本节中，我们将说明，即使只有部分对象被正确构造，`new[]` 也是异常安全的。

首先，new[] 在尝试分配所需内存时可能抛出异常。在这种情况下，会抛出 `bad_alloc`，而且由于没有分配任何东西，所以不会泄漏。

分配所需内存后，将依次为每个对象使用类的默认构造函数。某个时刻，构造函数可能抛出异常。接下来发生的情况由 C++ 标准定义：调用已构造对象的析构函数，并将为对象本身分配的内存归还到公共池。假设抛出异常的构造函数提供基本保证，因此即使构造函数可能抛出异常，`new[]` 也是异常安全的。

下面的示例说明了这种行为。程序请求分配并初始化五个对象，但在构造两个对象后，构造过程因抛出异常而失败。输出显示，正确构造的对象的析构函数被调用，并且已分配的*底层*内存被正确归还：

```cpp
#include <iostream>
using namespace std;

static size_t count = 0;

class X
{
    int x;
public:
    X()
    {
        if (count == 2)
            throw 1;
        cout << "Object " << ++count << '\n';
    }
    ~X()
    {
        cout << "Destroyed " << this << "\n";
    }
    void *operator new[](size_t size)
    {
        cout << "Allocating objects: " << size << " bytes\n";
        return ::operator new(size);
    }
    void operator delete[](void *mem)
    {
        cout << "Deleting memory at " << mem << ", containing: " <<
            *reinterpret_cast<int *>(mem) << "\n";
        ::operator delete(mem);
    }
};

int main()
try
{
    X *xp = new X[5];
    cout << "Memory at " << xp << '\n';
    delete[] xp;
}
catch (...)
{
    cout << "Caught exception.\n";
}
// Output from this program (your 0x??? addresses might differ)
// Allocating objects: 24 bytes
// Object 1
// Object 2
// Destroyed 0x8428010
// Destroyed 0x842800c
// Deleting memory at 0x8428008, containing: 5
// Caught exception.
```

## 11.10 函数对象

函数对象通过重载*函数调用运算符* `operator()` 创建。通过定义函数调用运算符，对象会伪装成函数，因此称为*函数对象*。函数对象也称为*仿函数*。

在使用*泛型算法*时，函数对象很重要。与函数指针等替代方案相比，更推荐使用函数对象。函数对象在泛型算法语境中很重要，这给我们带来了一个教学上的两难。在《C++ Annotations》的这一部分，如果已经讲过泛型算法就好了，但讨论泛型算法又需要函数对象的知识。这个自举问题以一种众所周知的方式解决：暂时忽略这种依赖关系，现在集中讨论函数对象概念。

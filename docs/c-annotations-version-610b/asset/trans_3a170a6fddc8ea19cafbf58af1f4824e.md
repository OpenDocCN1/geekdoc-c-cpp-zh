
由 `shared_ptr` 对象控制的指针被初始化为 0（零）。尽管 `shared_ptr` 对象本身不是指针，但其值可以与 0 进行比较。示例：

```cpp
shared_ptr<int> ip;

if (!ip)
    cout << "0-pointer with a shared_ptr object\n";
```

或者，可以使用成员 `get`（参见 18.4.4 节）。

## 18.4.3 指向新分配的对象（C++11）

通常情况下，`shared_ptr` 由一个动态分配的内存块初始化。其一般形式为：

```cpp
shared_ptr<type> identifier(new-expression [ , deleter]);
```

第二个参数（`deleter`）是可选的，指的是负责销毁已分配内存的函数对象或自由函数。删除器（deleter）用于例如分配了双重指针且销毁时必须访问每个嵌套指针以销毁已分配内存的情况（参见下文示例）。它用于与 `unique_ptr` 所遇到的情况类似的情形（参见 18.3.4 节）。

下面是一个初始化指向 `string` 对象的 `shared_ptr` 的示例：

```cpp
shared_ptr<string> strPtr(new string("Hello world"));
```

传递给构造函数的参数是 `operator new` 返回的指针。注意，`type` 并*不*涉及指针。`shared_ptr` 构造中使用的类型与 new 表达式中使用的类型相同。

下一个示例说明两个 `shared_ptr` 确实共享它们所管理的信息。在修改其中一个对象所管理的信息后，另一个对象所管理的信息也会被修改：

```cpp
#include <iostream>
#include <memory>
#include <string>
using namespace std;

int main()
{
    shared_ptr<string> sp(new string("Hello world"));
    shared_ptr<string> sp2(sp);

    sp->insert(strlen("Hello "), "C++ ");
    cout << *sp << '\n' <<
            *sp2 << '\n';
}
/*
    Displays:
        Hello C++ world
        Hello C++ world
*/
```

## 18.4.4 运算符和成员（C++11）

`shared_ptr` 类提供以下运算符：

- `shared_ptr & operator=(shared_ptr<Type> const & other);`
  
  复制赋值：运算符左侧操作数的引用计数减少。如果引用计数降为零，则删除左侧操作数所控制的动态分配内存。然后，它共享运算符右侧操作数所管理的信息，并使该信息的引用计数递增。

- `shared_ptr & operator=(shared_ptr<Type> && tmp);`
  
  移动赋值：运算符左侧操作数的引用计数减少。如果引用计数降为零，则删除左侧操作数所控制的动态分配内存。然后，它接管运算符右侧操作数所控制的信息，而右侧操作数会变成一个 0 指针。

- `operator bool() const;`
  
  如果 `shared_ptr` 确实指向内存，则返回 true，否则返回 false。

- `Type & operator*();`
  
  返回对存储在 `shared_ptr` 对象中的信息的引用。其行为类似于普通指针。

- `Type * operator->();`
  
  返回指向 `shared_ptr` 对象所控制信息的指针。示例：
  
  ```cpp
  shared_ptr<string> sp(new string("hello"));
  cout << sp->c_str() << '\n';
  ```

支持以下成员函数：

- `Type * get();`
  
  返回指向 `shared_ptr` 对象所控制信息的指针。其行为类似于 `operator->`。可以对返回的指针进行检查。如果它为零，则 `shared_ptr` 对象不指向任何内存。

- `Deleter & get_deleter();`
  
  返回对 `shared_ptr` 的删除器（函数或函数对象）的引用。

- `void reset(Type * p);`
  
  `shared_ptr` 对象所控制信息的引用计数减少，如果降为零，则删除其指向的内存。此后，对象的信息将指向传递给函数的参数，并将其共享计数设为 1。也可以不带参数调用，使对象变为 0 指针。这个成员函数可用于将一个新的动态分配内存块赋给 `shared_ptr` 对象。

- `void shared_ptr<Type>::swap(shared_ptr<Type> &&);`
  
  交换两个类型相同的 `shared_ptr`。

- `bool unique() const;`
  
  如果当前对象是唯一引用该对象所控制内存的对象，则返回 true，否则（包括对象为 0 指针的情况）返回 false。

- `size_t use_count() const;`
  
  返回共享该对象所控制内存的对象数量。

## 18.4.6 对数组使用 `shared_ptr` 对象（C++11）

与 `unique_ptr` 类不同，`shared_ptr` 类没有专门化来处理动态分配的对象数组。

但与 `unique_ptr` 类似，当 `shared_ptr` 指向数组时，解引用运算符意义不大，而在这类情况下 `shared_ptr` 对象可以受益于下标运算符。

创建一个提供这些功能的 `shared_array` 类并不困难。类模板 `shared_array` 继承自 `shared_ptr`，只需提供一个合适的 `deleter` 来确保数组及其元素被正确销毁。此外，它还应定义下标运算符，并可选择使用 `= delete` 来声明解引用运算符。

下面是一个示例，展示如何定义和使用 `shared_array`：

```cpp
struct X
{
    ~X()
    {
        cout << "destr\n";  // show the object's destruction
    }
};
template <typename Type>
class shared_array: public shared_ptr<Type>
{
    struct Deleter             // Deleter receives the pointer
    {                          // and calls delete[]
        void operator()(Type* ptr)
        {
            delete[] ptr;
        }
    };
public:
    shared_array(Type *p)                 // other constructors
    :                                      // not shown here
        shared_ptr<Type>(p, Deleter())
    {}
    Type &operator[](size_t idx)    // index operators
    {
        return shared_ptr<Type>::get()[idx];
    }
    Type const &operator[](size_t idx) const
    {
        return shared_ptr<Type>::get()[idx];
    }
    Type &operator*() = delete;     // delete pointless members
    Type const &operator*() const = delete;
    Type *operator->() = delete;
    Type const *operator->() const = delete;
};
int main()
{
    shared_array<X> sp(new X[3]);
    sp[0] = sp[1];
}
```

## 18.5 具有指针数据成员的类（C++11）

具有指针数据成员的类需要特别关注。尤其是在构造期间，必须小心防止野指针和/或内存泄漏。考虑以下定义了两个指针数据成员的类：

```cpp
class Filter
{
        istream *d_in;
        ostream *d_out;
    public:
        Filter(char const *in, char const *out);
};
```

假设 `Filter` 对象过滤从 *d_in 读取的信息，并将过滤后的信息写入 *d_out。使用指向流的指针可以让我们将它们指向任何类型的流，如 istream、ifstream、fstream 或 istringstream。所示的构造函数可以实现如下：

```cpp
Filter::Filter(char const *in, char const *out)
:
        d_in(new ifstream(in)),
        d_out(new ofstream(out))
{
        if (!*d_in || !*d_out)
                throw string("Input and/or output stream not available");
}
```

当然，构造可能会失败。`new` 可能抛出异常；流构造函数可能抛出异常；或者流无法打开，此时会从构造函数体内抛出异常。使用函数 try 块会有所帮助。注意，如果 `d_in` 的初始化抛出异常，无需担心。`Filter` 对象尚未构造，不会调用其析构函数，处理会继续在捕获抛出的异常处进行。但是，当 `d_out` 的初始化或构造函数中的 `if` 语句抛出异常时，`Filter` 的析构函数同样不会被调用：没有对象，因此不会调用析构函数。这可能会导致内存泄漏，因为不会为 `d_in` 和/或 `d_out` 调用 `delete`。为了防止这种情况，`d_in` 和 `d_out` 必须首先被初始化为 0，之后才能执行（实际的）初始化：

```cpp
Filter::Filter(char const *in, char const *out)
try
:
        d_in(0),
        d_out(0)
{
        d_in = new ifstream(in);
        d_out = new ofstream(out);

        if (!*d_in || !*d_out)
                throw string("Input and/or output stream not available");
}
catch (...)
{
        delete d_out;
        delete d_in;
}
```

但这很快就会变得复杂。如果 `Filter` 还包含另一个类的数据成员，而该类的构造函数需要两个流，那么这个数据成员要么无法构造，要么必须将其自身转换为指针：


如果假设上面使用的 `cout` 不抛出异常，那么至少有 13 次抛出异常的机会：

- `X x`: 载载构造函数可能会抛出异常 (#1)
- `cout << x`: 载载插入运算符可能会抛出异常 (#2)，但其参数可能不是 `X`，例如 `int`，因此 `x:operator int` 可能会被调用，从而提供了另一个抛出异常的机会 (#3)
- `*xp = new X{}`: 构造函数可能会抛出异常 (#4)，或者 `new` 运算符也可能 (#5a)。但你是否注意到，后者的异常可能不是从 `:new` 抛出的，而是来自例如 `X` 自己的重载的 `operator new`？ (#5b)
- `cout << (x + *xp);`
- `delete xp;`

*注：由于原文列表部分格式混乱，上述翻译基于代码逻辑的对齐。*

### 10.10. 异常保证

如果可以假设上面使用的 `cout` 不抛出异常，那么至少有 13 次抛出异常的机会：
- `cout << (x + *xp)`
- `operator+`: 可能是重载的左侧运算符 (#6)、右侧运算符 (#7)，或者两者都可能。
- `operator+` 返回值可以是任何类型，因此 `cout << return-type-of-operator` 可能会抛出异常 (#9)。由于 `operator+` 返回一个临时对象，它在使用后不久就会被销毁。`X` 的析构函数可能会抛出异常 (#10)
- `delete xp`: 只要 `operator delete` 被重载就可能抛出异常 (#11)。而且，`X` 的析构函数可能会抛出异常 (#12)。
- `)`: 当函数终止时 `X` 对象被销毁；可能会抛出异常 (#13)。

强调（并在 10.12 节中进一步讨论）异常可能会导致违反 C++ 标准的析构函数，因此这在良好的 C++ 程序中必须被避免。

当异常在很多情况下产生时，我们如何期望创建出工作的程序？

异常可能在很多情况下产生，但如果我们能够提供至少一种以下异常保证，就能防止严重问题：

- 基础保证：资源不泄露。在实践中意味着：当异常发生时，分配的内存会被正确释放。
- 强保证：如果发生异常，程序的状态保持不变。
- 不抛出异常保证：该函数保证不会抛出异常。

#### 10.10.1 基础保证

基础保证规定资源不泄露。基础保证意味着当异常发生时，分配的内存会被正确释放。这是通过可能抛出异常的函数实现的。

```cpp
void allocator(X xdest) {
    Y *yp = 0;
    try {
        yp = new Y; // 这部分可能会抛异常
    } catch (...) {
        delete yp;
        throw;
    }
    // ...
}
```

#### 10.10.2 强保证

强保证规定在面临异常时，程序的状态不应改变。这是通过对数据的副本执行所有可能抛出异常的操作来实现。

```cpp
Class &operator=(Class const &other)
{
    Class tmp(other); // 构造可能会抛出异常
    swap(tmp);        // swap 不应该抛出异常
    return *this;
}
```

# 第 10 章 异常

```cpp
catch (...)
{
    delete[] tmp;
    throw;
}
```

```cpp
void PersonDb::add(member Person const &next)
{
    Person *tmp = newAppend(next);
    delete[] d_data;
    d_data = tmp;
    ++d_size;
}
```

（私有）成员函数 `newAppend` 的任务是创建已分配的 `Person` 对象的副本，包括下一个 `Person` 对象的数据。`catch` 处理器捕获分配或拷贝过程中可能抛出的任何异常，并释放所有已分配内存，然后在调用者处重新抛出异常。该函数异常将其所有异常传递给调用者。该函数没有修改 `PersonDb` 的数据，因此它满足了异常保证。从 `newAppend` 返回时，成员可能会修改其数据。其现有的数据被返回，其 `d_data` 指针将指向新创建的 `Person` 对象数组。其 `d_size` 会增加。由于这三个步骤都会抛出异常，因此满足了强保证。

第二个经验准则（修改对象数据的成员不应通过值返回原始（包含的）对象）可以使用成员函数 `PersonDb::erase(size_t idx)` 来说明。以下是一个尝试返回原始 `d_data[idx]` 对象的实现：

```cpp
void PersonDb::erase(size_t idx)
{
    if (idx >= d_size)
        throw "Array bounds exceeded";
    Person ret = d_data[idx];
    Person *tmp = copyBut(idx);
    delete[] d_data;
    d_data = tmp;
    --d_size;
    return ret;
}
```

虽然拷贝消除（copy elution）通常会防止在返回 `ret` 时使用拷贝构造函数，但这并不一定发生。此外，拷贝构造函数可能会抛出异常。如果发生这种情况，函数已经不可逆地修改了 `PersonDb` 的数据，导致丢失强保证。

与其通过值返回 `d_data[idx]`，不如在修改 `PersonDb` 的数据之前将其赋值给外部 `Person` 对象：

```cpp
void PersonDb::erase(Person *dest, size_t idx)
{
    if (idx >= d_size)
        throw "Array bounds exceeded";
    *dest = d_data[idx];
    Person *tmp = copyAll(idx);
```

```cpp
delete[] d_data;
d_data = tmp;
--d_size;
```

这种修改是有效的，但它改变了创建成员并返回原始对象的赋值。然而，这两个函数都面临任务过载的问题，因为它们既修改 `PersonDb` 的数据又返回原始对象。在这种情况下，应该记住“一个函数一个职责”的经验准则：函数应该有一个单一且定义良好的职责。

推荐的方法是使用类似 `Person const &(size_t idx) const` 的成员获取 `PersonDb` 对象，并使用类似 `void PersonData::erase(size_t)` 的成员删除对象。

## 10.11 不抛出保证 (nothrow guarantee)

只有当某些函数和操作保证不会抛出异常，才能实现异常安全。这被称为不抛出保证。必须提供不抛出保证的函数示例是 `swap` 函数。考虑经典的重载赋值运算符：

```cpp
Class &operator=(Class &other)
{
  Class tmp(other);
  swap(tmp);
  return *this;
}
```

如果允许 `swap` 抛出异常，它很可能会让当前对象处于部分交换的状态。当 `catch` 处理器获取到抛出的异常时，`tmp` 已经被销毁，因此非常困难（即不可能）恢复对象的原始状态。结果就是丢失了强保证。

`swap` 函数必须提供不抛出保证。它必须设计为使用以下原型（见第 23.8 节）：

```cpp
void Class::swap(Class &other) noexcept;
```

同样，根据 C++ 标准，`operator delete` 和 `operator delete[]` 的析构函数可能抛出异常（如果它们的行为在形式上是未定义的，另见第 10.12 节）。

由于 C 语言没有定义异常概念，标准 C 库隐含提供了不抛出保证。这允许我们在第 9.6 节中使用 `memcpy` 配合 `swap` 函数。

对基本类型的操作提供了不抛出保证。指针可以重新赋值，引用可以返回，而无需担心可能抛出的异常。

## 10.12 函数块 (Function blocks)

异常可能在构造函数内部产生。在这种情况下，异常是由构造函数本身捕获，还是在外部捕获？直观的解决方案是将构造函数嵌套在 `try` 块中，但这并没有解决问题。

下面的示例说明了 `try` 块，其中 `main` 定义了一个 `PersonDb` 类对象。假设 `PersonDb` 的构造函数抛出了异常，我们无法在 `catch` 处理器中访问已分配的资源，因为 `pdb` 对象已经离开了作用范围：

```cpp
int main(int argc, char **argv)
{
    try {
        PersonDb pdb(argc, argv); // 可能抛出异常
        // main() 的其他代码
    }
    catch(...) {
        // 或其他处理器
        // pdb 在这里是不可访问的
    }
}
```

# 第 10 章 异常

```cpp
{
    std::cout << "Throw's exception handled locally by Throw()\n";
    throw;
}
```

```cpp
class Composer {
    Throw d_t;
public:
    Composer() // 注意：try 位于初始化列表之前
      try {
        d_t(5);
      }
      catch (...) {
        std::cout << "Composer() caught exception as well\n";
      }
}
```

```cpp
int main() {
    Composer c;
}
```

当运行此示例时，我们遇到了一个糟糕的意外：程序运行后以一个 `abort`（中止）异常崩溃了。以下是它产生的输出，最后两行是由系统的最终 catch 处理器添加的，它捕获了所有剩余未捕获的异常：

> Throw's exception handled locally by Throw()
Composer() caught exception as well
terminate called after throwing an instance of 'int'
Abort

其原因在 C++ 标准中有所记录：在属于构造函数或析构函数代码块的 catch 处理器末尾，原始异常会被重新抛出。

如果处理器本身抛出了另一个异常，则异常不会被重新抛出，这为构造函数或析构函数提供了用一个异常替换另一个的方法。只有当异常到达构造函数或析构函数代码块的 catch 处理器的末尾时，才会被重新抛出。嵌套 catch 处理器捕获的异常不会被自动重新抛出。

由于构造函数和析构函数会重新抛出其函数 try 块处理器捕获的异常，上述示例中遇到的运行时错误可以通过为 `main` 函数提供它自己的函数 try 块来简单地修复：

```cpp
int main() {
  try {
    Composer c;
  } catch (...) {
  }
}
```

# 10.12 构造函数中的异常

现在程序按计划运行，输出了以下输出：

```
Throw's exception handled locally by Throw()
Composer() caught exception as well
```

最后一点：如果定义 try 块的函数还声明了异常抛出列表（throw list），那么重新抛出的异常的类型必须与 throw 列表中提到的类型匹配。

# 10.12 构造函数中的异常

对象的析构函数仅对完全构造的对象被激活。尽管这听起来像是一句真理，但这里有一个微妙之处。如果对象的构造由于某种原因失败，那么当对象离开范围时，对象的析构函数*不会*被调用。如果构造函数生成的异常没有被构造函数捕获，就会发生这种情况。如果在对象已经分配内存时抛出异常，则内存将不会返回：因为对象的构造没有成功完成，其析构函数不会被调用。

以下示例以原型形式说明了这种情况。`Incomplete` 类的构造函数显示了一条消息并抛出一个异常。

```cpp
class Incomplete
{
public:
    Incomplete()
    {
      cerr << "Allocated some memory\n";
      throw 0;
    }
    ~Incomplete()
    {
      cerr << "Destroying the allocated memory\n";
    }
}
```

接下来，`main()` 在 try 块内部创建了一个 `Incomplete` 对象。任何可能生成的异常随后会被捕获：

```cpp
int main()
{
  try
  {
    cerr << "Creating `Incomplete` object\n";
    Incomplete();
    cerr << "Object constructed\n";
  }
  catch(...)
  {
    cerr << "Caught exception\n";
  }
}
```

# 第 10 章 异常

当运行此程序时，它产生了以下输出：

```
Creating 'Incomplete' object
Allocated some memory
Caught exception
```

因此，如果 `Incomplete` 的构造函数实际上分配了一些内存，会导致内存泄漏。为了防止这种情况发生，有以下对策措施：

- 防止异常离开构造函数。
- 如果构造函数体的一部分可能会生成异常，可以将该部分由 try 块包裹，允许构造函数本身捕获异常。当构造函数能够修复异常原因并完成其作为有效对象的构造时，这种方法是合理的。
- 如果基类构造函数或成员初始化构造函数生成异常，构造函数内部的 try 块将无法捕获该异常。这会导致异常离开构造函数，并且对象不被认为已正确构造。try 块可以包含成员初始化器，且 try 块的复合语句包含构造函数体，如下例所示：

```cpp
class Incomplete2 {
    Composed d_composed;
    public:
        Incomplete2()
        try {
            d_composed(* arguments */)
            {
                // body
            }
        catch (...) {
        }
}
```

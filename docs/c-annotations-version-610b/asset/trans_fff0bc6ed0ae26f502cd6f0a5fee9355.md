
### 4.1.2.2 ‘Koenig 查找’

如果 *Koenig 查找* 被称为“Koenig 原理”，它本可以成为一部新的 Ludlum 小说的标题。然而并非如此。相反，它指的是 C++ 中的一项技术细节。

“Koenig 查找”指的是这样一个事实：如果调用函数时没有指定其命名空间，那么就使用其参数类型的命名空间来确定该函数的命名空间。如果定义参数类型的命名空间中包含这样的函数，那么就使用该函数。这一过程称为“Koenig 查找”。

作为说明，考虑下面的例子。函数 `FBB::fun(FBB::Value v)` 定义在 FBB 命名空间中。可以在不显式提及其命名空间的情况下调用它：

```cpp
#include <iostream>

namespace FBB
{
    enum Value        // defines FBB::Value
    {
        FIRST
    };

    void fun(Value x)
    {
        std::cout << "fun called for " << x << '\n';
    }
}

int main()
{
    fun(FBB::FIRST);    // Koenig lookup: no namespace
                        // for fun() specified
}
/*
    generated output:
fun called for 0
*/
```

编译器在处理命名空间时相当智能。如果 FBB 命名空间中的 `Value` 被定义为 `typedef int Value`，那么 `FBB::Value` 将被识别为 `int`，从而导致 Koenig 查找失败。

作为另一个例子，考虑下面的程序。这里涉及两个命名空间，每个命名空间都定义了自己的 `fun` 函数。不存在歧义，因为参数决定了命名空间，所以会调用 `FBB::fun`：

```cpp
#include <iostream>

namespace FBB
{
    enum Value        // defines FBB::Value
    {
        FIRST
    };

    void fun(Value x)
    {
        std::cout << "FBB::fun() called for " << x << '\n';
    }
}

namespace ES
{
    void fun(FBB::Value x)
    {
        std::cout << "ES::fun() called for " << x << '\n';
    }
}

int main()
{
    fun(FBB::FIRST);      // No ambiguity: argument determines
                          // the namespace
}
/*
    generated output:
FBB::fun() called for 0
*/
```

下面是一个存在歧义的例子：`fun` 有两个参数，分别来自两个命名空间。程序员必须解决这一歧义：

```cpp
#include <iostream>

namespace ES
{
    enum Value          // defines ES::Value
    {
        FIRST
    };
}

namespace FBB
{
    enum Value          // defines FBB::Value
    {
        FIRST
    };

    void fun(Value x, ES::Value y)
    {
        std::cout << "FBB::fun() called\n";
    }
}

namespace ES
{
    void fun(FBB::Value x, Value y)
    {
        std::cout << "ES::fun() called\n";
    }
}

int main()
{
    //  fun(FBB::FIRST, ES::FIRST); ambiguity: resolved by
    //                                explicitly mentioning
    //                                the namespace
}
```

```cpp
ES::fun(FBB::FIRST, ES::FIRST);
}
/*
    generated output:
ES::fun() called
*/
```

命名空间的一个有趣微妙之处在于，一个命名空间中的定义可能会破坏另一个命名空间中定义的代码。这表明命名空间可能相互影响，如果我们没有意识到它们的特性，命名空间也可能适得其反。考虑下面的例子：

```cpp
namespace FBB
{
    struct Value
    {};

    void fun(int x);
    void gun(Value x);
}

namespace ES
{
    void fun(int x)
    {
        fun(x);
    }
    void gun(FBB::Value x)
    {
        gun(x);
    }
}
```

无论如何，程序员最好不要使用任何 `ES::fun` 函数，因为它会导致无限递归。然而，重点不在这里。重点在于，由于编译失败，程序员甚至不会有机会调用 `ES::fun`。

`gun` 的编译失败，但 `fun` 的编译没有失败。为什么会这样？为什么 `ES::fun` 能够顺利编译，而 `ES::gun` 却不能？在 `ES::fun` 中调用了 `fun(x)`。由于 x 的类型没有定义在命名空间中，Koenig 查找不适用，于是 `fun` 会以无限递归调用自身。

对于 `ES::gun`，参数定义在 `FBB` 命名空间中。因此，`FBB::gun` 函数是可能被调用的候选者。但 `ES::gun` 本身也是可能的，因为 `ES::gun` 的原型与调用 `gun(x)` 完全匹配。

现在考虑 `FBB::gun` 尚未声明的情况。那么当然没有歧义。负责 `ES` 命名空间的程序员正高枕无忧。一段时间之后，维护 `FBB` 命名空间的程序员认为，向 `FBB` 命名空间添加一个函数 `gun(Value x)` 可能不错。现在，由于另一个完全不同的命名空间（`FBB`）中的添加，`ES` 命名空间中的代码突然无法编译。命名空间显然并非完全相互独立，因此我们应当注意上述这类微妙之处。在后面的 C++ Annotations（第 11 章）中，我们将回到这个问题。

### 4.1.3 标准命名空间

`std` 命名空间由 **C++** 保留。标准定义了许多属于运行时可用软件的实体（例如 `cout`、`cin`、`cerr`）；在 *标准模板库* 中定义的模板（参见第 18 章）；以及 *泛型算法*（参见第 19 章）都定义在 `std` 命名空间中。

## 4.1  命名空间

关于上一节的讨论，在引用 std 命名空间中的实体时可以使用 using 声明。例如，要使用 `std::cout` 流，代码可以按如下方式声明该对象：

```cpp
#include <iostream>
using std::cout;
```

然而，通常可以不加多想地接受 std 命名空间中定义的所有标识符。因此，人们经常遇到 using 指令，它允许程序员在引用用该 using 指令指定的命名空间中定义的任何实体时省略命名空间前缀。人们经常不指定 using 声明，而是遇到如下 using 指令：

```cpp
#include <iostream>
using namespace std;
```

应该使用 using 指令而不是 using 声明吗？根据经验法则，可以决定坚持使用 using 声明，直到列表变得长得不切实际，此时可以考虑使用 using 指令。

using 指令和声明有两条限制：

- 程序员不应在 std 命名空间内部声明或定义任何内容。这*不*是由编译器强制执行的，而是标准对用户代码提出的要求；
- 不应将 using 声明和指令强加于第三方编写的代码。在实践中，这意味着 using 指令和声明应被禁止出现在头文件中，并且只应在源文件中使用（参见第 7.10.1 节）。

### 4.1.4  嵌套命名空间与命名空间别名

命名空间可以嵌套。下面是一个例子：

```cpp
namespace CppAnnotations
{
    namespace Virtual
    {
        void *pointer;
    }
}
```

变量 pointer 定义在 Virtual 命名空间中，而该命名空间本身嵌套在 CppAnnotations 命名空间下。要引用该变量，有以下选项可用：

- 可以使用 *完全限定名*。实体的完全限定名是直到到达该实体定义为止所遇到的所有命名空间的列表。命名空间和实体通过作用域解析运算符连接在一起：

```cpp
int main()
{
    CppAnnotations::Virtual::pointer = 0;
}
```

- 可以为 CppAnnotations::Virtual 提供 using 声明。现在 Virtual 可以在不带任何前缀的情况下使用，但 pointer 必须使用 Virtual:: 前缀：

```cpp
using CppAnnotations::Virtual;
```

```cpp
int main()
{
    Virtual::pointer = 0;
}
```

- 可以对 `CppAnnotations::Virtual::pointer` 使用 `using` 声明。现在 `pointer` 可以在不带任何前缀的情况下使用：

```cpp
using CppAnnotations::Virtual::pointer;

int main()
{
    pointer = 0;
}
```

- 可以使用一个或多个 `using` 指令：

```cpp
using namespace CppAnnotations::Virtual;

int main()
{
    pointer = 0;
}
```

或者，也可以使用两个单独的 `using` 指令：

```cpp
using namespace CppAnnotations;
using namespace Virtual;

int main()
{
    pointer = 0;
}
```

- 可以组合使用 `using` 声明和 `using` 指令。例如，可以对 `CppAnnotations` 命名空间使用 `using` 指令，并对 `Virtual::pointer` 变量使用 `using` 声明：

```cpp
using namespace CppAnnotations;
using Virtual::pointer;

int main()
{
    pointer = 0;
}
```

对于每个 `using` 指令，该命名空间的所有实体都可以在不带任何进一步前缀的情况下使用。如果某个命名空间是嵌套的，那么该命名空间也可以在不带任何进一步前缀的情况下使用。然而，嵌套命名空间中定义的实体仍然需要该嵌套命名空间的名称。只有在应用了 `using` 声明或指令之后，才能省略嵌套命名空间的限定名。

当更倾向于使用完全限定名，但像

```
CppAnnotations::Virtual::pointer
```

这样的长名称仍然被认为太长时，可以使用 *命名空间别名*：

```cpp
namespace CV = CppAnnotations::Virtual;
```


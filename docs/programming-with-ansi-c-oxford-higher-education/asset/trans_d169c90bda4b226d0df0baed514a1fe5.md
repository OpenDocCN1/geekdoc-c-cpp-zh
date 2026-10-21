

```
class Product
{
    void registration()
    {...}
}

int main()
{
    namespace Product = NewProduct;
    /* The most important line */
    Product::Product MyProduct;
    /* The first is the name of namespace and the second is the class in Product::Product */
    MyProduct.registration();
}
```

请看最重要的一行

```
namespace Product = NewProduct
```

将这一行改为

```
namespace Product = OldProduct
```

程序其余部分就会改用旧版 Product。

这种设计的妙处在于，我们将新旧两个版本产品相关的所有内容分别放在两个不同的命名空间中。尽管如此，我们仍然可以使用相同的代码，包括两个命名空间中都存在的函数（如 `register()`），让它们表现出不同的行为。这样的设计帮助程序员能够重复使用相同的函数名，同时为新版产品增加额外的功能。

例如，假设新版产品的新的 `registration()` 函数需要客户以不同格式提供地址。旧的 `registration` 函数可能仍然存在于 `OldProduct` 命名空间中，而新的、更新的 `registration` 函数将成为 `NewProduct` 命名空间的一部分。因此，用于注册客户的代码仍然保持不变，如下所示：

```
MyProduct.registration();
```

如果 `MyProduct` 是 `NewProduct` 的别名，就会调用新的 `registration` 函数；另一方面，如果 `MyProduct` 是 `OldProduct` 的别名，就会调用旧的 `registration` 函数。

## 14.7 std 命名空间

`std` 是定义标准库例程的命名空间。如果在程序开头编写 `using namespace std`，就可以不加任何限定地使用 `cout` 或 `cin` 等对象。包含 `std` 命名空间会使 `std` 命名空间中封装的所有标准库例程在全局命名空间中可用。

如果程序开头没有编写 `using namespace std`，则可以通过限定符 `std::` 来调用 `std` 中的元素。

新使用的头文件，如 `<iostream>` 和 `<cstdlib>`（替代 `<iostream.h>` 和 `<stdio.h>`），使用的是 `std` 命名空间。旧式设计直接将 `.h` 头文件的内容插入全局命名空间，不使用 `std` 命名空间；因此，它无法解决名称冲突问题。相反，程序员可以通过避免使用 using 指令，轻松地避免将整个 `std` 命名空间添加到全局命名空间中。为了避免冲突，可以使用 using 声明或完全限定名。这在旧式设计中是不可能的。在新版本中，库元素可以通过 using 声明进行区分。因此，如果程序员自己定义了类 `abs`，并且没有编写 `using <cmath>`，他们可以调用 `cmath::abs()` 来调用库中的绝对值函数，并调用 `OurLib::abs()` 来访问他们库中的 `abs()`。

我们前面也看到，命名空间是可以扩展的。然而，`std` 命名空间是一个例外。不能向 `std` 命名空间添加新的定义。

## 14.8 KOENIG 查找

如果一开始编写了 `using std::cout`，然后使用 `cout` 配合 `<<`，程序可以正常工作。我们在本章前面已经看到了这一点。运算符 `<<` 是 `std` 命名空间的一部分。即使没有指定定义它的命名空间，编译器如何找到并限定该运算符呢？这要归功于 Andrew Koenig 提出的一种算法，该算法现已被大多数编译器实现。所有符合 ANSI C++ 的编译器都必须实现该算法。该算法的正式名称是“依赖实参查找”（argument-dependent lookup）。任何符合 ANSI/ISO 标准的编译器都会自动应用 Koenig 查找；因此，无需启用或禁用任何东西。

Koenig 查找使编译器能够搜索命名空间以定位某个元素，即使没有使用 using 指令，甚至没有使用完全限定名。请看以下程序。

```
//KoenigLookup.cpp
#include <iostream>
// 这里缺少 using namespace std

int main()
{
    using std::cout;
    // 下面一行现在被注释掉了 // using std::operator <<;
    cout << "Hi";
    return 0;
}
```

程序仍然照常工作。运算符 `<<` 将由 Koenig 查找算法从 `std` 命名空间中找到。

## 14.9 命名空间的开销

命名空间不会引入任何运行时开销。

命名空间在编译时解析。所有 using 指令、using 声明、完全限定名等都由编译器静态处理。运行时无需做任何事情。简而言之，命名空间没有运行时开销。

因此，建议在必要时使用命名空间，而不必担心运行时的性能开销。然而，需要注意的是，如果构建不必要的命名空间，可能会影响程序的可读性。

## 本章小结

- 第三方库的使用会引入名称冲突问题。
- 如果函数被分组，并且每个组都给定一个特定名称，那么我们可以将该函数限定为某个组的一部分。
- 命名空间是一种逻辑分组机制，用于对对象进行分组，并通过该分组限定对象，以避免名称冲突问题。
- 命名空间使程序员能够无歧义地指定不同库中的对象。
- using 声明可以使库中的单个元素对程序可用，而 using 指令可以使整个库都可用。
- 可以在不使用 using 指令或声明的情况下使用命名空间中的对象。在这种情况下，我们可以使用完全限定名。
- 我们可以在命名空间内定义变量、函数和类。
- 可以扩展命名空间（`std` 命名空间除外），添加其他对象。

- 也可以使用未命名命名空间，即没有任何名称的命名空间。
- 在未命名命名空间中定义的变量，在同一个文件中与全局静态变量类似，可供程序使用。
- 可以在另一个命名空间内定义一个命名空间。这样的命名空间称为嵌套命名空间。
- 可以通过命名空间别名来缩短较长的命名空间名称。
- 当用户没有为任何对象指定命名空间名称时，编译器可以应用依赖实参查找算法，从上下文中找到该命名空间名称。该算法通常称为 Koenig 查找算法。
- 命名空间不会带来任何运行时开销，因为与命名空间相关的所有处理都在编译时解决。

## 关键词

完全限定名 指任何对象、变量或函数的名称，并带有命名空间名称和作用域解析运算符（`::`）。

全局命名空间 在旧版 C++ 中，默认情况下每个函数或类都被复制到其中的命名空间。

Koenig 查找 编译器即使在程序员未指定时也能找到正在使用的对象的准确命名空间的能力，称为 Koenig 查找。

命名空间 一种逻辑上的封装，帮助库独立存在并解决名称冲突问题。

命名空间别名 使用命名空间别名语法，为较长的完全限定名指定的较短名称，称为该较长完全限定名的命名空间别名。这个过程称为命名空间别名化。

嵌套命名空间 定义在另一个命名空间内部的命名空间称为嵌套命名空间。

未命名命名空间 没有指定任何名称的命名空间。现在推荐使用未命名命名空间来代替全局静态变量。

using 声明 一种使库中的单个元素对程序可用的机制。

using 指令 一种使库中的所有元素一次性对程序可用的机制。

## 练习题

1. 当定义一个与先前命名空间同名的命名空间时，________。

(a) 新命名空间覆盖先前命名空间
(b) 新命名空间覆盖先前命名空间
(c) 新命名空间扩展先前命名空间
(d) 编译器生成错误

2. 以下哪个是仅定义变量作为成员的命名空间的正确语法？

(a) namespace MyNamespace { int myNumber; string myString; }
(b) MyNamespace { int myNumber; string myString; }
(c) namespace MyNamespace { myNumber; myString; }
(d) MyNamespace namespace { int myNumber; string myString; }

3. ________ 使编译器能够找到某个元素的命名空间，即使该元素既没有使用 using 指令，也没有使用完全限定名。

(a) 查找
(b) 全局查找
(c) 依赖查找
(d) Koenig 查找

4. 命名空间没有 ________ 开销。

(a) 编译时
(b) 链接时
(c) 加载时
(d) 运行时

5. 命名空间可以 ________ 定义。

(a) 在编译库中
(b) 在外部程序中
(c) 分段
(d) 仅可作为整体命名空间

6. 当使用命名空间进行逻辑分组时，任何名称都可以使用语法 ________ 进行限定。

(a) namespace::element
(b) element::namespace
(c) namespace::data type element
(d) data type element::namespace

7. `namespace ABC{...};` 是以下哪种示例？

(a) 未命名命名空间
(b) 命名空间别名
(c) 常规命名空间
(d) 以上都不是

8. 如何在使用 using 指令的情况下，创建定义在名为 `MyNamespace` 的命名空间中的类 `MyClass` 的对象？

(a) `using namespace MyNamespace; MyClass <对象名>;`
(b) `using MyNamespace; MyClass <对象名>;`
(c) 两者都可以
(d) 以上都不是

9. 以下哪个语法显示了对给定命名空间中任何元素的使用？

(a) namespace::element
(b) element::namespace
(c) using namespace::element
(d) using element::namespace

10. 名称冲突问题可以通过以下方式解决：

(a) 将所有冲突的名称放在同一个封装中
(b) 将冲突的名称放在不同的封装中
(c) 必须使用唯一名称；否则无法解决
(d) 无法解决

1. 什么是名称冲突问题？如何使用命名空间解决它？

2. 命名空间如何提供逻辑分组？如何处理具有相同名称的对象？

3. 什么是完全限定名？我们何时需要使用完全限定名？

4. using 声明和 using 指令之间有什么区别？

5. 如何在不使用 using 指令或 using 声明的情况下定义对象？

6. 如何定义我们自己的命名空间？如何在命名空间内定义我们的函数并在外部使用它们？


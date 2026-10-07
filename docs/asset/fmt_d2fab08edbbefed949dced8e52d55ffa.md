
你可以将其扩展到任意层数量的间接层。例如：

```
const int* const* const ip = nullptr;
```

> 注意 另一个易于记忆的判断复杂变量定义的规则：从右向左读。例如，从左到右读是“`ip` 是一个指向 `int` 的常量指针”。另一方面，“`int* const ip`”会被读作“`ip` 是一个指向常量 `int` 的指针”。

# const 引用

由于两个原因，`const` 应用于引用要比应用于指针简单得多。首先，引用默认情况下是 `const` 的，你无法改变它们所引用的内容。因此，没有需要显式地将它们标记为 `const`。其次，你无法创建引用的引用，所以引用通常只有一层间接层。获取多层间接层的唯一方法是创建一个指向指针的引用。

因此，当 C++ 程序员提到“`const` 引用”时，他们指的是这样的：

```cpp
int z;
const int &zRef = z;
zRef = 4; // 无法编译
```

通过对 `int` 应用 `const`，你防止了对 `zRef` 赋值。记住 `const int& zRef` 等同于 `const int*`。注意，将 `zRef` 标记为 `const` 对 `z` 没有影响。你仍然可以通过直接修改 `z` 而不是引用来修改它的值。

`const` 引用最常用作参数，在那里非常有用。如果你为了效率通过引用传递东西，但不想让它被修改，请将其变为 `const` 引用。例如：

```cpp
void doSomething(const BigClass& arg)
{
  // 在这里实现
}
```

> 警告 你将对象作为参数的默认选择应该是 `const` 引用。

# const 方法

第 8 章解释了你可以将方法标记为 `const`，这可以防止方法修改类成员。该方法无法修改非 `const` 数据成员。例如，以下代码在 C++ 中无效：

```cpp
const int getArraySize() { return 32; }
int main()
{
  int myArray[getArraySize()]; // 无效
  return 0;
}
```

## constexpr 关键字

C++ 允许常量表达式的概念，并且在某些情况下需要常量表达式。例如，在定义数组时，数组的大小需要是常量表达式。使用 `constexpr` 关键字，`getArraySize()` 函数可以定义为常量表达式。常量表达式在编译时求值。

```cpp
constexpr int getArraySize() { return 32; }
int main()
{
  int myArray[getArraySize()]; // OK
  return 0;
}
```

声明 `constexpr` 函数对函数有很多限制，因为编译器必须能够在编译时评估函数，并且函数不允许有副作用。这里有一些限制：

- 函数体应该是单个返回语句，不包含 `goto` 语句或 `try catch` 块，且不抛出任何异常。允许调用其他 `constexpr` 函数。
- 函数的返回值应该是字面量。不能是 `void`。
- 如果 `constexpr` 函数是类的成员，则该函数不能是虚函数。
- 所有函数参数都应该是字面量。
- `constexpr` 函数在定义于该编译单元之前不能被调用，因为编译器需要完整的定义。
- 不允许 `dynamic_cast`。
- 不允许 `new` 和 `delete`。

通过定义 `constexpr` 构造函数，你可以创建自定义类型的实例变量。`constexpr` 构造函数应该满足以下要求：

- 所有构造函数参数都应该是字面量。
- 构造函数体不能是函数异常处理块。
- 构造函数体应满足与 `constexpr` 函数相同的要求。
- 所有数据成员必须用常量表达式初始化。

例如，以下 `Rect` 类定义了一个满足上述要求的 `constexpr` 构造函数，并定义了一个执行某些计算的 `constexpr` `getArea()` 方法。

```cpp
class Rect
{
public:
    constexpr Rect(int width, int height)
    : mWidth(width), mHeight(height) {}
    constexpr int getArea() const { return mWidth * mHeight; }
private:
    int mWidth, mHeight;
};
```

使用此类声明 `constexpr` 对象是直观的：

```cpp
constexpr Rect r(8, 2);
int myArray[r.getArea()]; // OK
```

# static 关键字

C++ 中的 `static` 关键字有多种用法，这些用法似乎互不相关。引入“重载”该关键字的动机之一，是尝试避免向语言中引入新的关键字。

## static 数据成员和方法

你可以为类声明静态 `static` 数据成员和方法。与非静态数据成员不同，`static` 数据成员不属于每个对象。该数据成员只有一份，并且存在于该类的任何对象之外。

`static` 方法同样处于类级别，独立于对象级别。`static` 方法不会在特定对象的上下文中执行执行。

第 8 章提供了关于静态数据成员和方法的相关示例。

## static 链接

在介绍 `static` 关键字在链接中的用法之前，你需要理解 C++ 中“链接”`linkage`的概念。每个源文件都是独立编译的，生成的对象文件会被链接在一起。C++ 源文件中的每个名称包括函数和全局变量都具有内部或外部的链接。外部链接意味着该名称在其他源文件中可用。内部链接也称为静态链接意味着它不可用。默认情况下，函数和全局变量具有外部链接。然而，你可以通过在声明前加上 `static` 关键字来指定内部或静态链接。例如，你有两个源文件：`FirstFile.cpp` 和 `AnotherFile.cpp`。这里是 `FirstFile.cpp`：

```cpp
void f();
int main() {
    f();
    return 0;
}
```

请注意，该文件提供了 `f()` 的原型，但没有显示定义。这里是 `AnotherFile.cpp`：

```cpp
#include <iostream>
using namespace std;
void f();
void f() {
    cout << "*f\n";
}
```

该文件同时提供了 `f()` 的原型和定义。请注意，在两个不同的文件中为同一个函数编写原型是合法的。这正是预处理器为你做的事情：你将原型放在一个头文件中，并在每个源文件中对其进行 `#include`。使用头文件的原因是更容易维护并保持同步一份原型的副本。然而，在这个示例中，我没有使用头文件。

这些源文件每一个编译时均不会报错，且程序可以正常链接：因为 `f()` 具有外部链接，`main()` 可以从另一个文件调用它。

然而，假设你在 `AnotherFile.cpp` 的 `f()` 原型上使用了 `static`。注意，你不需要在 `f()` 的定义前重复 `static` 关键字。只要它出现在函数名称第一次出现之前，就不需要重复它。

```cpp
#include <iostream>
using namespace std;
static void f();
void f() {
    cout << "*f\n";
}
```

现在，每个源文件编译时都没有报错，但链接步骤失败了，因为 `f()` 具有内部静态链接，导致它在 `FirstFile.cpp` 中不可用。某些编译器在定义了 `static` 方法但在该源文件中未使用时，会发出警告暗示它们并不是静态的，因为它们在其他地方被自豪地被使用了。

使用 `static` 进行内部链接的替代方案是使用匿名命名空间 `anonymous namespaces`。与其将变量或函数设为 `static`，不如将其封装在如下无名的命名空间中：

```cpp
#include <iostream>
using namespace std;
namespace {
    void f();
    void f() {
        cout << "*f\n";
    }
}
```

匿名命名空间中的实体可以在同一源文件中声明后的任何地方被访问，但不能从其他源文件访问。这些语义与通过 `static` 关键字获得的语义是相同的。

## extern 关键字

另一个相关的关键字 `extern` 似乎应该是 `static` 的相反面，它为其前后的名称指定外部链接。它可以在某些情况下使用，例如，`const` 和 `typedef` 默认具有内部链接。你可以使用 `extern` 给它们赋予外部链接。然而，`extern` 具有一些复杂性。当你将一个名称指定为 `extern` 时，编译器将其视为一个声明，而不是定义。对于变量，编译器不会为该变量分配空间。你必须提供一个不带 `extern` 关键字的变量定义行。例如：

```cpp
extern int x;
int x = 3;
```

或者，你也可以在 `extern` 行中初始化 `x`，这样该行既是声明也是定义：

```cpp
extern int x = 3;
```

在这种情况下，`extern` 并不十分用，因为 `x` 默认就具有外部链接。`extern` 的真正用途是你想从另一个源文件 `FirstFile.cpp` 中使用 `x`：

```cpp
#include <iostream>
using namespace std;
extern int x;
int main() {
    cout << x << endl;
}
```

在这里，`FirstFile.cpp` 使用了 `extern` 声明以便使用 `x`。编译器在 `main()` 中使用 `x` 需要 `x` 的声明。如果你在没有 `extern` 关键字的情况下声明了 `x`，编译器会认为这是一个定义并为 `x` 分配空间，导致链接失败因为全局作用域中没有两个变量。通过 `extern`，你可以让变量在多个源文件中全局访问。

不建议使用全局变量。它们会令人困惑且容易出错，特别是在大型程序中。对于类似的功能，你可以使用静态类数据成员和方法。

## 函数中的静态变量

```cpp
void performTask() {
    static bool initialized = false;
    if (!initialized) {
        cout << "initializing\n";
        // 执行初始化。
        initialized = true;
    }
    // 执行所需的任务。
}
```

然而，静态变量是令人困惑的，通常有更好的方法来组织代码以避免使用它们。在这种情况下，你可以使用静态类数据成员和方法。

`typedef` 可以包含作用域限定符。前面的示例通过为 `StringVector` 包含作用域 `std` 显示了这一点。

STL 广泛使用 `typedef` 为类型提供更短的。例如，`string` 实际上是一个如下所示的 `typedef`：

```
typedef basic_string<char, char_traits<char>, allocator<char>> string;
```

# 函数指针的 typedef

`typedef` 最复杂的用法是定义函数指针。虽然函数指针在 C++ 中并不常见通常被虚拟方法所取代，但在某些情况下仍有获取函数指针的需求。最常见的例子是在从动态库中获取函数指针。接下来的示例显示了微软 Windows 动态链接库 `DLL` 中的一个函数指针。Windows DLL 的细节不属于平台无关 C++ 的范畴，但对程序员来说，讨论它是值得的，而且它是解释函数指针通用细节的一个指针。

考虑一个有一个名为 `MyFunc()` 函数的 DLL。如果你只需要调用 `MyFunc()`，在 Windows 中仅通过 `LoadLibrary()` 内核调用即可完成库的运行时加载：

```
HMODULE lib = ::LoadLibrary("library name");
```

此调用的结果被称为“库句柄”，如果出错则返回 `NULL`。在从库中调用函数之前，你需要知道该函数的原型。假设以下是 `MyFunc()` 的原型，它返回一个 `int` 并接受三个参数：一个布尔、一个 `int` 和一个 C 风格字符串。

```
int __stdcall MyFunc(bool b, int n, const char* p);
```

`__stdcall` 是一个微软特定的指令，用于指定如何向函数传递参数以及如何清理它们。

你现在可以使用 `typedef` 为具有上述原型的函数指针定义一个短名称 `MyFuncProc`。

```
typedef int (*__MyFuncProc)(bool b, int n, const char* p);
```

注意 `typedef` 名称 `MyFuncProc` 嵌入在语法的中间。从这个示例可以明显看出这类 `typedef` 是复杂的。下一节将为你展示一个更整洁的解决方案

在成功加载库并为函数指针定义了短名称后，你可以按照如下方式获取库中的函数指针：

```
MyFuncProc MyProc = ::GetProcAddress(lib, "MyFunc");
```

如果失败，`MyProc` 将为 `NULL`。如果成功，你可以调用加载的函数：

```
MyProc(true, 3, "Hello world");
```

一个 C 程序员可能会认为在调用函数指针之前需要对其进行解引用，如下：

```
(*MyProc) (true, 3, "Hello world");
```

这在几十年前是真的 `true`，但现在每个 C 和 C++ 编译器都足够智能，知道如何在调用之前自动解引用函数指针。

# 类型别名

在某些情况下，类型别名比 `typedef` 更容易理解。例如，采用以下 `typedef`：

```
typedef int MyInt;
```

可以使用类型别名写如下：

```
using MyInt = int;
```

这种类型别名在 `typedef` 对于函数变得复杂的情况下如上一节特别有用。例如，以下 `typedef` 定义了一个函数指针，它返回一个整数并接受一个 `char` 和一个 `double` 作为参数：

```
typedef int (*FuncType)(char, double);
```

这个 `typedef` 有点复杂，因为名称 `FuncType` 位于它的中间。使用类型别名，可以写如下：

```
using FuncType = int (*) (char, double);
```

通过阅读这些，你可能会认为类型别名并没有比 `typedef` 容易得多，但还有更多内容。`typedef` 的问题在你想配合模板使用它们时会变得明显，但这在第11 章中涵盖，它需要更多关于模板的细节。

# 转换

C++ 提供了四种特定的转换：`static_cast`、`dynamic_cast`、`const_cast` 和 `reinterpret_cast`。

旧的 C 风格转换 `()` 在 C++ 中仍然有效，并在现有代码库中被广泛使用。C 风格转换涵盖了所有的 C++ 转换，因此更容易出错，因为并不清楚你想实现什么。强烈建议在新代码中使用仅 C++ 风格的转换，因为它们在语法上更清晰。

本节描述了每种 C++ 转换的用途以及何时使用它们。

# const_cast

**`const_cast`** 是最直接的转换。你可以用它去掉变量的 `const` 属性。它是四种转换中唯一去掉 `const` 属性的。理论上，当然不需要 `const_cast`。如果一个变量是 `const`，它应该保持为 `const`。但在实践中，你有时会发现自己需要调用一个接受非 `const` 变量的函数，而你必须传递它。正确的解决方案是在程序中保持 `const` 的一致性，但不总是可能的，特别是当你使用第三方库时。因此，你可能需要去掉变量的 `const` 属性，但只有当你确定函数不会修改该对象时才这样做，否则除了重构程序外没有其他选择。这里有一个示例：

```
extern void ThirdPartyLibraryMethod(char* str);
void f(const char* str) {
    ThirdPartyLibraryMethod(const_cast<char*>(str));
}

# static_cast

可以使用 `static_cast` 执行编译时已知的转换。例如，如果你想将 `int` 转换为 `double`，可以使用 `static_cast`：

```

double d = static_cast<double>(i);

```

`static_cast` 的另一个用法是在继承层次执行向下转换。例如，如果你有一个基类和一个派生类，你可以将基类指针转换为派生类指针：

```cpp

class Base {

    public:

    Base() {}

    virtual ~Base() {}

};

class Derived : public Base {

    public:

    Derived() {}

};

int main() {

    Base* b = new Derived();

    Derived* d = static_cast<Derived*>(b);

    delete b;

    return 0;

}

```

注意 `static_cast` 不进行运行时检查。如果 `Base` 对象实际上没有指向 `Derived` 对象，你却将其转换为 `Derived` 指针，结果将是非定义行为。例如：

```cpp

Base* b = new Base();
```

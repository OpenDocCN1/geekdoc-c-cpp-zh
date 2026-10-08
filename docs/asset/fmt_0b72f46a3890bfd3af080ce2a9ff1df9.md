
### 移动构造函数

`91:   MyString(MyString&& MoveSource)`

```cpp
92: {
93:     cout << "Move constructor to move from: " << MoveSource.Buffer << endl;
94:     if(MoveSource.Buffer != NULL)
95:     {
96:         Buffer = MoveSource.Buffer; // 获取所有权，即“移动”
97:         MoveSource.Buffer = NULL; // 释放移动源
98:     }
99: 
100:    return *this; // 修复：构造函数不应返回 *this
101: }
```

### 移动赋值运算符

`102:   MyString& operator=(MyString&& MoveSource)`

```cpp
103: {
104:     cout << "Move assignment operator to copy from: " << MoveSource.Buffer << endl;
105:     if ((MoveSource.Buffer != NULL) && (this != &CopySource))
106:     {
107:         if (Buffer != NULL)
108:             delete[] Buffer; // 释放所有缓冲区
109:         Buffer = MoveSource.Buffer; // 获取所有权，即“移动”
110:         MoveSource.Buffer = NULL; // 释放移动源
111:     }
112: 
113:     return *this;
114: }
```

`115: int main()`

`116: {`

```cpp
117:   MyString('Hello');
118:   MyString('World');
119:   MyString('C++');
120:   MyString('overwrite this');
121:   sayHelloAgain = Hello + World;
122:   return 0;
123: }
```

# 第 12 节：运算符类型与运算符重载

列表 12.12 续）

### 输出

没有移动构造函数和赋值运算符的输出（注释掉 95-19）：

`Constructor called: Hello`

`Constructor called: World`

`Constructor called: C++`

`Constructor called: overwrite this`

`operator called:`

`Default constructor`

`Copy constructor to copy from: World`

`operator called:`

`Default constructor`

`Copy constructor to copy from: C++`

启用移动构造函数和赋值运算符的输出：

`Constructor called: Hello`

`Constructor called: World`

`Constructor called: C++`

`Constructor called: overwrite this`

`operator called:`

`Default constructor`

`Move constructor to move from: World`

`operator called:`

`Default constructor`

`Move constructor to move from: C++`

### 分析

这可能是一个长代码示例，但大部分已经在之前的示例和课程中演示。最重要的部分是 95-19 行，它们分别实现了移动构造函数和赋值运算符。受此影响的输出部分已加粗。再次查看移动构造函数和赋值运算符的实现，你会发现移动语义本质上是通过从源获取所有权来实现的，如 101 行和 114 行所示。因此，即使移动源被销毁，通过析构函数（程序位于 16-20）调用的 `delete` 实际上什么也没有做，因为所有权已经转移到了目标对象。注意，在没有移动构造函数的情况下会调用拷贝构造函数，它会对指向的字符串进行深拷贝。因此，移动构造函数通过减少不需要的内存分配和拷贝步骤了大量的处理时间。

编写移动构造函数和赋值运算符是完全可选的。与拷贝构造函数和拷贝赋值运算符不同，编译器不会为你提供默认实现。使用此 C++11 特性优化指向动态分配资源的类，否则这些资源在临时情况下会被深拷贝。

# 运算符无法重载

尽管 C++ 在自定义运算符行为和使你的类易于使用方面提供了巨大的活性，但它保留了一些底牌，不允许你更改或改变某些预期行为保持一致的运算符的行为。不能重新定义的运算符见表 12.3。

**表 12.3** 无法被重载或重新定义的运算符

| 运算符 | 名称 |
| --- | --- |
| `.` | 成员选择 |
| `*` | 指针到成员选择 |
| `::` | 作用域解析 |
| `? :` | 条件三元运算符 |
| `sizeof` | 获取对象/类类型的大小 |

# 第 12 课：运算符类型与运算符重载

| 应当 (DO) | 绝不要 (DON'T) |
|---|---|
| 应当尽可能编写许多有助于让你的类变得易于使用的运算符，但不要过度。 | 绝不要忘记，如果你不提供这些内容，编译器会定义默认的拷贝赋值运算符和拷贝构造函数，而且它们无法确保类中包含的任何原始指针的深拷贝。 |
| 应当对于包含原始成员的类，务必编写拷贝赋值运算符（以及配套的拷贝构造函数和析构函数）。 | 不要忘记，如果你不提供移动赋值运算符或移动构造函数，编译器就不会创建它们，而是回退到普通的拷贝赋值运算符和拷贝构造函数。 |
| 应当在使用符合 C++11 标准的编译器时，对于管理动态分配资源（如数据数组）的类，务必编写移动赋值运算符（移动构造函数）。 | 不要忘记，编写运算符是可选的，但它能提高你类的易用性。 |
| | 不要忘记，在你编写了 `operator (*)` 和 `operator (-)` 之前，你的智能指针类还不是一个指针；在你实现了析构函数并考虑了拷贝赋值和拷贝构造的情况之前，它也不足够智能。 |

## 总结

你学习了编写运算符如何显著提高你的类被调用的易用性。在编写管理资源的类（例如动态数组或字符串）时，除了析构函数外，你至少需要提供拷贝构造函数和拷贝赋值运算符。一个管理动态数组的工具类配合移动赋值运算符效果非常好，该运算符可以确保临时对象不会对资源进行深拷贝。最后，你还学习了诸如 `*`、`::`、`?` 和 `sizeof` 等运算符是无法重定义的。

# 问答 (Q&A)

问 我的类封装了一个整数动态数组。我至少应该实现哪些函数和运算符？

答 在编写此类类时，你需要明确定义当实例通过赋值直接拷贝到另一个实例，或通过值传递给函数进行间接拷贝时的行为。你通常需要实现拷贝构造函数、拷贝赋值运算符和析构函数。如果你想在某些情况下调优该类的性能，还需要实现移动构造函数和移动赋值运算符。

问 我有一个类对象。我想支持这种语法：`cout << object;`。我需要实现什么运算符？

答 你需要实现一个转换运算符，允许你的类被解释为 `std::cout` 可以处理的类型。一种方法是像你在列表 I2.2 中做的那样定义 `operator char*()`。

问 我想创建自己的智能指针类。我至少需要实现哪些函数和运算符？

答 智能指针需要提供像普通指针一样的使用，例如 `*pSmartPtr` 或 `pSmartPtr->func()`。为了实现这一点，你需要实现 `operator (*)` 和 `operator (-)`。为了使其足够智能，还需要通过相应编写析构函数来处理资源的自动释放/返回，并通过实现拷贝构造函数和拷贝赋值运算符（或将这两个设为私有）来明确定义拷贝或赋值的工作方式。

# 工作坊 (Workshop)

工作坊包含测验题，帮助你巩固对涵盖内容的理解，并提供使用所学知识的练习。在检查附录 D 中的答案之前，尝试回答测验和练习题，并在进入下一节之前确保你已经理解了答案。

# 测验 (Quiz)

+ 1. 我的下标运算符 `[]` 可以返回返回类型的 `const` 和非 `const` 变体吗？

   `const Type& operator[](int Index);`

   `Type& operator[](int Index); // 这样可以吗？`

+ 2. 你会将拷贝构造函数或拷贝赋值运算符声明为私有吗？

+ 3. 为你的 `Date` 类定义移动构造函数和移动赋值运算符有意义吗？

# 练习 (Exercises)

+ 1. 为 `Date` 类编写一个转换运算符，将它持有的日期转换为唯一的整数。

+ 2. 为 `DynIntegers` 类编写一个移动构造函数和移动赋值运算符，该类以私有成员 `int*` 的形式封装了动态分配的数组。

# 第 13 课

## 转换运算符 (Casting Operators)

转换是程序员可以临时或永久改变编译器对对象解释的机制。注意，这并不意味着程序员改变了对象本身——他只是改变了对象的解释。改变对象解释的运算符被称为转换运算符。

在本节中，你将学习：

- 转换运算符的必要性
- 为什么 C 风格转换不受某些 C++ 程序员欢迎
- 四种 C++ 强制转换运算符
- 向上转换（upcasting）和向下转换（downcasting）的概念
- 为什么 C++ 转换运算符也不是一直的首选

### 转换的必要性

在一个完美类型安全且类型强大的世界中，良好的 C++ 应用程序是不需要转换和转换运算符的。然而，我们生活在一个真实的世界中，由许多不同的人和供应商编写的模块经常在不同的环境中工作。为了实现这一点，编译器通常需要以某些方式解释数据，以便能够正确编译和运行应用程序。

让我们来看一个真实示例：尽管某些 C++ 编译器可能支持将某些视为原生类型，但许多库仍在使用 C 语言。为了实现这一点，C 编译器依赖于：

```cpp
typedef unsigned BOOL;
```

使用整型类型来持有布尔数据的函数声明如下：

```cpp
BOOL IsX();
```

现在，如果要在最新版本中使用此类库，程序员需要一种让编译器理解 `bool` 类型的方法。这种方法是使用：

```cpp
bool Result = (bool)IsX(); // C 风格转换
```

C++ 的演变看到了新转换运算符的出现，这在 C++ 社区中引发了分裂：一组继续在应用程序中使用 C 风格转换，而另一组则严格遵守转换关键字。前一组的论点是 C++ 转换使用起来繁琐，且在功能上微乎其微，以至于只有理论价值。后一组（显然由 C++ 专家组成）指出了 C 风格转换的缺陷。

由于现实世界中存在这两种代码，最好仔细阅读本节，了解每种方法的优缺点并形成自己的观点。

# 为什么 C 风格转换不受某些 C++ 程序员欢迎

类型安全是 C++ 程序员信誉该编程语言品质的准则之一。事实上，大多数 C++ 编译器不会允许这样做：

```cpp
char* pszString = 'Hello World!';
int* pBuf = pszString; // 错误：无法将 char* 转换为 int
```

而且完全如此！

现在，C++ 编译器仍然认为需要向后兼容以构建旧和遗留代码，因此自动允许如下语法：

```cpp
int* pBuf = (int*)pszString; // 解决一个问题，引入另一个
```

然而，C++ 风格实际上强制编译器将目标解释为程序员选择的非常方便的类型——这个程序员在这种情况下没有考虑编译器报告错误是有道理的，却扼杀了编译器并强迫它执行。这对于那些看到自己的类型安全被强制转换所破坏的 C++ 程序员来说并不受欢迎。

# C++ 转换运算符

尽管转换有缺点，但转换的概念本身无法丢弃。在许多情况下，转换是确保重要兼容性问题的合法需求。C++ 额外提供了一种针对继承场景的新转换运算符，这在 C 编程中是不存在的。

四种 C++ 转换运算符是：

- `static_cast`
- `dynamic_cast`
- `reinterpret_cast`
- `const_cast`

转换运算符的使用语法是一致的：

```cpp
destination_type result = cast_type <destination_type> (object_to_be_casted);
```

# 使用 static_cast

`static_cast` 是一种用于在相关类型之间转换指针的机制，并对标准数据类型执行显式类型转换（这些转换在其他情况下会自动或隐式地发生）。对于指针而言，`static_cast` 实现了基础的编译时检查，以确保指针正被转换为相关类型。这是对 C 风格转换的改进，C 风格转换允许指针在没有任何检查的情况下转换为无关的类型。使用 `static_cast`，可以将指针向上转型为基类类型（upcasted），也可以向下转型为派生类型（downcasted），如下代码示例所示。

```
Base* pbase = new Derived(); // 构造一个 Derived 对象
Derived* pDerived = static_cast<Derived>(pbase); // OK！

// Unrelated 不通过任何继承层次结构与 Base 关联
Unrelated* pUnrelated = static_cast<Unrelated>(pbase); // 错误
// 上述转换是不允许的，因为类型是不相关的
```

将 `Derived*` 转换为 `Base*` 称为向上转型（upcasting），可以在不使用任何显式转换符的情况下完成：

```
Derived objDerived;
Base* pbase = &objDerived; // OK！
```

将 `Base*` 转换为 `Derived*` 称为向下转型（downcasting），无法在没有显式转换符的情况下完成：

```
Derived objDerived;
Base* pbase = &objDerived; // 向上转型 -> OK！
Derived* pDerived = pbase; // 错误：向下转型需要显式转换
```

注意，`static_cast` 仅验证指针类型是相关的。它不执行任何运行时检查。因此，使用 `static_cast` 时程序员仍然可能遇到这种 Bug：

```
Base* pbase = new Base();
Derived* pDerived = static_cast<Derived*>(pbase); // 仍然没有错误！
```

在这里，`pDerived` 实际上指向一个部分的 `Derived` 对象，因为所指向的对象实际上是 `Base()` 类型。由于 `static_cast` 仅执行验证相关类型是否相关的编译时检查，而不执行运行时检查，因此调用 `pDerived->SomeDerivedClassFunction()` 将通过编译，但在运行时可能会导致意料之外的行为。

# C++ 转换符

除了有助于向上转型或向下转型外，`static_cast` 在很多情况下还可以帮助将隐式转换显式化并引起程序员或读者的注意：

```
double dPi = 3.14159265;
int Num = static_cast<int>(dPi); // 将原本隐式的转换变为显式
```

在前述代码中，`Num = dPi` 也可以良好地工作且效果相同。然而，使用 `static_cast` 会将转换的本质引起读者的注意，并向（那些熟悉 `static_cast` 的人）表明编译器已经根据编译时可用信息执行了必要的调整以完成所需的转换。

# 使用 dynamic_cast 和运行时标识

动态转换（Dynamic casting）正如其名，是静态转换的对立面，它实际上在运行时执行转换——即在应用程序执行时。`dynamic_cast` 的结果可以被检查，以判断转换尝试是否成功。`dynamic_cast` 符的典型语法是：

```
destination_type* pDest = dynamic_cast <class_type> (pSource);
```

```
if (pDest)
    // 在使用指针之前检查转换是否成功
    pDest->CallFunc();
```

例如：

```
Base* pBase = new Derived();
```

```
// 执行向下转型
Derived* pDerived = dynamic_cast<Derived*>(pBase);
```

```
if (pDerived)
    // 检查转换是否成功
    pDerived->CallDerivedClassFunction();
```

在前述简短示例中，给定一个指向基类对象的指针，程序员可以利用 `dynamic_cast` 在继续使用该指针之前验证所指向的目标对象的类型。注意，在代码片段中显然该对象是 `Derived` 类型。

# C++ 类型转换运算符

361

### 注意

> 尽可能地，你应该在应用程序中避免使用 `reinterpret_cast`，因为它允许你指示编译器将类型 X 解释为不相关的类型 Y，这看起来并不像良好的设计或实现。

# 使用 const_cast

`const_cast` 允许你关闭对对象的 `const` 访问修饰符。如果你在怀疑为什么这有必要，那么你的直觉可能是正确的。在程序员正确编写类的理想情况下，请记住在正确的位置频繁地使用 `const` 关键字。遗憾的是，现实世界要不同得多，像下面的代码非常常见：

```cpp
class SomeClass{
public:
    void DisplayMembers(); // 显示函数应该是 const 的
};
```

所以，当你像这样编写函数时：


- 1. 在定义时不进行实例化的情况下，模板代码本身会忽略模板参数进行正确性检查。这包括：
  - 检测语法错误，例如缺少分号。
  - 检测使用了不依赖于模板参数但未知的名称（类型名、函数名等）。
  - 检查不依赖于模板参数的静态断言。
- 2. 在实例化时，会（再次）检查该模板代码以确保所有代码有效。也就是说，现在尤其是所有依赖于模板参数的部分都会被再次检查。

例如：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_25_0.png)

```cpp
template<typename T>
void foo(T t)
{
    undeclared();       // first-phase compile-time error if undeclared() unknown
    undeclared(t);      // second-phase compile-time error if undeclared(T) unknown
    static_assert(sizeof(int) > 10, // always fails if sizeof(int) <= 10
                  "int too small");
    static_assert(sizeof(T) > 10,   // fails if instantiated for T with size <= 10
                  "T too small");
}
```

有些部分被检查两次的现象称为两阶段查找，将在第249页的14.3.1节详细讨论。

注意，某些编译器不会执行第一阶段的全部检查。因此，在模板代码至少被实例化一次之前，你可能不会发现所有普遍问题。

### 编译和链接

两阶段翻译在实践中给模板处理带来了一个重要问题：当函数模板以触发其实例化的方式使用时，编译器在某个时刻需要看到模板的定义以及模板内部使用的所有实体的声明。对于普通函数，声明和定义通常是分开的；函数的定义足以编译它。然而，对于模板来说，这个问题要困难得多，如第6章所述。当前（但并非最简单）的做法是：将每个模板都实现在头文件中。

## 1.2 模板实参推导

当我们为某些实参调用函数模板（如max()）时，模板参数由我们传入的实参决定。如果我们为函数参数使用参数类型T，编译器必须推导出T必须是……

然而，T可能只是类型的一部分。例如，如果我们声明max()使用常量引用：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_25_1.png)

```cpp
template<typename T>
T max(T const& a, T const& b)
{
    return b < a ? a : b;
}
```

并且传入一个int，T同样被推导为int，因为函数参数与int const&匹配。

### 类型推导过程中的类型转换

- 注意，类型推导过程中自动类型转换是受限的：
  - 通过引用推导调用参数时，即使平凡转换也不适用于类型推导。使用同一模板参数T声明的两个实参必须完全匹配。
  - 通过值推导调用参数时，仅支持会发生退化的平凡转换：忽略cv限定符（const和volatile），引用转换为被引用的类型，原始数组或函数转换为相应的指针类型。对于使用同一模板参数T声明的两个实参，退化后的类型必须匹配。

例如：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_25_2.png)

```cpp
template<typename T>
T max(T a, T b)
{
    ...
}
...
int a = 42;
int b = 42;
max(a, b);            // OK: T is deduced as int
max(1, 2);            // OK: T is deduced as int
max(1, 2.0);          // ERROR: T can be deduced as int or double
...
int i = 42;
double d = 42.0;
max(i, d);            // ERROR: T can be deduced as int or double
max(1, 2.0);          // ERROR: T can be deduced as int or double
...
```

然而，下面这些是错误的：

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_25_3.png)

```cpp
max(4, 7.2);          // ERROR: T can be deduced as int or double
...
double d;
max(4, d);            // ERROR: T can be deduced as int or double
```

- 1. 转换实参，使两者匹配：

```cpp
max(static_cast<double>(7), 7.2);    // OK
```

- 2. 显式指定（或限定）类型T，以防止编译器尝试类型推导：

```cpp
max<double>(7, 7.2);    // OK
```

- 3. 指定参数可以具有不同的类型。

第9页的1.3节将详细阐述这些选项。第108页的7.2节和第15章将详细讨论模板函数推导过程中的类型转换规则。

### 默认实参的类型推导

请注意，类型推导不适用于默认调用实参。例如：

```cpp
template<typename T>
void f(T = 7);
```

```cpp
f();    // error: cannot deduce T
f(1);   // OK
```

为了支持这种情况，你还必须为模板参数声明一个默认实参，这将在第13页的1.4节中讨论：

```cpp
template<typename T = std::string>
void f(T = "");

f();    // OK
```

## 1.3 多个模板参数

到目前为止我们已经看到，函数模板有两组不同的参数：

- 1. **模板参数**，在函数模板名称之前的尖括号中声明：

  ```cpp
  template<typename T>
  ```

- 2. **调用参数**，在函数模板名称之后的圆括号中声明：

  ```cpp
  T max (T a, T b)       // a and b are call parameters
  ```

你可以拥有任意数量的模板参数。例如，你可以为两个可能不同类型的参数定义max()模板：

```cpp
template<typename T1, typename T2>
T1 max (T1 a, T2 b)
{
    return b < a ? a : b;
}
auto m = max(7, 4.2);    // OK, but type of first argument defines return type
```

能够向max()模板传递不同类型的参数似乎很理想，但这同时也包含一个问题。如果你使用其中一个参数类型作为返回类型，另一个参数的实参可能会被转换为该类型，而不管调用者的意图如何。因此，返回类型取决于调用实参的顺序。66.66和42的最大值将是double类型的66.66，而42和66.66的最大值将是int类型的66。

C++提供了不同的方式来处理这个问题：

- 为返回类型引入第三个模板参数。
- 让编译器推断返回类型。
- 将返回类型声明为两个参数类型的“公共类型”。

所有这些选项将在接下来讨论。

### 1.3.1 返回类型的多个模板参数

我们之前的讨论表明，模板实参推导允许我们以与调用普通函数相同的语法调用函数模板。我们不必显式指定与模板参数对应的类型。

然而，我们也提到过，我们可以显式指定用于模板参数的类型：

当模板参数和调用参数之间没有联系，且无法推导出模板参数时，你必须在调用时显式指定模板实参。例如，你可以引入第三个模板实参类型来定义函数模板的返回类型：

```cpp
template<typename T1, typename T2, typename RT>
RT max (T1 a, T2 b);
```

然而，模板实参推导不考虑返回类型，并且RT不会出现在函数调用参数的类型中。因此，RT无法被推导。

因此，你必须显式指定模板实参列表。

```cpp
template<typename T1, typename T2, typename RT>
RT max (T1 a, T2 b);

::max<int,double,double>(4, 7.2);       // OK; but ambiguous
```

到目前为止，我们看到的都是要么显式指定全部函数模板实参，要么全部不指定的情况。另一种方法是只显式指定前几个实参，并让推导过程推导出其余实参。通常，你必须指定到最后一个无法隐式确定的实参类型为止的所有实参类型。因此，如果在我们的示例中改变模板参数顺序，调用者只需指定返回类型：

```cpp
template<typename RT, typename T1, typename T2>
RT max (T1 a, T2 b)
{
    return b < a ? a : b;
}

::max<double>(4, 7.2)      // OK: return type is double, T1 and T2 are deduced
```

在这个示例中，对max<double>的调用显式要求RT为double，但参数T1和T2会根据实参被推导为int和double。

注意，这些修改后的max()版本并不会带来显著优势。一个原因是，你已经可以指定函数调用的参数类型。实际上，结果并不依赖于你传入的实参类型。因此，如果使用max()是为了保持简单而不使用运算符版本，你可以改用以下实现。这样，你还可以按不同顺序定义函数模板参数。

有关推导过程的详细信息，请参阅第6章。

### 1.3.2 推导返回类型

如果返回类型依赖于模板参数，推导返回类型最简单也是最好的方法是让编译器来推导。自C++14起，只需不声明任何返回类型（你仍然必须将返回类型声明为auto）即可实现：

basics/auto.cpp

```cpp
template<typename T1, typename T2>

auto max (T1 a, T2 b)
{
    return b < a ? a : b;
}
```

实际上，在不使用相应的尾置返回类型语法（即用->引入）的情况下，使用auto作为返回类型意味着实际返回类型必须从函数体中的返回语句推导出来。当然，函数体的类型必须是有效的。因此，代码必须是可用的，并且多个返回语句必须匹配。

在C++14之前，只能通过使用实例化点处的函数类型来让编译器确定返回类型。在C++11中，我们可以利用尾置返回类型语法允许我们使用调用参数这一优势。也就是说，我们可以声明返回类型由operator<的结果推导而来：

basics/decltype.cpp

```cpp
template<typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype(b < a ? b : a)
{
    return b < a ? a : b;
}
```

在这里，结果类型由operator ?:的规则决定，这些规则相当复杂，但通常会产生符合直觉的预期结果。

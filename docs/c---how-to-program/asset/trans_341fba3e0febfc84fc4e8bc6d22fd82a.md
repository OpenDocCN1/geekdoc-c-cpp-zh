
为了支持列表初始化，你可以定义一个接收类模板 `initializer_list` 的对象的构造函数。对于类 `Array`，你需要包含 `<initializer_list>` 头文件。然后，你可以定义一个构造函数，其第一行为：

```cpp
Array::Array( initializer_list< int > list )
```

你可以通过调用其 `size` 成员函数来确定列表参数中的元素数量。为了获取每个初始化项并将其复制到 `Array` 对象的动态分配内置数组中，你可以使用基于范围的 for 循环如下：

```cpp
size_t i = 0;
for ( int item : list )
    ptr[ i++ ] = item;
```

## 18.11 作为成员函数与非成员函数的运算符

无论运算符函数是作为 *member function* 实现还是作为 *non-member function* 实现，运算符在表达式中的使用方式仍然相同。那么哪种更好？

当运算符函数作为 *member function* 实现时，*leftmost*（或唯一）的操作数必须是运算符类的对象（或对象的引用）。如果左操作数必须是不同类的对象或基本类型，则此运算符函数 *必须* 作为 *non-member function* 实现（如我们在第 18.5 节中所做的那样，将 `<<` 和 `>>` 重载为流插入和流提取运算符）。如果该函数必须直接访问类的私有或受保护成员，则可以使 *non-member operator function* 成为该类的友元。

特定类的 *Operator member functions* 仅在二元运算符的 *left* 操作数 specifically 是该类的对象时，或一元运算符的 *single* 操作数是该类的对象时才会被编译器 (*implicitly* 调用)。

### 可交换运算符

选择非成员函数重载运算符的另一个原因是使运算符能够 *commutative*。例如，假设我们有一个 *fundamental type variable*，`number`，类型为 `long int`，以及一个 *object* `bigInteger1`，属于类 `HugeInt`（一个整数可以任意大而不受底层硬件机器字大小限制的类；类 `HugeInt` 在章节练习中开发）。加法运算符 (+) 会生成一个 *temporary HugeInt object*，作为 `HugeInt` 和 `long int` 的和（如表达式 `bigInteger1 + number` 中），或作为 `long int` 和 `HugeInt` 的和（如表达式 `number + bigInteger1` 中）。因此，我们要求加法运算符是 *commutative*（正如它在两个基本类型操作数时一样）。问题在于，如果要将该运算符重载为 *member function*，则类对象 *必须出现在* 加法运算符的 *left*。因此，我们还将运算符重载为 *non-member function*，以允许 `HugeInt` 出现在加法的 *right*。处理 *left* 上的 `HugeInt` 的 `operator+` 函数仍然可以是 *member function*。*non-member function* 只需交换其参数并调用 *member function* 即可。

## 18.12 在类型之间转换

大多数程序处理多种类型的信息。有时所有操作都“stay within a type”。例如，将 `int` 加到 `int` 上会产生一个 `int`。然而，通常有必要将一种类型的数据转换为另一种类型的数据。这可能发生在赋值中、在计算中、在向函数传递值时以及从函数返回值时。编译器知道如何在基本类型之间执行某些转换。你可以使用 *cast operators* 来 *force* 基本类型之间的转换。

但对于用户定义的类型呢？编译器无法预先知道如何在用户定义类型之间以及用户定义类型与基本类型之间进行转换，因此你必须指定如何执行此操作。这种转换可以使用转换构造函数来执行——可以带单个参数调用的构造函数（我们将这些称为 *single-argument constructors*）。这样的构造函数可以将其他类型（包括基本类型）的对象转换为特定类的对象。

### 转换运算符

转换运算符（也称为 *cast operator*）可用于将一个类的对象转换为另一种类型。这样的转换运算符必须是 *non-static member function*。函数原型

```cpp
MyClass::operator char *() const;
```

声明了一个重载的转换运算符函数，用于将类 `MyClass` 的对象转换为临时的 `char *` 对象。运算符函数被声明为 `const`，因为它 does *not* 修改原始对象。重载转换运算符函数的返回类型 *implicitly* 为对象正在被转换成的类型。如果 `s` 是一个类对象，当编译器看到表达式 `static_cast<char *>(s)` 时，编译器会生成调用

```cpp
s.operator char *()
```

以将操作数 `s` 转换为 `char *`。

### 重载的转换运算符函数

可以定义重载的转换运算符函数来将用户定义类型对象的对象转换为基本类型或转换为其他用户定义类型的对象。原型

```cpp
MyClass::operator int() const;
MyClass::operator OtherClass() const;
```

声明了重载的转换运算符函数，可分别将用户定义类型 `MyClass` 的对象转换为整数或转换为用户定义类型 `OtherClass` 的对象。

### 对转换运算符和转换构造函数的隐式调用

转换运算符和转换构造函数的优点之一是，在必要时，编译器可以 *implicitly* 调用这些函数以创建 *temporary* 对象。例如，如果用户定义的 `String` 类的对象 `s` 在程序中出现在期望普通 `char *` 的位置，例如

```cpp
cout << s;
```

编译器可以调用重载的转换运算符函数 `operator char *` 将对象转换为 `char *` 并在表达式中使用结果的 `char *`。有了为 `String` 类提供的此转换运算符，流插入运算符就不必重载以使用 `cout` 输出 `String`。

> **Software Engineering Observation 18.5**
>
> 当转换构造函数或转换运算符用于执行隐式转换时，C++ 只能应用一次隐式构造函数或运算符函数调用（即一次用户定义转换）来尝试匹配另一个重载运算符的需求。编译器不会通过执行一系列隐式用户定义转换来满足重载运算符的需求。

## 18.13 explicit 构造函数和转换运算符

回想一下，我们将每个可以用一个参数调用的构造函数都声明为 `explicit`。除拷贝构造函数外，任何可以用单个参数调用且未声明为 `explicit` 的构造函数都可由编译器用于执行隐式转换。构造函数的参数被转换为构造函数所在类的对象。转换是自动的，你无需使用转换运算符。在某些情况下，隐式转换是不期望的或容易出错的。例如，我们在图 18.10 中的 `Array` 类定义了一个接受单个 `int` 参数的构造函数。此构造函数的意图是创建包含 `int` 参数指定的元素数量的 `Array` 对象。然而，如果此构造函数未声明为 `explicit`，编译器可能会将其误用以执行隐式转换。

> **Common Programming Error 18.6**
>
> 不幸的是，编译器可能会在你不期望的情况下使用隐式转换，导致产生编译错误或执行时逻辑错误的模糊表达式。

### 意外地将单参数构造函数用作转换构造函数

程序（图 18.12）使用图 18.10–18.11 的 `Array` 类来演示不当的隐式转换。为了允许此隐式转换，我们移除了 `Array.h`（图 18.10）第 14 行中的 `explicit` 关键字。

`main` 中的第 11 行实例化 `Array` 对象 `integers1` 并调用单参数构造函数，使用 `int` 值 7 指定 `Array` 中的元素数量。回想图 18.11，接收 `int` 参数的 `Array` 构造函数将所有 `Array` 元素初始化为 0。第 12 行调用函数 `outputArray`（定义在第 17–21 行），其参数为指向 `Array` 的 `const Array&`。该函数输出其 `Array` 参数中的元素数量和 `Array` 的内容。在此情况下，`Array` 的大小为 7，因此输出七个 0。

第 13 行使用 `int` 值 3 作为参数调用函数 `outputArray`。然而，此程序不包含接受 `int` 参数的名为 `outputArray` 的函数。因此，编译器确定类 `Array` 是否提供可将 `int` 转换为 `Array` 的转换构造函数。由于 `Array` 构造函数接收一个 `int` 参数，编译器假定构造函数是转换构造函数，可用于将参数 3 转换为包含三个元素的临时 `Array` 对象。然后，编译器将临时 `Array` 对象传递给函数 `outputArray` 以输出 `Array` 的内容。因此，即使我们没有显式提供接收 `int` 参数的 `outputArray` 函数，编译器仍能编译第 13 行。输出显示包含 0 的三元素 `Array` 的内容。

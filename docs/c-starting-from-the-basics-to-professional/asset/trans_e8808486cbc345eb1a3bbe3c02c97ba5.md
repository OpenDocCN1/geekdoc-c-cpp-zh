

## 显式模板实参

如果在 Ex10_01.cpp 的 `main()` 中加入以下语句，它将无法编译：

```cpp
std::cout << std::format("Larger of {} and 19.6 is {}\n", small_int,
                         larger(small_int, 19.6));
```

`larger()` 的实参类型不同，而模板中 `larger()` 的参数类型相同。编译器无法创建具有不同参数类型的模板实例。显然，可以将一个实参转换为另一个实参的类型，但必须显式编写代码；编译器不会这样做。可以定义模板允许 `larger()` 的参数为不同类型，但这会带来复杂性，本章后面会讨论：两种类型中用哪一个作为返回类型？现在，我们集中讨论调用函数时如何显式指定模板参数的实参。这样可以控制使用函数的哪个版本。编译器不再推导用于替换 T 的类型；它接受你指定的内容。

可以通过模板的*显式实例化*来解决 `larger()` 使用不同实参类型的问题：

```cpp
std::cout << std::format("Larger of {} and 19.6 is {}\n", small_int,
                         larger<double>(small_int, 19.6));  // Outputs 19.6
```

将函数模板的显式类型实参放在函数名后的尖括号中。这会生成 T 为 double 类型的实例。使用显式模板实参时，编译器完全相信你知道自己在做什么。它会为第一个实参插入到 double 类型的隐式类型转换。即使这可能不是你想要的，它也会提供隐式转换。下面是一个例子：

```cpp
std::cout << std::format("Larger of {} and 19.6 is {}\n", small_int,
                         larger<int>(small_int, 19.6));     // Outputs 19
```

你是在告诉编译器使用 T 为 int 类型的模板实例。这需要将第二个实参隐式转换为 int。转换结果是值 19，在这种情况下这可能并不是你真正想要的。大多数编译器会对这种危险的转换发出警告，尽管并非所有编译器都会。

## 函数模板特化

假设你扩展 Ex10_01.cpp，用指针实参调用 `larger()`：

```cpp
std::cout << std::format("Larger of {} and {} is {}\n", big_int, small_int,
                         *larger(&big_int, &small_int)); // Output may be 10!
```

编译器会实例化该模板，参数类型为 `int*`。这个实例的原型如下：

```cpp
int* larger(int*, int*);
```

返回值是一个地址，必须解引用它才能输出值。然而，结果很可能就是 10，这大概并非本意。原因在于比较的是作为实参传入的地址，而不是这些地址处的值。由于编译器可以随意重新安排局部变量的内存位置，实际结果可能因编译器而异。但考虑到 `small_int` 变量排在第二位，其地址更大并非不可想象。

> **注意**  如果你的编译器将前面的代码片段输出为非 10，可以尝试调整 `big_int` 和 `small_int` 的声明顺序。两个整数值的比较当然不应取决于它们的声明顺序。

原则上，可以定义模板的特化来适配指针类型的模板实参（尽管我们很快会告诉你这很少是个好主意）。对于特定参数值，或者在多参数模板情况下的一组值，模板特化定义了不同于标准模板的行为。模板特化的定义必须出现在原始模板的声明或定义之后。如果把特化放在前面，程序将无法编译。特化还必须出现在其第一次使用之前。

特化的定义以 `template` 关键字开头，但省略参数，因此关键字后的尖括号为空。`larger()` 针对 `int*` 类型的特化定义如下：

```cpp
template <>
int* larger(int* a, int* b)
{
    return *a > *b ? a : b;
}
```

函数体唯一的改动是对实参 a 和 b 解引用，以便比较值而不是地址。要在 Ex10_01.cpp 中使用它，需要将该特化放在模板原型之后、`main()` 之前。

不幸的是，模板特化有一些微妙的缺点。因此，就我们而言，我们把它和 typedef、new/new[]、delete/delete[] 一起列入不推荐使用的语言特性清单：

> **提示**  我们建议你*永远不要*使用函数模板特化。要为特定类型定制函数模板，应改为重载该函数模板，可以使用普通函数或另一个函数模板。下一节将讨论这些选项。一般而言，函数重载的行为比函数模板特化更直观。

## 函数模板与重载

可以通过定义其他同名函数来重载函数模板。这样可以为特定情况定义“覆盖”，而不必求助于模板特化。编译器总是优先使用更具体的重载，而不是更通用模板的实例。和往常一样，每个重载函数必须具有唯一的签名。

让我们重新考虑之前的情况：需要重载 `larger()` 函数以接受指针实参。与其为 `larger()` 使用模板特化，不如直接定义一个重载函数。下面的重载函数原型可以达到目的：

```cpp
int* larger(int* a, int* b); // Function overloading the larger template
```

然后，应使用下面的函数定义来代替特化定义：

```cpp
int* larger(int* a, int* b)
{
    return *a > *b ? a : b;
}
```

甚至可以用另一个专门针对指针类型的模板来重载原始模板：

```cpp
template<typename T>
T* larger(T* a, T* b)
{
    return *a > *b ? a : b;
}
```

注意，这*不是*原始模板的特化，而是第二个不同的模板，只会在指针类型上实例化。如果编译器遇到调用 `larger(x,y)`，其中 x 和 y 是指向同类型值的指针，它将实例化这第二个函数模板；否则，它仍会实例化我们之前的模板。

当然，也可以用另一个生成完全不同签名函数的模板来重载现有模板。例如，可以定义一个模板来重载 Ex10_01.cpp 中的 `larger()` 模板，以查找 vector 中包含的最大值：

```cpp
template <typename T>
const T* larger(const std::vector<T>& data)
{
    const T* result {};            // The largest of an empty vector is nullptr
    for (auto& value : data)
        if (!result || value > *result) result = &value;
    return result;
}
```

参数列表将由此模板生成的函数与原始模板的实例区分开来。

可以扩展 Ex10_01.cpp 来演示这一点。将前面的模板添加到源文件末尾，并在开头添加这些原型：

```cpp
template <typename T> T* larger(T*, T*);
template <typename T> const T* larger(const std::vector<T>& data);
```

然后可以将 `main()` 中的代码改为以下内容：

```cpp
int big_int {17011983}, small_int {10};
std::cout << std::format("larger of {} and {} is {}", 
                         big_int, small_int, larger(big_int, small_int)) << std::endl;
```


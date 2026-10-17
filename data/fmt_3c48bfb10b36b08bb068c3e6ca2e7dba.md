
```cpp
void swapValues(Type_Of_The_Variables &variable1,
    Type_Of_The_Variables& variable2)
{
    Type_Of_The_Variables temp;
    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

正如我们将看到的，这样做是可能的。我们可以定义一个适用于所有类型变量的函数，尽管语法与我们之前展示的有不同。该语法将在下一节中进行描述。

## 函数模板

显示 17.1 展示了一个用于 `swapValues` 函数的 C++ 模板。这个函数模板允许你交换任何两个变量的值，只要这两个变量的类型相同即可。定义和函数声明以以下行开始：

```cpp
template<class T>
```

这通常被称为模板前缀（template prefix），它告诉编译器随后的定义或函数声明是一个模板，且 `T` 是一个类型参数。在这种语文中，`class` 一词实际上的意思是“类型”。¹¹ 正如我们将看到的，类型参数 `T` 可以被任何类型替换，无论该类型是否为类。在函数定义的体内，类型参数 `T` 的用法与任何其他类型一样。

### 函数模板的定义实际上是一系列函数定义的集合。对于显示 17.1 所示的 `swapValues` 模板，实际上对于每一个可能的类型名称都有一个定义。这些定义中的每一个都是通过将类型参数 `T` 替换为类型名称得到的。例如，下面的函数定义是通过将 `T` 替换为类型名称 `double`得到的：

```cpp
void swapValues(double& variable1, double& variable2)
{
    double temp;
    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

另一个 `swapValues` 的定义是通过将函数模板中的参数 `T` 替换为类型名称 `int`得到的。另一个定义是将类型 `T` 替换为 `char`。显示 17.1 所示的函数模板重叠了函数 `swapValues`，因此对于每个可能的类型都有略有不同的函数定义。

编译器不会字面上为函数名 `swapValues` 的每一个可能的类型都生成定义，但它的行为恰好就像生成了所有此类函数一样。对于你使用的每个类型，它都会产生一个独立的定义，但不会为你你使用的任何类型产生定义。无论你使用该模板多少次，对于同一个类型只会生成一个定义。注意在显示 17.1 中调用了两次 `swapValues`：一次参数类型为 `int`，另一次参数为 `char`。

考虑显示 17.1 中的以下调用：

```cpp
swapValues(integer1, integer2);
```

当 C++ 编译器处理此函数调用时，它注意到在这种情况下参数的类型是 `int` —— 于是它使用模板来生成一个将类型参数 `T` 替换为类型名称 `int` 的函数定义。同样，当编译器看到它的调用：

```cpp
swapValues(symbol1, symbol2);
```

> ¹ ANSI 标准规定，你可以在模板前缀中使用关键字 `typename` 代替 `class`。虽然我们同意 `typename` 比使用 `class` 更有意义，但使用 `class` 是一个根深蒂固的传统，为了与大多数程序员和作者保持一致，我们使用了 `class`。

## 显示 17.1 一个演示函数模板的程序

```cpp
//演示函数模板的程序。
#include <iostream>
using namespace std;
// 交换 variable1 和 variable2 的值。
template<class T>
void swapValues(T& variable1, T& variable2)
{
    T temp;
    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
int main() {
    int integer1 = 1, integer2 = 2;
    cout << "Original integer values are " << integer1 << " " << integer2 << endl;
    swapValues(integer1, integer2);
    cout << "Swapped integer values are " << integer1 << " " << integer2 << endl;
    char symbol1 = 'A', symbol2 = 'B';
    cout << "Original character values are " << symbol1 << " " << symbol2 << endl;
    swapValues(symbol1, symbol2);
    cout << "Swapped character values are " << symbol1 << " " << symbol2 << endl;
    return 0;
}
```

输出

```
Original integer values are 1 2
Swapped integer values are 2 1
Original character values are A B
Swapped character values are B A
```

当 C++ 编译器处理此函数调用时，它注意到参数的类型 —— 在情况下是 `int` —— 于是它使用模板生成一个将类型参数 `T` 替换为类型名称 `char` 的函数定义。注意，当你调用用函数模板定义的函数时，不需要进行任何特殊操作；你只需像调用其他函数一样调用它。编译器会完成从函数模板生成函数定义的所有工作。

注意在显示 17.1 中，我们将函数模板放在程序的主体之前，并且没有使用模板函数声明。函数模板可以有函数声明，就像普通函数一样。你可能（也可以不）将函数模板的声明和定义放置在普通函数声明和定义相同的位置。然而，某些编译器并不支持模板函数声明，当它们被支持时，细节可能会变得混乱，并且在不同编译器之间存在差异。你最安全的策略是不使用函数声明，并确保函数定义出现在它被使用的文件中。

我们说，函数模板定义应该出现在与使用它的同一个文件中（那个，即调用该函数的同一个文件）。然而，函数模板定义可以通过 `#include` 指令出现。你可以将函数模板定义放在一个文件中，然后在使用模板的文件中 `#include`。这是最整洁、安全的通用策略。然而，这在某些编译器上可能不起作用。如果不起作用，请咨询当地专家。

虽然我们在代码中不会使用模板函数声明，但为了那些支持使用这些函数声明的读者，我们将描述它们并给出示例。

在显示 17.1 的函数模板中，我们使用字母 `T` 作为类型的参数。这是一种传统，但 C++ 语言强制强制。类型参数可以是任何标识符（关键字除外）。`T` 是类型参数很好的名称，但有时其他名称可能更好。例如，显示 17.1 所示的 `swapValues` 函数模板等同于：

```cpp
template<class VariableType>
void swapValues(VariableType& variable1,
                               VariableType& variable2)
{
    VariableType temp;
    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

### 多个类型参数

可以拥有具有多个类型参数的函数模板。例如，一个具有名为 `T1` 和 `T2` 的两个类型参数的函数模板起始如下：

```cpp
template<class T1, class T2>
```

## 17.1 算法抽象的模板

然而，大多数函数模板只需要一个类型参数。你不能使用未使用的模板模板（template templates）；即每个模板参数都必须在你的模板函数中使用。

### 陷阱 编译复杂性

C++ 不允许你以通常的方式对模板定义进行接口（头文件）和实现文件的分离，因此，你需要将模板定义包含在使用它的代码中。按照惯例，至少函数声明必须在对模板的任何使用之前出现。这是因为当类型未知时，头文件无法正确匹配实现部分。

你最安全的策略是使用模板函数声明，并确保函数定义出现在使用该函数的同一个文件中，且在函数调用之前。不过，函数模板定义可以通过 `#include` 指令出现。你可以在一个文件中给出函数定义，然后在使用该模板函数的文件中 `#include` 该文件。

另一种常用的技术是将你的定义和实现——全部放在头文件中。如果你使用这种技术，那么你将只有一个头文件（.h）而没有实现文件（.cpp）。有时，当所有代码都在头文件中时，会使用 `.hpp` 扩展名。最后，另一种方法是包含你模板类的实现文件（.cpp）而不是头文件（.h）。

某些 C++ 编译器对模板有额外的特殊要求。如果你在编译模板时遇到困难，请检查手册或咨询当地专家。你可能需要设置特殊选项，或者重新调整文件中模板定义与其他项的顺序。

![](img/ca450b03f7ea64419b139be8fdd92a4a_967_0.png)

## 函数模板

函数模板的函数定义和函数声明带有以下内容：

```
template<class Type_Parameter>
```

函数声明（如果使用）和定义与普通函数的声明和定义相同，不同之处 `Type_Parameter` 可以用来代替类型。

例如，这是一个函数模板的函数声明：

```
template<class T>
void showStuff(int stuff1, T stuff2, T stuff3);
```

该函数模板的定义可能如下：

```cpp
template<class T>
void showStuff(int stuff1, T stuff2, T stuff3)
{
    cout << stuff1 << endl;
    << stuff2 << endl;
    << stuff3 << endl;
}
```

示例中给出的函数模板等于为每个可能的类型名称提供一个函数声明和一个函数定义。类型名称替换了类型参数（在上面的示例中为 `T`）。例如，考虑以下函数调用：

`showStuff(2, 3.3, 4.4);`

当执行此函数调用时，编译器将使用将 `T` 替换为类型名称 `double` 后得到的定义。对于你使用的每种不同类型，将产生单独的定义，但对于你没有使用的任何类型则不会。无论你使用模板多少次，对于特定类型只会生成一个定义。

## 自测练习

- 1. 编写一个名为 `maximum` 的模板。该函数接受两个相同的值作为参数，并返回两个参数中较大的一个（如果它们相等，则返回其中一个值）。给出该模板的函数声明和函数定义。你将在定义中使用运算符 `<`。因此，此函数模板仅适用于定义了 `<` 的类型。为函数声明写一个注释来解释这一限制。
- 2. 我们使用了三种类型的绝对值函数：`abs`、`labs` 和 `fabs`。这些函数的区别仅在于参数的类型。最好有一个名为 `absolute` 的绝对值函数模板。该模板将仅适用于定义了 `<` 且定义了一元否定运算符，并且在与该类型的值进行比较时可以使用常量 `0` 的类型。因此，这种函数模板适用于任何类型。给出该模板的函数声明和定义。
- 3. `template<class T>` 适用于哪种类型？
  - a. T 必须是类。
  - b. T 不能是类。
  - c. T 是 C++ 内置的。
  - d. T 可以由程序员定义。

### 抽象

正如我们在讨论中所看到的，使用函数模板意味着我们正在以一种非常通用的方式表达算法。这是 C++ 支持的一项特性。

### 编程示例 通用排序函数

在第17章中我们给出了排序 `int` 类型数组的简单算法。该函数的定义如下：

```cpp
void sort(int a[], int numberUsed)
{
    int indexOfSmallest;
    for (int index = 0; index < numberUsed - 1; index++)
    {
        indexOfSmallest = indexOfsmallest(a, numberUsed);
        swapValues(a[index], a[indexOfSmallest]);
    }
}
```

如果你研究这个 `sort` 的定义，你会发现数组的基类型并没有以任何方式使用。如果我们将高亮的 `int` 替换为 `double`，那么我们就得到了适用于 `double` 类型数组的 `sort` 函数。为了让 `sort` 能够用于 `double` 类型数组，我们只需要替换几次 `int` 类型名称。此外，`double` 类型并没有特殊之处。

## 第17章 / 模板

我们还必须考虑内部调用的辅助函数。这两个辅助函数是 `swapValues` 和 `indexOfsmallest`。

我们已经知道 `swapValues` 可以适用于任何类型，我们将其定义为函数模板。让我们看看 `indexOfsmallest` 是否依赖于所排序数组的基类型。这里重复 `indexOfsmallest` 的定义以便你研究其细节：

```cpp
int indexOfsmallest(const int a[], int startIndex, int numberUsed)
{
    int min = a[startIndex];
    int indexOfMin = startIndex;
    for (int index = startIndex + 1; index < numberUsed; index++)
    {
        if (a[index] < min)
        {
            min = a[index];
            indexOfMin = index;
        }
    }
    return indexOfMin;
}
```

`indexOfsmallest` 函数同样没有以任何重要的方式依赖数组的基类型。如果我们将两个高亮的 `int` 类型实例替换为 `double`，那么我们就得到了适用于 `double` 类型数组的 `indexOfsmallest` 函数。

注意显示 17.2 所示的 `sort` 函数模板可以用于非数字值的数组。在显示 17.3 的演示程序中，调用函数模板 `sort` 来排序字符数组。字符可以使用 `<` 运算符进行比较。虽然

## 17.2 通用排序函数

```cpp
// 这是一个文件 sortfunc.cpp
template<class T>
void swapValues(T& variable1, T& variable2)
<swapValues 的剩余定义见显示 17.1.>
template<class BaseType>
int indexOfSmallest(const BaseType a[], int startIndex, int numberUsed)
{
    BaseType min = a[startIndex];
    int indexOfMin = startIndex;
    for (int index = startIndex + 1; index < numberUsed; index++)
        if (a[index] < min)
        {
            min = a[index];
            indexOfMin = index;
        }
        //min 是 a[startIndex] 到 a[index] 之间的最小值
    return indexOfMin;
}
template<class BaseType>
void sort(BaseType a[], int numberUsed)
{
    int indexOfNextest;
    for (int index = 0; index < numberUsed - 1; index++)
        // 将正确的值放在 a[index] 中
        indexOfNextest = indexOfSmallest(a, numberUsed);
        swapValues(a[index], a[indexOfNextest]);
    // a[0] <= a[1] <= a[i] 是原始数组中最小的
    // 其余元素位于剩余的位置。
}
```

应用于字符值的 `<` 运算符的行为在不同实现之间可能有所不同，但关于字母表字母的某些属性总是成立的。当应用于大写字母时，`<` 运算符测试第一个字母是否在字母顺序上于第二个。同样，当应用于小写字母时，`<` 运算符测试第一个字母是否在字母顺序上于第二个。当你混合使用大写和小写字母时，情况就没那么理想了，但显示 17.3 中的程序只处理大写字母。在程序中，一个

### # 显示 17.3 使用通用排序函数（部分 1/2）

```cpp
// 演示了一个通用排序函数。
#include <iostream>
using namespace std;
// 文件 sortfunc.cpp 定义了以下函数：
//template<class BaseType>
void sort(BaseType a[], int numberUsed)
// 前提条件：numberUsed <= 数组 a 的声明大小。
```



# 类模板 709

显示 16.4 类模板定义（2 部分中的第 2 部分）

```
template<class T>
PairT::Pair(T firstValue, T secondValue)
{
    first = firstValue;
    second = secondValue;
}
```

> 并不是所有的成员函数都显示在这里。

```cpp
template<class T>
void PairT::setFirst(T newValue)
{
    first = newValue;
}
```

```cpp
template<class T>
T Pair<T>::getFirst( ) const
{
    return first;
}
```

# 定义成员函数

类模板成员函数的定义方式与普通类的成员函数相同。唯一的区别在于，成员函数的定义本身也是模板模板。例如，显示 16.4 展示了成员函数 `setFirst` 和 `getFirst` 的适当定义，以及模板类 `Pair` 带有两个参数的构造函数的定义。注意作用域操作符之前的类名是 `PairT` 而不是 `Pair`。然而，作用域操作符之后的构造函数名称是不带 `<T>` 的简单名称 `Pair`。类模板的名称可以用作函数的类型。例如，以下是一个带有整数参数的函数的可能声明：

```cpp
int addUp(const PairInt& thePair);
// 返回 thePair 中两个整数之和。
```

现在我们已经指定了类型——在本例中为 `int`——它用于了类型参数 `T` 的填充。你可以在函数模板中使用类模板。例如，与其在给定的代码中定义特化函数 `addUp`，使得该函数适用于所有类型的数字：

```cpp
template<class T>
T addUp(const Pair<T>& thePair);
// 前置条件：已为类型 T 的值定义了 + 运算符。
// 返回 thePair 中两个值之和。
```

# 作为参数的类模板

# 第 16 章 模板

## 类型参数的限制

几乎所有的模板类定义对哪些类型可以合理地替换为类型参数（或参数）都有某些限制。即使是像 `Pair` 这样简单的模板类，也不能与绝对所有的类型 `T` 良好地工作。除非为类型 `T` 定义了赋值运算符和拷贝构造函数，否则 `Pair<T>` 可能表现不佳，因为赋值运算符在成员函数中使用，并且存在带有 `T` 的值传递参数的成员函数。如果 `T` 涉及指针和动态变量，则 `T` 也应该有一个合适的析构函数。然而，这些要求可能是期望一个行为良好的类 `T` 应该具备的。对于其他模板类，对可以替换类型参数的类型的限制可能更加严格。

# 类模板语法

类模板定义及其成员函数的定义以以下内容为前缀：

```
template<class Type_Parameter>
```

随后，类和成员函数的定义与任何普通类相同，只是 `Type_Parameter` 可以用在类型所在的地方。

例如，以下是类模板定义的开头：

```cpp
template<class T>
class Pair
{
public:
    Pair( );
    Pair(T firstValue, T secondValue);
```

成员函数和重载运算符随后被定义为函数模板。例如，上述示例类模板的双参数构造函数的定义将如下所示：

```cpp
template<class T>
Pair<T>::Pair(T firstValue, T secondValue)
{
  ...
```

你可以通过给类名提供类型参数来特化类模板，如下例所示：

```cpp
Pair<int>
```

特化的类名（如 `Pair<int>`）随后可以像任何类名一样使用。它可以用于声明对象或指定形式参数的类型。

# 类模板

# 类型定义

你可以定义一个新的类类型名称，其含义与特化的类模板相同，例如 `Pair<int>`。定义类类型的语法如下：

```cpp
typedef Class_Name<Type_Argument> New_Type_Name;
```

例如，

```cpp
typedef Pair<int> PairOfInt;
```

`PairOfInt` 可以用于声明 `Pair<int>` 类型的对象：

```cpp
PairOfInt pair1, pair2;
```

`PairOfInt` 的名称也可以在任何需要类型的地方使用。

# 自测题

- 9. 给出类模板默认（无参数）构造函数的定义，显示 16.4。
- 10. 给出以下函数的完整定义，如文所示：

```cpp
int addUp(const PairInt& thePair);
// 返回 thePair 中两个整数之和。
```

- 11. 给出以下函数的完整定义，如文所示：

```cpp
template<class T>
T addUp(const Pair<T>& thePair);
// 前置条件：已为类型 T 的值定义了 + 运算符。
// 返回 thePair 中两个值之和。
```

# 第 16 章 模板

# 示例：模板类

在第 10 章中，我们定义了类型 `T` 的填充数组类。在本例中，模板类 `PArray` 是任意类型的填充数组。其成员函数定义显示 16.5。注意我们将模板放在命名空间中，正如使用简单模板一样。我们将类模板、实现和应用程序分到三个文件中。不幸的是，这些文件不能单独编译。因此，我们可以在应用程序文件中包含接口和实现。

# 显示 16.5 PArray 类的接口（2 部分中的第 1 部分）

```cpp
// 这是头文件 pfray.h。这是 PArray 类的接口。
// 此类型的对象是填充数组。
#ifndef PARRAY_H
#define PARRAY_H

namespace PArraySavitch
{
    template<class T>
    class PArray{
        public:
            PArray(); // 初始化容量为 50。

            PArray(int capacityValue);

            PArray(const PArray<T>& pObject);

            void addElement(const T element);
// 前置条件：数组未满。
                // 后置条件：元素已添加。
```

# 显示 16.5 PArray 类的接口（2 部分中的第 2 部分）

```cpp
bool full() const; // 如果数组已满则返回 true；
// 否则返回 false。

int getCapacity() const;

int getNumberUsed() const;

void emptyArray();
// 将使用数量重置为零，从而清空数组。

T& operator[](int index);
// 读取和更改 0 到 numberUsed - 1 的元素。

PFArray<T>& operator=(const PFArray<T>& rightSide);

virtual ~PFArray();
private:
    T *;//用于指向 T 的数组。
    int capacity;//用于数组的大小。
    int used;//用于当前使用的数组位置数量。
};
PFArraySavitch
#endif //PFRAY_H
```

# 显示 16.6 PFArray 类的实现（3 部分中的第 1 部分）

```cpp
// 这是实现文件 pfray.cpp。
// 这是 PFArray 模板类的实现。
// 模板类的接口在文件 pfray.h 中。

#include "pfray.h"
#include <iostream>
using std::cout;

namespace PFArraySavitch
{
    template <class T>
    PFArray<T>::PFArray() :capacity(50), used(0)
{
        a = new T[capacity];
}
```

> 注意在作用域解析符之前使用了 T，但在构造函数名称中没有使用 T。

(继续)



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

`indexOfSmallest`函数也没有在很大程度上依赖于数组的基类型。如果我们把两个高亮的`int`类型实例替换为`double`类型，那么我们就更改了`indexOfSmallest`函数，使其适用于基类型为`double`的数组。

为了更改`sort`函数使其能够排序基类型为`double`的数组，我们只需要将几个类型名`int`实例替换为类型名`double`即可。此外，`double`类型并没有特殊之处。我们可以对其他类型进行类似的替换。我们需要知道的是该类型是否定义了`<`运算符。这是函数模板的完美用例。如果我们将`sort`函数和`indexOfSmallest`函数中的几个类型名`int`实例替换为类型参数，那么`sort`函数就可以对任何类型的数值数组进行排序，前提是该类型的值可以使用`<`运算符进行比较。在显示 17.2 中，我们编写了这样一个函数模板。

请注意，显示 17.2 所示的函数模板可以用于非数字数值数组。在显示 17.3 的演示程序中，调用了`sort`函数来对字符数组进行排序。字符可以使用`<`运算符进行比较。虽然应用于字符值的精确`<`运算符在不同实现之间可能有所不同，但在它如何排列字母表字母方面，某些规律总是成立的。当应用于大写字母时，`<`测试第一个在字母顺序上是否在第二个之前。同样，当应用于小写字母时，`<`测试第一个在字母顺序上是否在第二个之前。当你混合使用大写和小写字母时，情况就没那么良好了，但显示 17.3 所示程序只处理大写字母。在该程序中，一个...

## 17.1 算法抽象的模板

### 显示 17.2 通用排序函数

```cpp
// 1 //This is a file sortunc.cpp

template<class T>
void swapValues(T& variable1, T& variable2) {
    // <The rest of the definition of swapValues is given in Display 17.1.>
}

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
    } //min is the smallest of a[startIndex] through a[index]
  return indexOfMin;
}

template<class BaseType>
void sort(BaseType a[], int numberUsed)
{
  int indexOfNextSmallest;
  for (int index = 0; index < numberUsed - 1; index++)
    //Place the correct value in a[index]:
    indexOfNextSmallest = indexOfSmallest(a, index, numberUsed);
    swapValues(a[index], a[indexOfNextSmallest]);
    //a[0] <= a[1]<= a[index] are the smallest of the original array
    //elements. The rest of the elements are in the remaining positions.
```

## 第 17 章 模板

### 显示 17.3 使用通用排序（部分1/2）

```cpp
//Demonstrates a generic sorting function.
#include <iostream>
using namespace std;
//The file sortfunc.cpp defines the following function:
template<class BaseType>
void sort(BaseType a[], int numberUsed);
//Precondition: numberUsed <= declared size of the array.
//The array elements a[0] through a[numberUsed-1] have values.
//Postcondition: The values of a[0] through a[numberUsed-1] are
//arranged so that a[0] <= a[1] <= ... <= a[numberUsed-1].
#include "sortfunc.cpp"
int main() {
    int i;
    int a[10] = {9, 8, 7, 6, 5, 1, 2, 3, 0, 4};
    cout << "Unsorted integers:\n";
    for (i = 0; i < 10; i++)
        cout << a[i] << " ";
    cout << endl;
    sort(a, 10);
    cout << "In sorted order the integers:\n";
    for (i = 0; i < 10; i++)
        cout << a[i] << " ";
    cout << endl;
    double b[5] = {5.5, 4.4, 1.1, 3.3, 2.2};
    cout << "Unsorted doubles:\n";
    for (i = 0; i < 5; i++)
        cout << b[i] << " ";
    cout << endl;
    sort(b, 5);
    cout << "In sorted order the doubles:\n";
    for (i = 0; i < 5; i++)
        cout << b[i] << " ";
    cout << endl;
    char c[7] = {'G', 'E', 'N', 'E', 'R', 'I', 'C'};
    cout << "Unsorted characters:\n";
    for (i = 0; i < 7; i++)
        cout << c[i] << " ";
    cout << endl;
    sort(c, 7);
    cout << "In sorted order the characters:\n";
    for (i = 0; i < 7; i++)
        cout << c[i] << " ";
    cout << endl;
    return 0;
}
```

应用于字符值的`<`运算符在不同实现之间可能有所不同，但在它如何排列字母表字母方面，某些规律总是成立的。当应用于大写字母时，`<`测试第一个在字母顺序上是否在第二个之前。同样，当应用于小写字母时，`<`测试第一个在字母顺序上是否在第二个之前。当你混合使用大写和小写字母时，情况就没那么良好了，但显示 17.3 所示程序...

## 编程提示 如何定义模板

我们在显示 17.2 中定义函数模板时，是从`int`元素的数组开始的。我们通过将数组的基类型替换为参数来创建一个模板。这是编写模板良好的通用策略。如果你想写一个函数模板，首先写一个完全不是模板的普通函数版本。完全调试该普通函数，然后通过将一些类型名替换为类型参数来将其转换为模板。这种方法有两个优点：首先，当你定义函数时，处理的是一个更具体的案例，这使得问题更容易可视化。其次，你在每个阶段需要检查的细节更少；当你担心算法本身时，不需要考虑模板语法规则。

## 陷阱 使用不当类型使用模板

如果函数定义中的代码符合逻辑，你可以使用任何类型使用模板。然而，模板中的所有代码必须符合逻辑并以恰当的方式运行。例如，你不能使用`swapValues`模板（显示 17.1），并将类型参数替换为赋值运算符完全不起作用或无法“正确”作用的类型。

作为一个更具体的例子，假设你的程序按照显示 17.1 定义了`swapValues`函数。你不能在程序中添加以下内容：

```cpp
int a[10], b[10];
<some code to fill arrays>
swapValues(a, b);
```

这段代码将不起，因为赋值不适用于数组类型。

### 自测题

- 5. 显示 17.10 显示了一个名为`search`的函数，它在数组中搜索指定的整数。给出一个`search`的函数模板版本，用于搜索任何类型元素的数组。给出该模板的函数声明和函数定义。（提示：它与显示 17.10 中给出的函数几乎相同）。
- 6. 在第 4 章的练习程序 8 中，你被要求重载`abs`函数，使`abs`名称能够适用于当时已学习的几种内置类型。在自测题 2 中，将函数重载与为此目的使用模板进行对比分析。

> 本陷阱部分中的示例使用了数组。如果你还没有学习数组（第 7 章），应该跳过此陷阱部分并在学习数组后返回。

## 17.2 数据抽象的模板

文化的财富平等与机会平等……仅仅使我们都成为了同一个阶级的成员。

爱德华·贝拉米，《回望过去：2000–1887》

正如你在上一节中看到的，通过使用模板可以使函数定义更具通用性。在本节，你将看到模板也可以让类定义更加通用。

## 类模板的语法

类模板的语法基本上与函数模板相同。在模板定义之前，需要放置以下内容：

```
template<class T>
```

类型参数`T`在类定义中的用法与其他任何类型都相同。与函数模板一样，类型参数`T`代表一个可以是任何类型的类型；类型参数不必被替换为类类型。与函数模板一样，你可以使用任何（非关键字）标识符来代替`T`。

例如，以下是一个类模板。该类的对象包含类型为`T`的两个值对；如果`T`是`int`，则对象值是整数对；如果`T`是`char`，则对象值是字符对，依此类推。

```
// 用于类型 T 值对的类：
class Pair
{
public:
    Pair();
    Pair(T firstValue, T secondValue);
    void setElement(int position, T value);
    // 前置条件：position 为 1 或 2。
    // 后置条件：
    // 所指定的位置已设置为 value。
    T getElement(int position) const;
    // 前置条件：position 为 1 或 2。
    // 返回所指定位置的值。
private:
    T first;
    T second;
};
```

一旦定义了类模板，你就可以声明该类的对象。声明必须指定要为`T`填充什么类型。例如，以下代码声明了对象`score`以记录一对整数，并声明了对象`seats`以记录一对字符：

```
Pair<int> score;
Pair<char> seats;
```

然后这些对象的使用方法就像使用任何其他对象一样。例如，以下代码将第一个队伍的分数设置为 3，第二个队伍的分数设置为 0：

```
score.setElement(1, 3);
score.setElement(2, 0);
```

类模板的成员函数定义方式与普通类的成员函数相同。唯一的区别是，成员函数的定义本身是模板。例如，以下是成员函数`createElement`以及带有两个参数的构造函数的适当定义：

```
// 使用 iostream 和 cstdlib
template<class T>::createElement(int position, T value)
{
    if (position == 1)
        first = value;
    else if (position == 2)
        second = value;
    else
    {
        cout << "Error: Illegal pair position.\n";
        exit(1);
    }
```

```
template<class T>
Pair<T>::Pair(T firstValue, T secondValue)
    : first(firstValue), second(secondValue)
{ // 函数体特意为空。
}
```

注意，在作用域解析符之前的类名是`Pair<T>`，而不仅仅是`Pair`。

类模板的名字可以作为函数参数的类型。例如，以下是一个带有整数对参数的函数的可能声明：

```
int addUp(const Pair<int>& thePair);
// 返回 thePair 中两个整数之和。
```

## 定义成员函数

## 类模板语法

类定义以及成员函数的定义前面带有以下内容：

```
template<class Type_Parameter>
```

类定义和成员函数的定义与任何普通类相同，不同之处`Type_Parameter`可以用来替换类型。

例如，以下是一个类模板定义的开头：

```
template<class T>
class Pair
{
public:
    Pair();
    Pair(T firstName, T secondValue);
    void setElement(int position, T value);
```

随后，成员函数和重载运算符被定义为函数模板。例如，上述示例类模板中函数定义可以如下如下开始：

```
template<class T>
void Pair<T>::setElement(int position, T value)
{
```

注意，我们指定了要为类型参数`T`填充的类型，在本例中为`int`。

你可以在函数模板中使用类模板。例如，与其定义上面那个特化的函数`addUp`，不如定义如下所示的函数模板，以便该函数适用于所有类型的数字：

```
template<class T>
T addUp(const T& a, const T& n) // 前置条件：类型 T 的值定义了运算符 +。
// 返回 thePair 中两个值之和。
```

## 类型定义

你可以通过为类名提供类型参数来特化类模板，在下面的示例中：

```
Pair<int>
```

特化后的类名（如`Pair<int>`）可以像任何类名一样被使用。它可以用于声明对象或指定形式参数的类型。

你可以定义一个与特化类模板名具有相同含义的新类名，例如`Pair<int>`。此类定义类名的语法如下：

```
typedef Class_Name<Type_Argument> New_Type_Name;
```

例如：

```
typedef Pair<int> PairOfInt;
```

`PairOfInt`名称可以用于声明`Pair<int>`类型的对象，如下所示：

```
PairOfInt pair1, pair2;
```

`PairOfInt`还可以用于形式参数的类型。

## 编程示例 数组类

17.4 包含一个对象为列表的类的接口。由于该类定义是一个类模板，因此列表可以是任何类型的列表。你可以拥有`int`类型的值对象、`double`类型的值列表，或者`string`类型对象的列表。

17.5 包含一个使用该类模板的演示程序。虽然这个程序并没有做什么，但它说明了如何使用类模板。一旦你理解了细节，就可以在任何需要列表的地方类模板。17.6 给出了类的实现。

注意我们重载了插入运算符`<<`以输出`GenericList`对象。为了实现这一点，我们将运算符`<<`为类的元。为了有一个与类相同的类型，我们在参数处使用了`GenericList<ItemType>`。当类型参数替换为`int`时，该列表将是`GenericList<int>`。

此外注意重载插入运算符`<<`的实现放在头文件中而不是实现文件中。这看起来可能很奇怪，但在模板中使用友元函数或运算符时非常常见。虽然我们将`<<`定义为类的成员，但请记住友元实际上存在于类之外并属于命名空间。当从其他文件包含类时，编译器可以轻松地找到`<<`的实现。

## 显示 17.4 类模板 GenericList 的接口（部分 1/2）

```
// 是头文件 genericlist.h。这是 GenericList 的接口。
// GenericList 类型的对象是任何定义了运算符 << 和 的类型的列表。
// 一个列表上的所有项必须是相同类型。一个可以容纳最多 max 个 Type_Name 类型项的列表声明如下：
// GenericList<Type_Name> the_object(max);
#ifndef GENERICLIST_H
#define GENERICLIST_H
#include <iostream>
using namespace std
{
    template<class ItemType>

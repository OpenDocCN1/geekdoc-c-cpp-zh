

## 图 C2-7 两个指针引用（指向）同一个对象

![](img/288a0c22d14d2450c1e772f228f867b0_154_0.png)

这里我们尝试通过在删除 myBoxPtr 指向的对象后将其设置为 nullptr 来实践安全可靠的编程。但是调用 yourBoxPtr->getItem() 会导致程序中止。发生了什么？图 C2-8 显示了此调用之前的内存状态。如您所见，myBoxPtr 指向的对象已被删除，正如它应该做的那样。问题出在 yourBoxPtr 仍然引用自由存储中对象的位置，尽管该对象不再存在。由于该对象不再存在，yourBoxPtr 是一个悬空指针，当我们尝试在该对象上调用方法时，程序会中止。

## 图 C2-8 悬空指针示例

![](img/288a0c22d14d2450c1e772f228f867b0_154_1.png)

## 编程提示：如何避免悬空指针

- 将指针变量初始设置为 nullptr，或在不再需要它们时设置为 nullptr。如果类有一个指针变量作为数据字段，构造函数应始终初始化该数据字段，使其指向一个对象或 nullptr。清单 C2-3 中的类 GoodMemory 演示了这一保障措施。
- 在使用指针变量调用方法之前，测试它是否包含 nullptr。
- 尽量减少程序中别名的使用。如您将看到，在某些情况下，这并不总是可能或可取的。
- 在确定没有其他别名需要使用它之前，不要删除自由存储中的对象。
- 删除对象时，将引用该已删除对象的所有别名设置为 nullptr。

## C2.4 虚方法和多态

现在我们已经掌握了指针的一些基础知识，可以深入多态的实现。为了允许编译器执行多态所需的后期绑定，必须将基类中的方法声明为虚方法。在 C++ 间奏 1 中，我们开始讨论虚方法——即使用关键字 virtual 表示它们可以被重写的方法。在第 C2.2 节的示例中，PlainBox 是基类，我们在 C++ 间奏 1 的清单 C1-3 中定义了它。当时编写的代码没有按我们期望的方式运行。为纠正该问题，我们必须将 PlainBox 中希望其他类重写的方法声明为虚方法，如清单 C2-4 所示。请注意，只需修订基类（PlainBox）的头文件。将方法 setItem 和 getItem 声明为虚方法，使得方法代码可以进行后期绑定。

```
LISTING C2-4 Revised header file for the class PlainBox
/** @file PlainBox.h */
#ifndef _PLAIN_BOX
#define _PLAIN_BOX
template<class ItemType> // Indicates this is a template
// Declaration for the class PlainBox
class PlainBox
{
private:
// Data field
ItemType item;
public:
// Default constructor
PlainBox();
// Parameterized constructor
PlainBox(const ItemType& theItem);
// Mutator method that can change the value of the data field
virtual void setItem(const ItemType& theItem);
// Accessor method to get the value of the data field
virtual ItemType getItem() const;
}; // End PlainBox
#include "PlainBox.cpp" // Include the implementation file
#endif
```

为了完全实现后期绑定，我们必须在自由存储中创建变量，并使用指针引用它们。因此，我们还必须将第 C2.2 节中第一个早期绑定示例的代码更改为

```cpp
string specialItem = "Riches beyond compare!";
string otherItem = "Hammer";

PlainBox<string>* myPlainBoxPtr = new PlainBox<string>();
placeInBox(myPlainBoxPtr, specialItem);

MagicBox<string>* myMagicBoxPtr = new MagicBox<string>();
placeInBox(myMagicBoxPtr, otherItem);

cout << myMagicBoxPtr->getItem() << endl;
```

后期绑定示例

接下来，我们必须修改函数 placeInBox 以接受指向 PlainBox<string> 对象的指针：

```cpp
void placeInBox(PlainBox<string>* theBox, string theItem)
{
 theBox->setItem(theItem);
} // end placeInBox
```

最后的更改是通过向程序添加以下语句来释放自由存储中变量所使用的内存：

```cpp
delete myPlainBoxPtr;
myPlainBoxPtr = nullptr;
delete myMagicBoxPtr;
myMagicBoxPtr = nullptr;
```

我们的函数 placeInBox 现在将根据其第一个参数所指向的盒子类型调用正确版本的 setItem。

使用虚方法对类的未来使用有重大影响。假设您在编写派生类 MagicBox 之前已经编译了类 PlainBox 及其实现。如果您随后编写 MagicBox，假设可以访问已编译的类 PlainBox，您可以重写 getItem，因为它在 PlainBox 中是虚方法。结果，您将更改 MagicBox 实例的 getItem 行为，尽管 PlainBox 已经编译。也就是说，定义虚方法的类是可扩展的。您可以在不访问祖先源语句的情况下，为派生类添加功能。

## 注：关于虚方法的要点

- 虚方法是派生类可以重写的方法。
- 必须实现类的虚方法。（纯虚方法不包括在此要求中。）
- 派生类不必重写继承的虚方法的现有实现。
- 类的任何方法都可以是虚方法。但是，如果您不希望派生类重写特定方法，则该方法不应是虚方法。
- 构造函数不能是虚函数。
- 析构函数可以且应该是虚函数。虚析构函数确保对象的未来后代可以正确地自行释放内存。
- 虚方法的返回类型不能被重写。

## C2.5 数组的动态分配

在 C++ 中声明数组时，使用诸如下面的语句

```cpp
const int MAX_SIZE = 50;
double myArray[MAX_SIZE];
```

普通 C++ 数组是静态分配的

编译器为数组预留特定数量（在此例中为 MAX_SIZE）的内存单元。此内存分配在程序执行之前发生，因此无法等到执行时才为 MAX_SIZE 赋值。我们已经讨论了当程序有超过 MAX_SIZE 个项要放入数组时，这种固定大小的数据结构所造成的问题。

您刚刚学习了如何使用 new 运算符动态分配内存——即在程序执行期间。尽管第 C2.3 节向您展示了如何为单个变量或对象分配内存，但您实际上可以一次为许多变量分配内存。如果您编写

使用 new 运算符动态分配数组

```cpp
int arraySize = 50;
double* anArray = new double[arraySize];
```

指针变量 anArray 将指向包含 50 个项的数组中的第一个项。与 MAX_SIZE 不同，arraySize 可以在程序执行期间更改。您可以在执行时为 arraySize 赋值，从而确定数组的大小。这很好，但您如何使用这个数组？

无论您如何分配数组——像第一个示例那样静态分配，或像第二个示例那样动态分配——都可以使用索引和熟悉的数组表示法来访问其元素。例如，anArray[0] 和 anArray[1] 是数组 anArray 中的前两个项。

当您动态分配数组时，在不再需要它们时，需要将其内存单元返回给系统。如前所述，您使用 delete 运算符执行此任务。要释放数组 anArray，您编写

```cpp
delete[] anArray;
```

delete 将动态分配的数组返回给系统以供重用

请注意，在对数组应用 delete 时，需要包含方括号。

现在假设您的程序使用了数组 anArray 的所有内容，尽管其大小是在执行期间选择的。您可以分配一个新的更大的数组，将旧数组复制到新数组中，最后释放旧数组。每次数组填满时将其大小加倍是一种合理的方法。以下语句将 anArray 的大小加倍：

```cpp
double* oldArray = anArray; // Copy pointer to array
anArray = new double[2 * arraySize]; // Double array size
for (int index = 0; index < arraySize; index++) // Copy old array
    anArray[index] = oldArray[index];
delete[] oldArray; // Deallocate old array
```

您可以增加动态分配数组的大小

本书后续讨论将同时涉及静态分配和动态分配的数组。我们的基于数组的 ADT 实现将出于简单性考虑使用静态分配的数组。编程问题将要求您创建使用动态分配数组的基于数组的实现。我们将此类数组称为可调整大小的数组。

### 2.5.1 基于可调整大小数组的袋子

我们可以使用可调整大小的数组来实现 ADT 袋子，使袋子永远不会填满——当然，这是在特定计算机的范围内。如果我们查看第 3 章清单 3-1 中给出的类 ArrayBag 的头文件，以及各种方法的实现，我们会发现只需更改 add 方法。当数组——因此也是袋子——填满时，add 可以加倍数组的容量，而不是无法添加项并返回 false。修订后的方法如下。由于袋子永远不会填满，此版本的 add 方法始终可以返回 true。

```cpp
template<class ItemType>
bool ArrayBag<ItemType>::add(const ItemType& newEntry)
{
   bool hasRoomToAdd = (itemCount < maxItems);
   if (hasRoomToAdd)
   {
      ItemType* oldArray = items;
```


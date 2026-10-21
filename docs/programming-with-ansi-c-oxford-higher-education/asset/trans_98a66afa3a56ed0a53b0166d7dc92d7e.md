

- 2. 规则 1 的一个推论是，不能存在名称不同但参数相同的多个构造函数。如果需要多个构造函数，应该只有一个构造函数，并用不同的参数集对其进行重载。

- 3. 构造函数不能指定返回类型。即使写 void 也不允许（尽管构造函数在构造后总是返回其所属类的对象）。

> 尽管构造函数不能指定返回类型，但它们总是返回其所属类的对象。

- 4. 构造函数的函数体中不应有 return 语句。

- 5. 不能获取构造函数的地址。因此，不能有指向构造函数的函数指针。

- 6. 构造函数可以定义为 private，但这样就无法使用这些构造函数定义对象。这是因为将构造函数定义为 private 会在对象定义时尝试由对象执行一个私有函数，而这是不允许的。因此，除非对象的正常定义不受限制，否则构造函数应定义为 public。

## 5.5 默认构造函数

默认构造函数是没有参数或全部参数都有默认值，即参数列表为空或所有参数都有默认值（因此构造函数可以在不带任何参数的情况下被调用）的构造函数。默认构造函数有两种不同类型。当用户未定义任何构造函数时，是编译器提供的默认构造函数，而当用户提供一个时，是用户定义的。编译器定义的默认构造函数并非在所有情况下都会由编译器合成，只有在默认构造函数必要时才会合成。用户可以在他/她希望时指定默认构造函数。通常，当用户提供构造函数时，编译器不会提供一个。

### 5.5.1 编译器定义的默认构造函数

假设定义了某个类的几个对象，但未为它们定义构造函数。当该对象被定义时会发生什么？例如，当语句

```
student CaptainStudent;
```

执行时，实际发生了什么？

在这种情况下，会为存储完整的 CaptainStudent 分配足够的内存并命名为‘CaptainStudent’。如果稍后引用 CaptainStudent，将获取该地址的内容。

当程序员未提供构造函数时，C++ 会通过在某些非平凡情况下合成物理构造函数代码来提供相同的效果。如果只需要为对象进行内存分配，则提供效果但不合成物理构造函数代码。了解何时需要构造函数的物理编码会很有趣，但这超出了入门书籍的范围。读者可参考 Stanly Lippman 的经典著作 Inside the C++ Object Model 中的描述。为了简化，我们假设提供了构造函数，并且我们具有对象构造的效果

> 当用户未定义任何构造函数时，编译器提供默认构造函数。

该 C++ 构造函数使我们能够在程序后面通过构造该对象来使用对象 CaptainStudent。此类不带任何参数的构造函数形式被称为默认构造函数。

> 注 物理构造函数并非总是由编译器合成。然而，在少数非平凡情况下，操作需要此类合成。

### 5.5.2 用户定义的默认构造函数

编译器合成的默认构造函数无法完成类所需的所有初始化。合成的构造函数只满足编译器的要求。即使物理构造函数未被合成，编译器也只提供适合其自身要求的效果，而非用户的需求。因此，内存分配由编译器提供，但初始化不提供。当我们定义 CaptainStudent 时，我们期望有足够大小的内存来容纳该对象，并希望使用它（通过存储 CaptainStudent 成员的信息并对其进行操作）。编译器将使用此构造函数提供该内存。然而，编译器不需要初始化，因此默认构造函数不提供它。初始化是程序员的责任，应显式完成。考虑一个链表的节点类的例子。

```
class node
{
    int Value;
    int *PtrNextValue; // Other items needed for node
}
```

在这种情况下，假设节点的使用如下：

```
node First;
// checking for empty list
if(First.PtrNextValue)
/* Wrong! The pointer is not initialized to null */
{
    // Necessary action
}
```

这里，考虑语句

```
node First;
```

根据情况，编译器可能会为我们定义默认构造函数。然而，在这种情况下它只提供内存分配以存储类型为 node 的对象（并且没有物理构造函数被构造）。它当然不会为我们初始化 Value 或 PtrNextValue。这是由程序员的工作，如果需要初始化，构造函数必须写成如下：

> 编译器提供适合其自身要求而非用户的补充。

```
class node
{
    int Value;
    int *PtrNextValue;
public:
node()
```

```
int ItemNo;
string ItemName;
public:
    Item()    // Default constructor
    {
        ItemNo = 0;
        ItemName = "";
        /* This is not required as String object is initialized already by the constructor provided in string class */
    }

    void SetDetails(int TempItemNo, string TempItemName)
    {
        ItemNo = TempItemNo;
        ItemName = TempItemName;
    }

    void ShowDetails()
    {
        cout << "\n Item number is" << ItemNo;
        cout << "\n Item name is" << ItemName;
    }
};

class ItemCollection
{
    Item ItemArray[20];
    int ItemIndex;
public:
    ItemCollection()      // Default constructor
    /* If we remove this default constructor, it will not affect the program */
    {
        for(int i=0; i<20; i++)
        ItemArray[i].SetDetails(0, "");
        ItemIndex = 0;
    }

    void SetDetails(Item TempItemArray[])
    {
        for(int i=0; i<20; i++)
        ItemArray[i] = TempItemArray[i];
    }

    void PrintDetails()
    {
        for(int i=0; i<20; i++)
        ItemArray[i].ShowDetails();
    }
};

int main()
{
    ItemCollection IC;
    Item TempItemArray[20];
    for(int i=0; i<20; i++)
    {
        TempItemArray[i].SetDetails(i, "Dummy");
    }
    IC.SetDetails(TempItemArray); IC.PrintDetails();
}
```

鼓励读者尝试以下操作。获取程序的输出。删除 ItemCollection 类的默认构造函数并再次获取输出。观察差异。

输出没有变化。这是因为默认构造函数初始化为零和 " " 是多余的。这只是良好的编程实践进行初始化，以便如果后来忘记为其赋值，将会得到值零和 " " 并意识到错误。当未提供构造函数时，这些值不会被初始化。只要为两者提供合理的值，就不会有任何麻烦，也不会产生重大问题。

ItemCollection 默认构造函数无论如何都是多余的，因为 Item 构造函数已经在初始化 Items。

## 必须存在默认构造函数的情形

有时，初始化非常重要，并且计数从那里开始。因此，如果未提供默认构造函数，计数器将未初始化，这将导致执行不正确。

程序 5.2 是一个用户定义默认构造函数必须存在的例子。

## 程序 5.2 有用的默认构造函数

```
//DefaultConstructor.cpp
#include <iostream>
#include <string>
using namespace std;

class Item
{
    int ItemNo;
    string ItemName;
public:
    Item()      // Default constructor
    {
        ItemNo = 0;
        ItemName = "";
        /* This is redundant as the string constructor must have done this already */
    }

    void SetDetails(int TempItemNo, string TempItemName)
    {
        ItemNo = TempItemNo;
        ItemName = TempItemName;
    }

    void ShowDetails()
    {
        cout << "\n Item number is" << ItemNo;
        cout << "\n Item name is" << ItemName;
    }
};

class ItemCollection
{
    Item ItemArray[20];
    int ItemIndex;
public:
    ItemCollection() // Default constructor
    {


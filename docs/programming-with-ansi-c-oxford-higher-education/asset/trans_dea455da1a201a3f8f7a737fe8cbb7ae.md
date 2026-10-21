

```cpp
/* The following for loop is not required. This will actually be added by the compiler when the array is defined by the class in the first line (Item ItemArray[20];) by calling the Item() constructor. */
for(int i=0; i<20; i++)
    ItemArray[i].SetDetails(0, "");

// The following is important
ItemIndex = 0;
}

/* This default constructor is needed as ItemIndex is initialized here and afterwards incremented. Other parts of the constructor are redundant and can be removed. */

void PrintDetails()
{
    for(int i=0; i<ItemIndex; i++)
        ItemArray[i].ShowDetails();
}

void InsertItem(int TempItemNo, string TempItemName)
{
    ItemArray[ItemIndex].SetDetails(TempItemNo, TempItemName);
    ItemIndex++;
    /* This statement flags an error in the absence of a default constructor */
};
int main()
{
    ItemCollection IC;
    IC.InsertItem(105,"Pentium 4 processor"); IC.InsertItem(111,"Seagate HDD");
    IC.InsertItem(122,"Samsung monitor"); IC.InsertItem(220,"Creative sound card");
    IC.PrintDetails();
}
```

### 程序的工作原理

程序 5.1 和 5.2 有两个不同的类；一个是 Item，另一个是 ItemCollection，其中包含一个项目数组。两者都定义了默认构造函数。让我们忽略 Item 的默认构造函数，只考虑第二种情况下的 ItemCollection，因为这里很重要。程序 5.1 包含使用数组一次性向完整项目集插入值的函数。程序 5.2 逐个插入项目。程序 5.1 中的默认构造函数将项目编号初始化为零，名称初始化为空字符串，并将 ItemIndex 初始化为零。如果删除此默认构造函数，对程序没有影响，程序将照常执行。

然而，在程序 5.2 中，将 ItemIndex 初始化为零是一个重要步骤。如果删除默认构造函数，程序将无法正常运行，因为函数 InsertItem() 和 PrintDetails() 依赖于该值。每次调用 InsertItem() 时，ItemIndex 都会递增。当函数首次被调用时，它必须从零开始递增。如果未初始化为零，InsertItem() 会将项目插入由 ItemIndex 值表示的随机位置。

也可以定义除默认构造函数之外的其他构造函数。让我们详细讨论这一点。

## 5.6 带一个参数的构造函数

单参数构造函数是一种特殊的构造函数类型，因为它实际上定义了两个操作而不是一个。程序 5.3 说明了这一概念。类 brother 有一个单一的数据成员，即表示兄弟姓名的字符串。在这里，引入了一个单参数构造函数。当传递包含兄弟姓名的字符串时，它会构造一个 brother 类型的对象。

### 程序 5.3 单参数构造函数

```cpp
//SingleArgCons.cpp
#include <iostream>
#include <string>
using namespace std;

class brother
{
    string Name;
public:
    brother(string BrotherName)
    {
        Name = BrotherName;
    }
};

void main()
{
    int j(5);  /* int j = 5 is its shorthand notation */
    int i = int(5);
    double f(3.4);  /* Equivalent of double f = 3.4 */
    brother FirstBrother = brother("Steve Waugh");
    brother SecondBrother("Mark Waugh");
    brother ThirdBrother("Gilchrist");
    brother FourthBrother = "Ricky Ponting";
}
```

### 程序的工作原理

这个程序非常简单易懂。给 brother 构造函数一个参数，它就会构造一个 brother 类型的对象。

值得注意的一个有趣点是，在定义对象时调用构造函数的可能方式。应注意，int i = 5; 被编译器理解为 int i(5); 这意味着编译器获取可以容纳 int 的内存，将值 5 赋给它，然后将其分配给 i；语句 int i = int(5); 也是初始化的一种情况。由 i 引用的对象由编译器创建的临时对象初始化。此临时对象在 int(5) 从 5 初始化时更早创建。

可以观察到，相同的简写表示法也适用于用户定义的对象。

```
brother FirstBrother = brother("Steve Waugh");
(explicit call to brother function; i.e., the constructor)
brother SecondBrother("Mark Waugh");
brother FourthBrother = "Ricky Ponting";
```

这里，第二条语句类似于第三条。在所有三种情况下，编译器都会调用用户定义的构造函数函数（此处类中定义的 brother 函数）并用它构造并初始化正在定义的对象。不过也有区别。第一种情况显式调用构造函数函数，而另外两种情况是自动（隐式）调用的。也有技术上的区别。第一种情况有临时对象的开销，而另外两种情况没有。

每当定义一个包含单个参数的构造函数时，编译器会自动定义一个转换运算符，用于在参数类型和用户定义对象类型之间进行转换。

### 转换运算符的自动生成

现在，让我们看另一个有趣的点。读者可能会想知道为什么程序的最后一句话，即

```
brother FourthBrother = "Ricky Ponting";
```

能够在没有错误的情况下编译。左侧（LHS）是 brother 类型的对象，右侧（RHS）是 C 类型字符串。程序没有为将 C 类型字符串转换为 brother 类提供任何转换器。一个 brother 对象正在用字符数组（即 C 类型字符串）初始化。brother 对象和 C 类型字符串是不同类型的。C++ 如何在没有我们特定指示的情况下提供这种转换？这是因为每当定义一个包含单个参数的构造函数时，编译器就会自动为参数类型（这里是 C 类型字符串）和用户定义对象类型之间定义一个转换运算符。

以下程序是另一个例子，说明类 Number 如何被赋予内置项（整数）。

在最后一句 No2 = 5; 中，我们没有指定将整数转换为数字的任何转换运算符，但它仍然会自动完成。

```cpp
//ImplicitConversion.cpp
#include <iostream>
#include <string>
using namespace std;
class Number
{
    int Value;
public:
    Number()
    {
        Value = 0;
    }
    Number(int TempValue)
    {
        Value = TempValue;
    }
};
void main()
{
    Number No1(5); Number No2;
    No2 = 5;
    /* This is implicit conversion. 5 is converted to Number Object and then assigned to No2*/
}
```

我们将在第 6 章学习转换运算符。有时我们不希望编译器进行自动转换。这种情况下应遵循的程序在第 5.7 节中解释。

## 5.7 显式构造函数

在大多数情况下，自动转换增加了可读性。因此非常有用。然而，有时我们不需要这种隐式转换。可以通过在定义构造函数时使用关键字 `explicit` 在构造函数名称前避免创建转换运算符。如果我们不希望语句 `brother FourthBrother = "Ricky Ponting"` 像 `brother FourthBrother("Ricky Ponting")` 一样工作，那么我们需要在构造函数名称前加上关键字 `explicit`。让我们使用程序 5.4 中的修改示例来讨论这一点。

```cpp
//ExplicitCons.cpp
#include <iostream>
#include <string>
using namespace std;

class brother
{
    string Name;
public:
    explicit brother(string BrotherName)
    {
        /* See the explicit keyword before the constructor */
        {
            Name = BrotherName;
        }
    }
};

void main()
{
    brother FirstBrother = brother("Steve Waugh");
    brother SecondBrother("Mark Waugh");
    brother ThirdBrother("Gilchrist");

    // The following statement is erroneous
    brother FourthBrother = "Ricky Ponting";

    /* A compiler would flag an error such as "initializing": cannot convert from "char[11]"
    to "brother" */
}
```

### 程序的工作原理

为什么语句
`brother FourthBrother = "Ricky Ponting"`
将无法工作而
会工作




## 第7章

以一个简单的 value class 定义为例：

// Class representing a height
value class Height
{
private:
    // Records the height in feet and inches
    int feet;
    int inches;

public:
    // Create a height from inches value
    Height(int ins)
    {
        feet = ins/12;
        inches = ins%12;
    }

    // Create a height from feet and inches
    Height(int ft, int ins) : feet(ft), inches(ins) {}
};
```

这定义了一个名为 Height 的 value class 类型。它有两个私有字段，都是 int 类型，用于记录英尺和英寸的高度。该类有两个构造函数——一个用于从作为参数提供的英寸数创建 Height 对象，另一个用于从英尺和英寸的指定值创建 Height 对象。后者最好检查作为参数提供的英寸数是否小于 12，但我把这个细节留给你补充。要创建 Height 类型的变量，你可以写：

```
Height tall = Height(7, 8);        // Height is 7 feet 8 inches
```

这创建了变量 tall，其中包含表示 7 英尺 8 英寸的 Height 对象；该对象是通过调用带两个参数的构造函数创建的。

```
Height baseHeight;
```

此语句创建了一个变量 baseHeight，它将被自动初始化为零高度。Height 类没有指定无参构造函数，并且由于它是一个 value class，你不允许在类定义中提供一个。value class 会自动包含一个无参构造函数，它会将所有值类型字段初始化为零的等价物，并将所有句柄字段初始化为 nullptr，并且你不能用自己的版本覆盖隐式构造函数。正是这个默认构造函数将被用来创建 baseHeight 的值。

value class 可以包含的内容还有一些其他限制：

- 你不得在 value class 定义中包含拷贝构造函数。
- 你不能在 value class 中重写赋值运算符（我将在第 8 章讨论如何在类中重写运算符）。

value class 对象始终通过仅复制字段来复制，一个 value class 对象对另一个 value class 对象的赋值也是以相同的方式进行。value class 旨在用于表示由有限数据定义简单对象，因此对于不符合此规范的对象或 value class 限制有问题的对象，你应该使用 ref class 类型来表示它们。

让我们对 Height 类进行测试。

## Try It Out Defining and Using a Value Class Type

以下是练习 Height value class 的代码：

// Ex7_14.cpp : main project file.
// Defining and using a value class type

#include "stdafx.h"

using namespace System;
```

```
// Class representing a height
value class Height
{
private:
    // Records the height in feet and inches
    int feet;
    int inches;

public:
    // Create a height from inches value
    Height(int ins)
    {
        feet = ins/12;
        inches = ins%12;
    }

    // Create a height from feet and inches
    Height(int ft, int ins) : feet(ft), inches(ins){}
};
```

```
int main(array<System::String ^> ^args)
{
    Height myHeight = Height(6,3);
    Height^ yourHeight = Height(70);
    Height hisHeight = *yourHeight;

    Console::WriteLine(L"My height is {0}", myHeight);
    Console::WriteLine(L"Your height is {0}", yourHeight);
    Console::WriteLine(L"His height is {0}", hisHeight);
    return 0;
}
```

执行此程序会产生以下输出：

```
My height is Height
Your height is Height
His height is Height
Press any key to continue . . .
```

## How It Works

嗯，输出有点单调，也许没有我们希望的那样，但我们稍后再回来讨论。在 main() 函数中，你使用以下语句创建了三个变量：

```
Height myHeight = Height(6,3);
Height^ yourHeight = Height(70);
Height hisHeight = *yourHeight;
```

第一个变量的类型为 Height，因此表示 6 英尺 3 英寸高度的对象被分配在栈上。第二个变量是类型为 Height^ 的句柄，因此表示 5 英尺 10 英寸高度的对象在 CLR 堆上创建。第三个变量是另一个栈变量，它是 yourHeight 引用的对象的副本。因为 yourHeight 是一个句柄，你必须对其进行解引用才能将其赋给 hisHeight 变量，其结果是 hisHeight 包含 yourHeight 引用的对象的副本。value class 类型的变量始终包含一个唯一的对象，因此两个此类变量不能引用同一个对象；将一个 value class 类型的变量赋给另一个变量始终涉及复制。当然，多个句柄可以引用单个对象，将一个句柄的值赋给另一个句柄只是将地址（或 nullptr）从一个复制到另一个，因此两个对象引用同一个对象。

输出由三个 Console::WriteLine() 函数调用产生。不幸的是，输出不是 value class 对象的值，而只是类名。那么这是怎么发生的呢？期望输出值有点乐观——毕竟，编译器怎么知道它们应该如何呈现呢？Height 对象包含两个值——应该呈现哪一个作为值？类必须有一种方法在这种情况下使值可用。

## The ToString() Function in a Class

你定义的每个 C++/CLI 类都有一个 ToString() 函数——我将在下一章讨论类继承时解释这是如何发生的——它返回一个表示类对象的字符串的句柄。编译器会在它识别到需要对象的字符串表示时安排调用对象的 ToString() 函数，你也可以在必要时显式调用它。例如，你可以写：

```
double pi = 3.142;
Console::WriteLine(pi.ToString());
```

这会输出 pi 的值作为字符串，并且提供该字符串的是 System::Double 类中定义的 ToString() 函数。当然，如果不显式调用 ToString() 函数，你也会得到相同的输出。

Height 类中默认的 ToString() 函数只是输出类名，因为事先没有办法知道应为你的类类型的对象返回什么值作为字符串。为了在前面的示例中让 Console::WriteLine() 函数输出适当的值，你必须向 Height 类添加一个 ToString() 函数，以你想要的形式呈现对象的值。

以下是带有 ToString() 函数的类：

// Class representing a height
value class Height
```

```
{
private:
    // Records the height in feet and inches
    int feet;
    int inches;

public:
    // Create a height from inches value
    Height(int ins)
    {
        feet = ins/12;
        inches = ins%12;
    }

    // Create a height from feet and inches
    Height(int ft, int ins) : feet(ft), inches(ins) {}

    // Create a string representation of the object
    virtual String^ ToString() override
    {
        return feet + L" feet " + inches + L" inches";
    }
};
```

在 ToString() 的返回类型前使用 virtual 关键字，并在函数参数列表后使用 override 关键字，表示此版本的 ToString() 函数覆盖了默认情况下存在于类中的函数版本。你将在第 8 章听到更多关于此的内容。我们新的 ToString() 函数现在输出一个以英尺和英寸表示高度的字符串。如果你在前面的示例中将此函数添加到类定义中，编译并执行程序时，你会得到以下输出：

```
My height is 6 feet 3 inches
Your height is 5 feet 10 inches
His height is 5 feet 10 inches
Press any key to continue . . .
```

这更像是你之前期望得到的。你可以从输出中看出，WriteLine() 函数非常乐意处理通过 yourHeight 句柄引用的 CLR 堆上的对象，以及在栈上创建的 myHeight 和 hisHeight 对象。

## Literal Fields

你用来在英尺和英寸之间转换的因子 12 有点令人困扰。它是所谓的“魔数”的一个例子，即阅读代码的人必须猜测或推断其意义和来源。在这种情况下，12 很明显是什么，但在许多情况下，计算中数值常量的来源并不那么明显。C++/CLI 具有字面量字段设施，可在类中引入命名常量，从而解决此问题。以下是如何从 Height 类的单参数构造函数中消除魔数：

```
value class Height
{
private:
```


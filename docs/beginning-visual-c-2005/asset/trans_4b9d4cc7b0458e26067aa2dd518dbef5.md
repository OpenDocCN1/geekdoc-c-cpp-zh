

## 重载赋值运算符

如果你没有为你的类提供重载的赋值运算符函数，编译器会提供一个默认版本。默认版本只是提供逐成员的复制过程，与默认拷贝构造函数类似；然而，不要把默认拷贝构造函数与默认赋值运算符混淆。默认拷贝构造函数会在用同一类的现有对象初始化类对象，或按值将对象传递给函数时被调用。另一方面，默认赋值运算符则在赋值语句的左侧和右侧都是同一类类型的对象时被调用。

对于 CBox 类，默认赋值运算符可以正常工作，但对于任何为成员动态分配空间的类，你都需要仔细查看该类的需求。如果在这种情况下省略赋值运算符，你的程序中可能会出现相当大的混乱潜力。

暂时回到你在我谈论拷贝构造函数时使用的 CMessage 类。记住它有一个成员 pmessage，它是指向字符串的指针。现在考虑默认赋值运算符可能产生的效果。假设你有两个类的实例，motto1 和 motto2。你可以尝试使用默认赋值运算符将 motto2 的成员设置为 motto1 的成员，如下所示：

```
motto2 = motto1;              // Use default assignment operator
```

对这个类使用默认赋值运算符的效果本质上与使用默认拷贝构造函数相同：会造成灾难！因为每个对象都有指向同一字符串的指针，如果为一个对象更改字符串，它对两个对象都发生了更改。还有一个问题是，当类的一个实例被销毁时，其析构函数会释放用于字符串的内存，而另一个对象就剩下指向可能现在被用于其他用途的内存的指针。

你需要赋值运算符做的是将文本复制到目标对象拥有的内存区域。

### 修复问题

你可以用自己的赋值运算符函数来修复这个问题，我们假设它是在类定义内定义的：

```
// Overloaded assignment operator for CMessage objects
CMessage& operator=(const CMessage& aMess)
{
    // Release memory for 1st operand
    delete[] pmessage;
    pmessage = new char[strlen(aMess.pmessage) + 1];

    // Copy 2nd operand string to 1st
    strcpy(this->pmessage, aMess.pmessage);

    // Return a reference to 1st operand
    return *this;
}
```

赋值看起来非常简单，但有几个细微之处需要进一步研究。请注意你从赋值运算符函数返回一个*引用*。为什么要这样做可能并不立即明显（毕竟，函数确实完全完成了赋值操作，并且右侧的对象被复制到左侧）。从表面上看，这似乎表明你不需要返回任何东西，但你需要更深入地考虑运算符可能如何被使用。

有可能你需要在表达式的右侧使用赋值操作的结果。考虑如下语句：

```
motto1 = motto2 = motto3;
```

因为赋值运算符是右结合的，所以先执行 motto3 赋给 motto2，这可以翻译成以下语句：

```
motto1 = (motto2.operator=(motto3));
```

这里运算符函数调用的结果在等号的右侧，所以语句最终变成这样：

```
motto1.operator=(motto2.operator=(motto3));
```

如果要使其工作，你当然必须返回一些东西。括号之间的 operator=() 函数调用必须返回一个可以作为另一个 operator=() 函数调用的参数使用的对象。在这种情况下，返回类型为 CMessage 或 CMessage& 都可以，所以引用在此情况下不是强制的，但你至少必须返回一个 CMessage 对象。

然而，考虑以下示例：

```
(motto1 = motto2) = motto3;
```

这是完全合法的代码（括号确保最左边的赋值先执行）。这可以翻译成以下语句：

```
(motto1.operator=(motto2)) = motto3;
```

当你将剩余的赋值操作表示为显式的重载函数调用时，这最终变成：

```
(motto1.operator=(motto2)).operator=(motto3);
```

现在你有一个情况，即从 operator=() 函数返回的对象被用来调用 operator=() 函数。如果返回类型只是 CMessage，这是不合法的，因为实际上返回的是原始对象的临时副本，而编译器不允许使用临时对象进行成员函数调用。换句话说，当返回类型为 CMessage 时，返回值不是左值。确保这种事情能够编译并正确工作的唯一方法是返回一个引用，它是左值，所以如果你想允许对类对象使用赋值运算符的完全灵活使用，唯一可能的返回类型是 CMessage&。

请注意，原生的 C++ 语言不对赋值运算符的接受参数或返回类型施加任何限制，但如果你希望你的赋值运算符函数支持正常的 C++ 赋值用法，有意义的是按我刚才描述的方式声明运算符。

你需要牢记的第二个细微之处是，每个对象已经为字符串分配了内存，所以运算符函数要做的第一件事是删除分配给第一个对象的内存，并重新分配足够的内存以容纳第二个对象所属的字符串。完成此操作后，第二个对象的字符串可以复制到现在由第一个对象拥有的新内存中。

这个运算符函数仍然存在缺陷。如果写下以下语句会怎样？

```
motto1 = motto1;
```

显然，你不会直接做这种愚蠢的事情，但它很容易隐藏在指针后面，例如在以下语句中。

```
motto1 = *pMess;
```

如果指针 pMess 指向 motto1，你本质上就有前面的赋值语句。在这种情况下，按原样存在的运算符函数会删除 motto1 的内存，基于已被删除的字符串长度分配更多内存，并尝试复制旧内存，而到那时，旧内存可能已经被破坏。你可以在函数开头添加对左右操作数是否相同的检查来修复它，因此 operator=() 函数的定义现在将变成这样：

```
// Overloaded assignment operator for CMessage objects
CMessage& operator=(const CMessage& aMess)
{
    if (this == &aMess)           // Check addresses, if equal
        return *this;             // return the 1st operand

    // Release memory for 1st operand
    delete[] pmessage;
    pmessage = new char[strlen(aMess.pmessage) + 1];

    // Copy 2nd operand string to 1st
    strcpy(this->pmessage, aMess.pmessage);

    // Return a reference to 1st operand
    return *this;
}
```

此代码假定函数定义出现在类定义内。

### 试试看 重载赋值运算符

让我们把它放在一个工作示例中。我们同时向类添加一个名为 Reset() 的函数。这只是将消息重置为星号字符串。

```
// Ex8_05.cpp
// Overloaded copy operator perfection
#include <iostream>
#include <cstring>
using std::cout;
using std::endl;

class CMessage

int main()
{
    CMessage motto1("The devil takes care of his own");
    CMessage motto2;

    cout << "motto2 contains - ";
    motto2.ShowIt();
    cout << endl;

    motto2 = motto1;                    // Use new assignment operator

    cout << "motto2 contains - ";
    motto2.ShowIt();
    cout << endl;

    motto1.Reset();                     // Setting motto1 to * doesn't
                                        // affect motto2

    cout << "motto1 now contains - ";
    motto1.ShowIt();
    cout << endl;

    cout << "motto2 still contains - ";
    motto2.ShowIt();
    cout << endl;

    return 0;
}
```

你可以看到从此程序的输出中，一切都按要求正常工作，两个对象的消息之间没有链接，除非你显式地将它们设为相等：

```
motto2 contains -
Default message
motto2 contains -
The devil takes care of his own
motto1 now contains -
********************************
motto2 still contains -
The devil takes care of his own
Destructor called.
Destructor called.
```

所以让我们从所有这些中再得到一条黄金法则：

> *如果为类的一个数据成员动态分配空间，始终实现赋值运算符。*

实现了赋值运算符后，像 `+=` 这样的操作会怎样？嗯，除非你实现它们，否则它们不起作用。对于你希望与类对象一起使用的每一种 `op=` 形式，你需要编写另一个运算符函数。


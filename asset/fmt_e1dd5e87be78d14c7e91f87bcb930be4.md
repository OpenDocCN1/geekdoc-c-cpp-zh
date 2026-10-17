
```cpp
inline const Length Length::operator++(int){
    Length length(*this);    // 拷贝当前对象
    ++this;                   // 增加当前对象
    return length;            // 返回原始拷贝
}
```

在拷贝当前对象后，使用该类的前缀 `++` 运算符对其进行增加。然后你返回原始的、未优化的对象拷贝；这个值将用于运算符所操作的表达式。将返回值指定为 `const` 可以防止诸如 `data++++compile` 这样的表达式出现。

# 重载函数调用运算符

函数调用运算符是 `()`，因此该函数的重载为 `operator(){}`。重载了函数调用运算符的类对象被称为函数对象（function object）或函数（function），因为你可以像使用函数名一样使用对象名。这是一个重载了函数调用运算符的类：

```cpp
class Area
{
public:
    int operator()(int length, int width) { return length*width; }
};
```

该类中的函数调用运算符通过其整数参数的积计算面积。要使用此运算符函数，你只需要创建一个 `Area` 类型的对象，例如：

`Area area;`

`int pitchLength(100), pitchWidth(50);`

`int pitchArea = area(pitchLength, pitchWidth);`

// 创建函数对象

// 执行函数调用重载

第一条语句创建了 `area` 对象，该对象在第三条语句中用于调用该对象的函数调用。在这种情况下，返回的是足球的长度。

当然，你可以像传递其他对象一样将函数对象传递给另一个函数。看这个函数：

```cpp
void printArea(int length, int width, Area& area)
{
cout << "Area is " << area(length, width);
}
```

这是一条使用该函数的语句：

```cpp
printArea(20, 35, Area());
```

这条语句调用了 `printArea()` 函数，前两个参数指定了矩形的长度和宽度。第三个参数调用 `Area` 类构造函数创建一个并在函数中计算面积的对象。因此，函数对象提供了一种将函数作为参数传递给另一个函数的方法，这比使用函数指针更简单且易于操作。

> 注意：在第 10 章中你将学习 `std::function<>` 模板，它在传递函数时提供了更大的灵活性。

定义函数对象的类通常不需要数据成员，也没有定义构造函数，因此创建和使用函数对象的开销极小。函数对象类通常定义为模板，因为正如你在本章稍后部分看到的，这使得它们非常灵活。

# 对象拷贝问题

在向函数传递参数时拷贝是隐式的。当参数是基本类型时，这不是问题；但对于类类型对象的参数，这可能会成为问题。拷贝对象产生的开销可能是巨大的，特别是当对象很大或拥有动态分配的内存时。拷贝对象通过调用类的拷贝构造函数完成，因此这种拷贝效率对执行性能至关重要。正如你在 `Message` 类中看到的，赋值运算符也涉及对象的拷贝。然而，在某些情况下，这种拷贝操作并不是真的，如果你能在这些情况下找到避免它们的方法就可以减少执行时间。右值引用（Rvalue reference）参数是实现这种可能的关键。

来自 `Ex8_05.cpp` 的 `CMessage` 类的修改版本将为观察其原理提供基础。以下是实现加运算符的类版本：

```cpp
class CMessage
{
private:
    char* message; // 指向对象文本字符串的指针
public:
    // 显示消息的
    void ShowIt() const {
        cout << endl << message;
    }

    // 重载的加运算符
    CMessage operator+(const CMessage& aMess) const {
        cout << "Add operator function called." << endl;
        size_t len = strlen(message) + strlen(aMess.message) + 1;
        CMessage result;
        result.message = new char[len];
        strncpy(result.message, message, len);
        strncat(result.message, aMess.message, len-strlen(result.message));
        return result;
    }

    // 用于 CMessage 对象的重载赋值运算符
    CMessage& operator=(const CMessage& aMess) {
        cout << "Assignment operator function called." << endl;
        if(this != &aMess) {
            // ... 赋值逻辑
        }
        return *this;
    }
};
```

(注：原文提供的 `CMessage` 类文本是片段化且不完整的；我已根据可见片段重建了结构。)

我们感兴趣的第二个语句是：

```cpp
motto3 = motto3 + motto + motto2;
```

调用 `operator+()` 函数来拼接 `motto3` 和 `motto`，该函数调用构造函数来创建返回的结果。返回的对象随后使用拷贝构造函数进行拷贝，函数内部创建的原始对象由析构函数销毁。然后通过再次调用一次 `operator+()` 将拷贝的对象与 `motto2` 拼接，并重复这一调用序列。最后，调用 `operator=()` 函数来存储结果。因此，对于这个简单的语句，我们包含了来自临时对象、来自拷贝构造函数调用以及来自赋值运算符的拷贝操作。

如果 `CMessage` 是一个大型或复杂的对象，所有这些拷贝操作在执行时间内可能非常昂贵。如果能够避免拷贝操作，你可以显著提高执行效率。让我们来看看如何实现这一点。

## 应用右值引用参数

当源 `CMessage` 对象是一个将在拷贝操作后立即销毁的临时对象时，拷贝它的替代方案是偷取属于临时对象的内存（由其 `pmessage` 成员指向）并将其转移到目标对象。如果这样做，你就避免了为目标对象分配更多内存的需要，不需要拷贝数据，也不需要释放源对象拥有的内存。源对象将在操作后立即被销毁，因此这样做没有风险——只是执行速度更快。执行此操作的关键在于能够检测拷贝操作中的源对象何时为右值（rvalue）。这正是右值引用参数允许你做的事情。

你可以像这样为 `operator=()` 函数创建一个重载：

```cpp
CMessage& operator=(const CMessage& ammessage)
{
    cout << "Move assignment operator called." << endl;
    delete[pmessage]; // 释放左侧操作数的内存
    pmessage = ammessage.pmessage; // 从右侧对象偷取字符串
    ammessage.pmessage = nullptr; // 将右侧指针置空
    return *this; // 返回左侧操作数的引用
}
```

当赋值的右操作数为右值（临时对象）时，将调用此运算符函数。当右操作数为左值（lvalue）时，将调用带有左值引用参数的原始函数。该左值引用函数会删除目标对象 `pmessage` 指向的字符串，并拷贝源对象 `pmessage` 成员中存储的地址。然后将源对象的 `pmessage` 成员设为 `nullptr`。这一点至关重要；否则消息将因源对象析构函数的调用而被删除。请注意，在这种情况下你不能将参数指定为 `const`，因为你正在修改它。

你可以通过添加一个带有右值引用参数的重载拷贝构造函数，将完全相同的逻辑应用于拷贝构造操作：

```cpp
CMessage(CMessage&& aMessage)
{
  cout << "Move constructor called." << endl;
  pmessage = aMessage.pmessage;
  aMessage.pmessage = nullptr;
}
```

与其将属于源对象的消息拷贝到正在构造的对象中，你只需将消息字符串的地址从源对象转移到新对象，因此在这种情况下，它只是一个移动操作。与之前一样，你将源对象的 `pmessage` 设置为 `nullptr`，以防止消息字符串被析构函数删除。

## 尝试高效的对象拷贝操作

你可以创建一个新实例 `Ex8_07`，并在 `CMessage` 类定义中创建我刚才讨论的拷贝构造函数。此示例将产生以下输出：

```
Constructor called.
Constructor called.
Constructor called.
Executing: motto3 = motto1 + motto2
Add operator function called.
Constructor called.
Move copy constructor called.
Destructor called.
Move assignment operator function called.
Destructor called.
Done!!

Executing: motto3 = motto1 + motto1 + motto2
Add operator function called.
Constructor called.
Move copy constructor called.
Destructor called.
Add operator function called.
Constructor called.
Move copy constructor called.
Destructor called.
Move assignment operator function called.
Destructor called.
Done!!
```

`motto3` 包含

- The devil takes care of his own. If you sup with the devil use a long spoon.

- The devil takes care of his own. If you sup with the devil use a long spoon.

Destructor called.

Destructor called.

Destructor called.

## 工作原理

在上一个示例中，你可以看到移动操作现在可以工作了。输出显示 `motto3` 包含与之前相同的字符串，因此成员函数已相应更改。请注意，对于定义了复杂或大型对象的类，拷贝构造函数和赋值运算符可以显著提高性能。输出显示，如果你不定义这些，编译器将提供执行拷贝的默认版本，而这并不是你想要的。

## 具名对象是左值

当使用右值参数调用赋值运算符时，它可以偷取内存。然而，如果参数是一个具名变量，它就是一个左值，必须使用拷贝构造函数。这是因为该具名变量在赋值完成后可能还会被需要。

```cpp
strcpy_s(this->pText, len, txt.pText);
}
return *this; // 返回第一个操作数的引用
```

// 用于 CText 对象的移动赋值运算符

`CText& operator=(CText& txt)`

```cpp
cout << "CText move assignment operator function called." << endl;
delete[] pText;
pText = txt.pText;
txt.pText = nullptr;
return *this; // 返回第一个操作数的引用
```

// 重载的加法运算符

`CText* operator+(const CText& txt) const`

```cpp
cout << "CText add operator function called." << endl;
size_t len=strlen(pText) + strlen(txt.pText) + 1;
aText->pText = new char[len];
strcpy_s(aText->pText, len, pText);
strcat_s(aText->pText, len, txt.pText);
return aText;
```

这看起来代码很多，但这是因为该类重载了拷贝构造函数和赋值运算符，并且定义了 `operator+()`。`CMessage` 类在实现其成员函数时利用了这些内容。当每个函数被调用时，还有输出跟踪。让我们通过示例来测试这些类。

# 尝试一下 悄悄积累的效率低下

这是一个简单的 `main()` 函数，它使用了 `CMessage` 的拷贝构造函数和赋值运算符：

```cpp
// CEx_09.cpp 悄悄积累的效率低下
#include <iostream>
#include <string>
using std::cout;
using std::endl;
```

```cpp
// 在此处插入 CText 类定义...
// 在此处插入 CMessage 类定义...
```

```cpp
int main() {
    CMessage motto1("*The devil takes care of his own.*");
    CMessage motto2("*If you sup with the devil using a large spoon.\n*");

    cout << endl << "* Executing: CMessage motto3(motto1+motto2); *" << endl;
```

```cpp
CMessage motto3(motto1+motto2);
cout << " * Done!!" << endl << " *motto3 contains -";
motto3.Show();
CMessage motto4;
cout << endl << " * Executing: motto4 = motto3 + motto2; *" << endl;
motto4 = motto3 + motto2;
cout << " * Done!!" << endl << endl << " *motto4 contains -";
motto4.Show();
cout << endl;
return 0;
}
```

## 工作原理

从 `main()` 中相对较少的语句中产生了大量的输出。我将讨论其中有趣的部分。让我们先考虑由语句产生的输出：

```cpp
CMessage motto3(motto1+motto2);
```

输出如下：

- CMessage add operator function called.

- CText constructor called.

- CMessage constructor called.

- CText constructor called.

- CText move assignment operator function called.

- CText destructor called.

- CText add operator function called.

- CText constructor called.

- CText move copy constructor called.

- CText destructor called.

- CText move assignment operator function called.

- CText destructor called.

- CText constructor called.

- CMessage move constructor called.

- CText assignment operator function called.

- CText destructor called.

要查看发生了什么，你需要将输出信息与被调用的函数代码联系起来。首先，调用 `CMessage` 类的 `operator+` 来连接 `motto` 和 `motto2`。在该函数的体中，调用了 `CMessage` 构造函数来创建消息对象，并且在这个过程中，调用了 `CText` 构造函数。一切运行顺利，直到我们到达输出的倒数第二行，紧跟在指示调用 `CMessage` 移动构造函数的行之后。当此构造函数执行时，参数必须是一个临时值 - 右值（rvalue），因此函数体中存储文本成员值的赋值操作应该是 `CText` 对象的移动操作，而不是拷贝赋值。问题的出现是因为在 `CMessage` 移动构造函数内部，`aMessage` 参数是一个左值（lvalue），因为它有一个名字，尽管我们非常确定传递给函数的参数是一个右值。这意味着 `aMessage.text` 也是一个左值。如果不是，就会调用 `CMessage` 的拷贝构造函数。

同样的语句也存在相同的问题：

```cpp
motto4 = motto3 + motto2;
```

如果你查看此语句的输出，你会发现当调用 `CMessage` 对象的移动赋值运算符时，出现了完全相同的问题。文本成员被拷贝了，而实际上它本可以移动。

为了修复这些效率低下的问题，你需要在 `CMessage` 类的移动赋值和移动构造函数中使用 `a.text` 将其变为右值。C++ 的实用头文件贴心地为你提供了 `std::move()` 函数，它恰好能实现你想要。该函数会将你传递给它的任何参数作为右值返回。你可以这样修改移动构造函数：

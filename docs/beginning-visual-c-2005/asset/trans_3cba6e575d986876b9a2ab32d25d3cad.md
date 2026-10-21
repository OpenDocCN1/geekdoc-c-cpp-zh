
（~）。类析构函数不返回值，也没有参数。对于 CBox 类，类析构函数的原型是：

```
~CBox();    // Class destructor prototype
```

由于析构函数没有参数，一个类中只能有一个析构函数。

> 为析构函数指定返回值或参数是错误的。

## 默认析构函数

到目前为止你使用的所有对象，都是由类的默认析构函数自动销毁的。如果你没有定义自己的类析构函数，编译器总是会自动生成默认析构函数。默认析构函数不会删除由 `new` 运算符在自由存储区中分配的对象或对象成员。如果类成员的空间是在构造函数中动态分配的，你就必须定义自己的析构函数，并显式使用 `delete` 运算符来释放构造函数通过 `new` 运算符分配的内存，就像对普通变量所做的那样。你需要练习编写析构函数，那我们就来试一试。

## 试一试……一个简单的析构函数

为了了解类的析构函数何时被调用，你可以在 `CBox` 类中加入一个析构函数。下面是包含带析构函数的 `CBox` 类的示例定义：

```
// Ex8_01.cpp
// Class with an explicit destructor
#include <iostream>
using std::cout;
using std::endl;

class CBox                 // Class definition at global scope
{
public:
    // Destructor definition
    ~CBox()
    {
        cout << "Destructor called." << endl;
    }

    // Constructor definition
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0);
        m_Length(lv), m_Width(wv), m_Height(hv)
    {
        cout << endl << "Constructor called.";
    }

    // Function to calculate the volume of a box
    double Volume() const
    {
        return m_Length*m_Width*m_Height;
    }

    // Function to compare two boxes which returns true
// if the first is greater that the second, and false otherwise
int compare(CBox* pBox) const
{
    return this->Volume() > pBox->Volume();
}

private:
    double m_Length;      // Length of a box in inches
    double m_Width;       // Width of a box in inches
    double m_Height;      // Height of a box in inches
};

// Function to demonstrate the CBox class destructor in action
int main()
{
    CBox boxes[5];        // Array of CBox objects declared
    CBox cigar(8.0, 5.0, 1.0);  // Declare cigar box
    CBox match(2.2, 1.1, 0.5);  // Declare match box
    CBox* pB1 = &cigar;         // Initialize pointer to cigar object address
    CBox* pB2 = 0;              // Pointer to CBox initialized to null

    cout << endl
         << "Volume of cigar is "
         << pB1->Volume();      // Volume of obj. pointed to

    pB2 = boxes;                // Set to address of array
    boxes[2] = match;           // Set 3rd element to match
    cout << endl
         << "Volume of boxes[2] is "
         << (pB2 + 2)->Volume();  // Now access thru pointer

    cout << endl;
    return 0;
}
```

## 工作原理

`CBox` 类的析构函数所做的唯一事情就是显示一条消息，表明它被调用了。

输出是：

```
Constructor called.
Constructor called.
Constructor called.
Constructor called.
Constructor called.
Constructor called.
Constructor called.
Volume of cigar is 40
Volume of boxes[2] is 1.21
Destructor called.
Destructor called.
Destructor called.
Destructor called.
Destructor called.
Destructor called.
Destructor called.
```

在程序结束时，每个存在的对象都会调用一次析构函数。每次发生的构造函数调用，都有一个匹配的析构函数调用。这里不需要显式调用析构函数。当类的对象超出作用域时，编译器会安排自动调用该类的析构函数。在我们的示例中，析构函数的调用发生在 `main()` 执行完之后，因此析构函数中的错误很可能导致程序在 `main()` 安全终止后崩溃。

## 析构函数与动态内存分配

你会发现，你经常需要为类数据成员动态分配内存。可以在构造函数中使用 `new` 运算符为对象成员分配空间。在这种情况下，你必须通过提供合适的析构函数，在对象不再需要时负责释放空间。我们先定义一个可以这样做的简单类。

假设你想定义一个类，其中每个对象都是某种消息，例如一个文本字符串。这个类应尽可能节省内存，因此，与其将数据成员定义为足以容纳你可能需要的最大长度字符串的 `char` 数组，不如在创建对象时在自由存储区中为消息分配内存。下面是这个类的定义：

```
//Listing 08_01
class CMessage
{
private:
    char* pmessage;                // Pointer to object text string

public:
    // Function to display a message
    void ShowIt() const
    {
        cout << endl << pmessage;
    }

    // Constructor definition
    CMessage(const char* text = "Default message")
    {
        pmessage = new char[strlen(text) + 1];   // Allocate space for text
        strcpy(pmessage, text);                  // Copy text to new memory
    }

    ~CMessage();                           // Destructor prototype
};
```

这个类只定义了一个数据成员 `pmessage`，它是一个指向文本字符串的指针。它定义在类的私有部分，因此无法从类外部访问。

在公有部分，有一个 `ShowIt()` 函数，用于将 `CMessage` 对象输出到屏幕。你还看到了一个构造函数的定义，以及类析构函数 `~CMessage()` 的原型，稍后我会介绍这个析构函数。

类的构造函数需要一个字符串作为参数，但如果没有传入参数，它就会使用为该参数指定的默认字符串。构造函数使用库函数 `strlen()` 获取作为参数传入的字符串长度，不包括结尾的 NULL 字符。为了让构造函数使用这个库函数，必须有包含 `<cstring>` 头文件的 `#include` 语句。构造函数通过给 `strlen()` 函数返回的值加 1，来确定在自由存储区中存储该字符串所需的内存字节数。

> 当然，如果内存分配失败，将抛出异常并终止程序。如果希望处理这类失败，使程序以更优雅的方式结束，可以在构造函数代码中捕获该异常。（有关处理内存不足情况的信息，请参阅第 6 章。）

使用 `new` 运算符取得字符串内存后，再使用同样在 `<cstring>` 头文件中声明的 `strcpy()` 库函数，将作为构造函数参数传入的字符串复制到为该字符串分配的内存中。`strcpy()` 函数会将第二个指针参数指定的字符串复制到第一个指针参数所含的地址中。

现在你需要编写一个类析构函数，用来释放为消息分配的内存。如果你不为该类提供析构函数，就没有办法删除为对象分配的内存。如果在程序中按现在这种形式使用这个类，并创建大量 `CMessage` 对象，自由存储区会被逐渐耗尽，直到程序失败。这种情况很容易发生在不太明显的情况下。例如，如果在一个函数中创建了临时的 `CMessage` 对象，而该函数在程序中被多次调用，你可能会认为这些对象在函数返回时已被销毁。你当然没有想错，但自由存储区中的内存并不会随之释放。因此，每调用一次函数，自由存储区中就会有更多内存被已丢弃的 `CMessage` 对象占用。

`CMessage` 类析构函数的代码如下：

```
// Listing 08_02
// Destructor to free memory allocated by new
CMessage::~CMessage()
{
    cout << "Destructor called."        // Just to track what happens
         << endl;
    delete[] pmessage;                // Free memory assigned to pointer
}
```

由于析构函数是在类定义之外定义的，你必须用类名 `CMessage` 来限定析构函数的名称。析构函数所做的只是显示一条消息，以便你了解正在发生的事情，然后使用 `delete` 运算符释放 `pmessage` 成员指向的内存。注意，必须将方括号与 `delete` 一起使用，因为你删除的是一个 `char` 类型的数组。

## 试一试：使用消息类

你可以通过一个小示例来使用 `CMessage` 类：

```
// Ex8_02.cpp
// Using a destructor to free memory
#include <iostream>        // For stream I/O
```

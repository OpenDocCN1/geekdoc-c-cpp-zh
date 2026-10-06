
```cpp
class CMessage
{
private:
    char* pmessage; // 指向对象字符串的指针

public:
    // 显示消息的函数
    void ShowIt() const {
        cout << endl << pmessage;
    }

    // 重载的加运算符
    CMessage operator+(const CMessage& aMessage) const {
        cout << "Add operator function called." << endl;
        size_t len = strlen(pmessage) + strlen(aMessage.pmessage) + 1;
        CMessage message;
        message.pmessage = new char[len];
        strcpy_s(message.pmessage, len, pmessage);
        strcat_s(message.pmessage, len, aMessage.pmessage);
        return message;
    }

    // CMessage 对象的重载赋值运算符
    CMessage& operator=(const CMessage& aMessage) {
        cout << "Assignment operator function called." << endl;
        if(this != &aMessage) // 检查地址是否相等
        {
            // 释放第一个操作数的内存
            delete[] pmessage;
            pmessage = new char[strlen(aMessage.pmessage) + 1];

            // 将第二个操作数的字符串拷贝到第一个
            strcpy_s(this->pmessage, strlen(aMessage.pmessage)+1, aMessage.pmessage);
        }
        return *this; // 返回第一个操作数的引用
    }

    // 构造函数定义
    CMessage(char* text = "Default message") {
        cout << "Constructor called." << endl;
        pmessage = new char[strlen(text) + 1]; // 为文本分配空间
        strcpy_s(pmessage, strlen(text)+1, text); // 将文本拷贝到新内存
    }

    // 拷贝构造函数定义
    CMessage(const CMessage& aMess)
    {
        cout << "Copy constructor called." << endl;
        size_t len = strlen(aMess.pmessage)+1;
        pmessage = new char[len];
        strncpy(pmessage, aMess.pmessage, len);
    }

    // 释放由 new 分配内存的析构函数
    ~CMessage()
    {
        cout << "Destructor called.";      // 仅用于跟踪发生了什么
        cout << endl;
        delete[] pmessage;             // 释放指针分配的内存
    }
};
```

`Ex8_05.cpp` 中的更改已高亮显示。现在通过构造函数和赋值运算符函数的输出来跟踪它们调用的时机。还有一个用于两个 `CMessage` 对象的拷贝构造函数和 `operator+()` 函数。你可以添加用于 `CMessage` 与字符串字面量拼接的版本，但这不是必须的。让我们看看在对 `CMessage` 对象进行某些操作时会发生多少拷贝。

# 尝试跟踪对象的拷贝操作

以下是练习 `CMessage` 类的代码：

```cpp
// Ex8_07.cpp
// 有多少拷贝操作？
#include <iostream>
#include <string>
using std::cout;
using std::endl;

// 在此处插入 CMessage 类定义...
int main()
{
    CMessage motto1("The devil takes care of his own.");
    CMessage motto2("If you sup with the devil a long spoon.");
    CMessage motto3;
    cout << " Executing: motto3 = motto1 + motto2 " << endl;
    motto3 = motto1 + motto2;
    cout << " Done!" << endl << endl;

    cout << " Executing: motto3 = motto1 + motto1 + motto2 " << endl;
    motto3 = motto3 + motto1 + motto2;
    cout << " Done!" << endl << endl;

    cout << " " << motto3 contains - " << "";
    motto3.ShowIt();
    cout << endl;
    return 0;
}
```

此示例产生以下输出：

- Constructor called.
- Constructor called.
- Constructor called.
- Executing: motto3 = motto1 + motto2
- Add operator function called.
- Constructor called.
- Copy constructor called.
- Destructor called.
- Assignment operator function called.
- Destructor called.
- Executing: motto3 = motto1 + motto1 + motto2
- Add operator function called.
- Constructor called.
- Copy constructor called.
- Destructor called.
- Assignment operator function called.
- Destructor called.
- Add operator function called.
- Constructor called.
- Copy constructor called.
- Destructor called.
- Assignment operator function called.
- Destructor called.
- Done!
- motto3 contains - The devil takes care of his own. If you sup with the devil a long spoon.

（注意：OCR 输出是碎片化的；上述内容根据代码逻辑重构）。

## 工作原理

第一个感兴趣的语句是：

```cpp
motto3 = motto1 + motto2;
```

调用 `operator+()` 函数返回结果。随后临时对象被销毁。因此，对于这条语句，我们有三次拷贝，来自两个构造函数和一个赋值。

第二个感兴趣的语句是：

```cpp
motto3 = motto3 + motto1 + motto2;
```

因此，对于这个简单的语句，我们有三次拷贝：

- Add operator function called.
- Constructor called.
- Copy constructor called.
- Destructor called.
- Assignment operator function called.
- Destructor called.

# 应用右值引用参数

当源 `CMessage` 是操作后将立即销毁的临时对象时，拷贝的替代方案是提取临时对象的内存并转移到目标对象。如果你这样做，就不需要为目标对象分配更多内存，也不需要释放源对象拥有的内存。源对象将在操作后立即被销毁，因此这样做没有风险——只是执行速度更快。执行这种技巧的关键是检测拷贝操作中的源对象是否为右值。这正是右值引用允许你做的。

你可以这样创建一个 `operator=()` 函数的重载：

```cpp
CMessage& operator=(CMessage&& amess)
{
    cout << "Move assignment operator called." << endl;
    delete[] pmessage; // 释放左操作数的内存
    pmessage = amess.pmessage; // 从右操作数窃取字符串
    amess.pmessage = nullptr; // 空指针
    return *this; // 返回第一个操作数的引用
}
```

你可以将完全相同的逻辑应用于拷贝构造函数操作，只需添加一个带有右值引用参数的重载拷贝构造函数：

```cpp
CMessage(CMessage&& aMessage)
{
    cout << "Move copy constructor called." << endl;
    pmessage = aMessage.pmessage;
    aMessage.pmessage = nullptr;
}
```

与其将属于源对象的消息拷贝到正在构造的对象，不如简单地将消息字符串的地址从源对象转移到新对象，因此在这种情况下，这是一个移动操作。如果你将源对象的 `pmessage` 设置为 `nullptr`，可以防止消息字符串被析构函数删除。

# 尝试高效的对象拷贝操作

你可以创建一个新实例 `Ex8_07`，并将我刚才讨论的重载 `operator=()` 函数和拷贝构造函数添加到 `CMessage` 类的定义中。此示例将产生以下输出：

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
Executing: motto3 = motto3 + motto1 + motto2
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
Destructor called.
Done!!
```

motto3 包含

The devil takes care of his own. If you sup with the devil use a long spoon.

The devil takes care of his own. If you sup with the devil use a long spoon.

Destructor called.
Destructor called.
Destructor called.

## 工作原理

你可以看到上一个示例中所有涉及拷贝对象的操作现在都执行为移动操作。赋值运算符函数现在调用了带有右值引用参数的版本，拷贝构造函数的调用也是如此。输出显示 `motto3` 最终获得了与之前相同的字符串，一切都按预期方式工作。

对于定义了复杂或大型对象的类，使用右值引用参数重载赋值运算符和拷贝构造函数可以显著提高性能。

> 注意：如果你在类中定义了非 `const` 右值引用作为参数的 `operator=()` 函数和拷贝构造函数，请确保你也定义了带有 `const` 左值引用参数的标准版本。如果不这样做，编译器将提供这些函数的默认版本，它们执行逐成员拷贝。这显然不是你想要的。

# 命名对象是左值（Lvalues）

当调用 `CMessage` 类中带有右值引用参数的赋值运算符函数时，你可以确定参数——即右操作——是一个右值，因此是一个你可以“偷取”内存的临时对象。在这个运算符函数的体内，参数 `aMessage` 是一个左值。这是因为命名变量的表达式是左值。这防止了低效的回拷贝，我们可以通过一个使用修改版 `CMessage` 类的示例来演示：

```cpp
class CMessage
{
private:
    CText text;                // 对象文本字符串

public:
    // 显示消息的函数
    void ShowIt() const
    {
        text.ShowIt();
    }

    // 重载加法运算符
    CMessage operator+(const CMessage& aMessage) const
    {
        cout << "CMessage add operator function called." << endl;

        CMessage message;
        message.text = text + aMessage.text;
        return message;
    }

    // CMessage 对象的拷贝赋值运算符
    CMessage& operator=(const CMessage& aMessage)
    {
        cout << "CMessage copy assignment operator function called." << endl;
        if(this != &aMessage) // 检查地址是否相等
            text = aMessage.text;
        return *this; // 返回第一个操作数的引用
    }

    // CMessage 对象的移动赋值运算符
    CMessage& operator=(CMessage&& aMessage)
    {
        cout << "CMessage move assignment operator function called." << endl;
        text = std::move(aMessage.text);
        return *this; // 返回第一个操作数的引用
    }

    // 构造函数定义
    CMessage(const char* str = "Default")
    {
        cout << "CMessage constructor called." << endl;
        text = CText(str);
    }

    // 拷贝构造函数定义
    CMessage(const CMessage& aMessage)
    {
        cout << "CMessage copy constructor called." << endl;
        text = aMessage.text;
    }

    // 移动构造函数
    CMessage(CMessage&& aMessage)
    {
        cout << "CMessage move constructor called." << endl;
        text = std::move(aMessage.text);
    }

    // 析构函数
    ~CMessage()
    {
        cout << "CMessage destructor called." << endl;
    }
};
```

# 第 8 章更多关于类

```cpp
CMessage motto3(motto1+motto2);
cout << " Done!!" << endl << endl << " " << motto3 << " contains - ";
motto3.ShowIt();
CMessage motto4;
cout << endl << " Executing: motto4 = motto3 + motto2;" << endl;
motto4 = motto3 + motto2;
cout << " Done!!" << endl << endl << " " << motto4 << " contains - ";
motto4.ShowIt();
cout << endl;
return 0;
```

## 工作原理

在 `main()` 函数中，相对较少的语句包含了大量内容。我将只讨论有趣的部分。让我们先考虑以下语句产生的输出：

```cpp
CMessage motto3(motto1+motto2);
```

输出看起来如下：

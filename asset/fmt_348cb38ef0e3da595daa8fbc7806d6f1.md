
将此头文件添加到项目 `Ex9_01` 中。你需要 `Box.h` 文件的 `#include` 指令，因为你在代码中引用了 `CBox`。如果你漏掉这一项，编译器将不知道 `CBox`，因此代码将无法编译。基类名 `CBox` 出现在派生类名 `CCandyBox` 之后，并用冒号与其隔开。在所有方面，它看起来像一个普通的类。你添加了新成员 `m_Contents`，因为它是指向字符串的指针，所以你需要一个构造函数来初始化它，一个析构函数来释放字符串内存。你为描述 `CCandyBox` 对象的字符串提供了一个默认值。

注意你在第 6 章中看到的 `strcpy()` 函数的使用。它有三个参数——拷贝操作的目的地、源以及……（注：原文此处为三个，但实际通常为两个，此处按原文逻辑翻译或保留原文）：拷贝操作的目的地、源。

## 尝试使用派生类

在你看到类定义如何表示这一点之前，请将以下代码添加到 `Ex9_01.cpp`：

```cpp
// Ex9_01.cpp
// 使用派生类
#include <iostream>
#include "Box.h"
using std::cout;

int main() {
    CBox myBox(4.0, 3.0, 2.0); // 创建 CBox 对象
    CCandyBox myCandyBox("Wafer"); // 创建 CCandyBox 对象

    cout << "myBox occupies " << sizeof(myBox) << endl;
    cout << "myCandyBox occupies " << sizeof(myCandyBox) << endl;
    cout << "myMint occupies " << sizeof(myMint) << endl;

    // myBox.m_Length = 10.0; // 取消注释此处会导致错误
    cout << "myLength is " << myBox.m_Length << endl;

    return 0;
}
```

## 如何工作

你已经看到基成员在派生类中是如何继承的。查看输出：

```
myBox occupies 24 bytes
myCandyBox occupies 32 bytes
myMint occupies 32 bytes
myLength is 4
```

第一行正如你在上一章讨论中所预期的。`CBox` 对象有三个 `double` 成员，每个 8 字节，总共 24 字节。`CCandyBox` 对象都是 32 字节。字符串的长度不会影响对象的大小，因为持有字符串的内存是单独分配的。32 字节是由继承自基类 `CBox` 的 24 字节成员、指针成员 `m_Contents` 的 4 字节组成的，另外 4 字节从哪里来？这是由于编译器在 8 字节倍数的地址处添加额外的内存。你可以通过在 `CCandyBox` 中添加一个 `int` 类型的成员来演示这一点。你会发现类的大小仍然是 32 字节。

你还输出了 `CBox` 对象的 `m_Length` 成员的值。尽管访问它没有困难，但如果你取消注释 `main` 函数中的语句：

```cpp
// myBox.m_Length = 10.0; // 取消注释此处会导致错误
```

程序将不再编译。编译器产生以下消息：

```
error C2247: 'CBox:m_Length' not accessible because 'CCandyBox'
uses 'private' to inherit from 'CBox'
```

它明确指出来自基类的 `m_Length` 成员不可访问的，因为 `m_Length` 在派生类中是私有的。这是因为在定义派生类时，基类的默认访问说明符是 `private`——就好像派生类定义的第一行是：

```
class CCandyBox: private CBox
```

基类总是有一个访问说明符来决定所继承成员的状态。如果你省略了基类的访问说明符，编译器会假设它是私有的。如果你将 `CandyBox.h` 中 `CCandyBox`类的定义更改如下，

## 继承中的访问控制

```cpp
class CCandyBox: public CBox {
public:
    char* m_Contents;

    explicit CCandyBox(const char* str = "Candy") // 构造函数
    {
        m_Contents = new char[strlen(str) + 1];
        strcpy_s(m_Contents, strlen(str) + 1, str);
    }

    ~CCandyBox() // 析构函数
    delete[] m_Contents;
};
```

成员 `m_Length` 在派生类中以 `public` 形式继承，可以在函数 `main()` 中访问。由于基类使用了访问限定符 `public`，基类中被指定为 `public` 的所有继承成员在派生类中具有相同的访问级别。

## 继承中的访问控制

需要更仔细地查看派生类中继承成员的访问情况。考虑基类的私有成员在派生类中的状态。

在之前的示例中，考虑具有公共数据成员的 `CBox` 类是有充分理由的，而不是后期更安全的具有私有数据成员的版本。虽然基类的私有成员也是派生类的成员，但它们在派生类中对于基类仍然是私有的，因此派生类中定义的成员函数无法访问它们。它们只能通过基类中非 own成员函数在派生类中访问。你可以轻松地将 `CBox` 数据成员更改为 `private`，并在派生类 `CCandyBox` 中放入 `Volume()` 函数来演示这一点，使得类定义如下：

```cpp
//无法编译的类版本
#include <string> // 用于 strlen() 和 strcpy()
class CBox {
public:
    explicit CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0):
        m_Length(lv), m_Width(wv), m_Height(hv) {}

private:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

```cpp
class CCandyBox : public CBox
{
public:
    char* m_Contents;

    // 计算 CCandyBox 对象体积的函数
    double Volume() const // 错误 - 成员不可访问
    { return m_Length*m_Width*m_Height; }

    explicit CCandyBox(const char* str = "Candy") // 构造函数
    {
        m_Contents = new char[strlen(str) + 1];
        strncpy(m_Contents, str, strlen(str) + 1);
    }

    ~CCandyBox() // 析构函数
    {
        delete[] m_Contents;
    }
};
```

使用这些类的程序无法编译。`CCandyBox` 中的 `Volume()` 函数尝试访问基类的私有成员，这是不合法的，因此编译器将为每个实例标记错误号 C2248。

## 尝试访问基类的私有成员

然而，使用基类中的 `Volume()` 函数是合法的，因此，如果你将 `Volume()` 函数的定义移动到基类 `CBox` 的 `public` 部分，程序不仅可以编译，你还可以使用该函数获取 `CCandyBox` 对象的体积。创建一个新的 Win32 项目 `Ex9_02`，`CBox.h` 的内容如下：

```cpp
// Ex9_02 中的 Box.h
#pragma once
class CBox
{
public:
    explicit CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0)
    : m_Length(lv), m_Width(wv), m_Height(hv) {}

    // 计算 CBox 对象体积的函数
    double Volume() const
    { return m_Length*m_Width*m_Height; }

private:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

项目中的 `CandyBox` 头文件包含：

```cpp
// 项目 Ex9_02 中的 CandyBox.h
#pragma once
#include "Box.h"
#include <string> // 用于 strlen() 和 strcpy()

class CCandyBox: public CBox{
public:
    char* m_Contents;

    explicit CCandyBox(const char* str = "Candy") // 构造函数
    {
        m_Contents = new char[strlen(str) + 1];
        strncpy(m_Contents, str, strlen(str) + 1);
    }

    ~CCandyBox()                                      // 析构函数
    { delete[] m_Contents; };
};
```

项目中的 `Ex9_02.cpp` 文件：

```cpp
// Ex9_02.cpp
// 使用从基类继承的函数
#include <iostream>                                用于流输出
#include "CandyBox.h"                              // 用于 CBox 和 CCandyBox
using std::cout;
using std::endl;

int main() {
    CBox myBox(4.0,3.0,2.0);                          // 创建 CBox 对象
    CCandyBox myMintBox;
    CCandyBox myMintBox("Wafer Thin Mints");         // 创建 CCandyBox 对象

    cout << endl;
    cout << "myBox occupies " << sizeof(myBox)      // 显示占用多少内存
    cout << " bytes: " << endl;
    cout << "myMintBox occupies " << sizeof(myMintBox)// 显示占用多少内存
    cout << " bytes: " << endl;
    cout << "myMintBox volume is " << myMintBox.Volume(); // 获取体积
    return 0;
}
```

### 452 | 第 9 章 类继承与函数

对于 `iostream` 头文件的 `#include` 指令和两个声明并不是严格必要的，因为 `Box.h` 包含了相同的代码，但将它们放在在这里也没有坏处。相反，将语句放在这里意味着意味着如果你因为不再需要而从 `Box.h` 中移除这些代码，`CandyBox.h` 仍然可以编译。

`Ex9_03.cpp` 的内容如下：

```cpp
// Ex9_03.cpp
// 从派生类构造函数调用基类构造函数
#include <iostream>               // 用于流 I/O
#include "CandyBox.h"             // 用于 CBox 和 CandyBox
using std::cout;
using std::endl;

int main() {
    CBox myBox(4.0, 3.0, 2.0);
    CandyBox myCandyBox;
    CandyBox myMintBox(1.0, 2.0, 3.0,"Wafer Thin Mints");

    cout << " " << sizeof(myBox) // 显示占用多少内存
         << " bytes" << endl; // 对象所需的字节
    cout << "CandyBox occupies " << sizeof(myCandyBox)
         << " bytes" << endl;
    cout << "MyMintBox occupies " << sizeof(myMintBox)
         << " bytes" << endl;
    cout << "MyMintBox volume: " // 获取 CandyBox
         << endl; // 对象的体积
    return 0;
}
```

## 工作原理

正如向派生类添加构造函数一样，你在每个构造函数中都添加了输出语句，以便知道它们中一个何时被调用。显式的 `CBox` 构造函数出现在派生类函数头部的冒号之后。这种符号与你一直用于在构造函数初始化成员的符号完全相同：

```cpp
// 调用基类构造函数
explicit CCandyBox(double lv, double wv, double hv, const char* str="Candy") :
{
CBox(lv, wv, hv);
}
```

这与你在这里的操作完全一致，因为你本质上是在初始化派生类的 `CBox` 子对象。在第一种情况下，你显式地调用了 `double` 成员 `m_Length`、`m_Width` 和 `m_Height` 的默认构造函数。在第二情况下，你调用了 `CBox` 的构造函数。这导致你选择的特定 `CBox` 构造函数在执行 `CCandyBox` 构造函数代码之前调用。

如果你构建并运行此示例，将产生以下输出：

```
CBox constructor called
CBox constructor called
CCandyBox constructor1 called
CBox constructor called
CCandyBox constructor2 called
myBox occupies 24 bytes
myCandyBox occupies 32 bytes
myMintBox occupies 32 bytes
myMintBox volume is 6
```

调用情况在下表中解释：

| 屏幕输出 | 正在构造的对象 |

|---|---|

| CBox constructor called | myBox |

| CBox constructor called | myCandyBox |

| CCandyBox constructor1 called | myCandyBox |

| CBox constructor called | myMintBox |

| CCandyBox constructor2 called | myMintBox |

第一行输出源于 `CBox` 类构造函数的调用，它源于 `CBox` 对象 `myBox` 的声明。第二行输出源于声明 `CCandyBox` 对象 `myCandyBox` 时引起的基类构造函数的自动调用。

注意基类构造函数总是在派生类之前被调用的。基类是构建派生类的基础，因此必须先创建基类。

下一行源于你为 `myMintBox` 对象调用了你版本的默认类构造函数。该构造函数被调用是因为对象没有被初始化。第四行输出源于在我们为 `CCandyBox` 对象编写的新构造函数中显式指定了要调用的 `CBox` 类。为 `CCandyBox` 对象维度指定的参数值被传递给基类构造函数。接下来是派生类构造函数本身的输出，因此构造函数再次调用基类，然后是派生类。

从你到目前为止所看到的内容可以清楚地看出，当执行类构造函数时，始终会调用基类构造函数来构造派生类的基部分。如果你不指定要使用的基类构造函数，编译器将安排调用默认基类构造函数。表格中的最后一行显示 `myMintBox` 对象基部分的初始化正在正常工作，私有成员已由 `CBox` 类构造函数初始化。

基类的私有成员仅对基类的成员函数可见，这并不方便。在许多情况下，你可能希望从派生类内部访问基类的私有成员。正如你现在可能预料的那样，C++ 提供了一种实现此方法。

## 声明保护的类成员

除了类成员的 `public`（公共）和 `private`（私有）访问限定符外，你还可以将成员声明为 `protected`（保护的）。`protected` 关键字与 `private` 类似，但它允许派生类访问这些成员。正如你现在可能已经预料的那样，C++ 提供了一种实现此方法。由于 `protected` 关键字与 `private` 类似，但它允许派生类访问这些成员。

你可以从派生类内部访问基类的保护成员，如下所示：



为类及其中定义的所有方法的原型。它是对类的描述，通常不包含可执行代码。例如，下面是 C++ 类 PlainBox 的头文件：

```
/* @file PlainBox.h */
#include <string> // Needed because we use string objects.
using namespace std; // Strings are part of the system std library.
class PlainBox // This is a class declaration for PlainBox.
{
private: // Items defined below have private access.
    string item;
public: // Items defined below have public access.
    // Prototypes for constructors and methods.
    PlainBox();
    PlainBox(string theItem);
    void setItem(string theItem);
    string getItem();
}; // end PlainBox - Note semicolon after declaration.
```

请注意，每个数据成员和方法不需要具有访问修饰符。私有数据成员和方法被分组在一起，公共方法也彼此分组。每个访问修饰符后跟一个冒号。可以有多个 private、protected 或 public 部分，但这并不常见。类声明必须在右花括号后以分号结束，如上所示。

类的实现文件（或源文件）通常与头文件同名，但以 .cpp 结尾以指示它是 C++ 文件。实现文件包含随附头文件中声明的方法的定义。下面是 C++ 类 PlainBox 的实现文件：

```
/* @file PlainBox.cpp */
#include "PlainBox.h" // We need to tell the compiler about our data fields and methods.
PlainBox::PlainBox()
{
} // end default constructor
PlainBox::PlainBox(string theItem)
{
    item = theItem;
} // end constructor
void PlainBox::setItem(string theItem)
{
    item = theItem;
} // end setItem
string PlainBox::getItem()
{
    return item;
} // end getItem
```

此实现文件首先包含头文件，以便编译器拥有类声明并了解该类的数据字段和方法。然后我们定义每个方法。在实现文件中，没有用一组大括号括起来的“主”方法。每个方法都单独定义。为了让编译器知道某个方法属于 PlainBox 类，我们在方法名前添加了前缀 PlainBox::。请注意，前缀位于方法返回类型之后。前缀只是方法名称的扩展。

要在 Java 中创建 PlainBox 对象，可以使用以下语句：

```
PlainBox myBox = new PlainBox("Jewelry");
```

C++ 也提供了几种创建对象的形式：

```
PlainBox myBox = PlainBox("Jewelry");
PlainBox myBox("Jewelry");
```

这些语句在 C++ 中是等价的，并创建一个局限于创建它的函数或方法的 PlainBox 对象。在这些示例中未使用 C++ 关键字 new。

下面的示例使用关键字 new 创建一个 PlainBox 对象，该对象将一直存在，直到程序员专门将其删除：

```
PlainBox *someBoxPtr = new PlainBox("Jewelry");
```

语法与 Java 非常相似，只是 PlainBox 后面跟有 * 字符。* 表示 someBoxPtr 是指向 PlainBox 对象的指针，而不是对象本身。指针在 C++ Interlude 2 中有更详细的讨论。

如果在 C++ 中使用 new 运算符（如上例所示）实例化对象，则程序员有责任在不再需要该对象时将其从内存中删除，因为 C++ 不提供垃圾回收。要删除 someBoxPtr 指向的对象，请使用以下语句：

```
delete someBox; // Frees memory used by the object.
someBox = nullptr; // A safety precaution.
```

每次使用 new 运算符创建对象时，都必须编写相应的 delete 运算符来释放对象的内存。否则，您的应用程序会出现内存泄漏。

### K.5 基本输入和输出

虽然在系统级别，Java 和 C++ 对键盘输入和控制台显示输出的处理相似，但用于完成这些任务的高级结构差异很大。

要让 Java 应用程序接受来自键盘的输入，请使用 System.in 创建一个 Scanner 对象并使用它来接受用户的输入。向显示器输出是通过调用 System.out 对象的 print 或 println 方法来完成的。以下代码创建一个 Scanner 对象，为用户显示提示，接受用户的响应，并将响应回显给用户：

```
Scanner keyboard = new Scanner(System.in);
System.out.print("How many apples are in a box? ");
int applesPerBox = keyboard.nextInt();
System.out.println("You entered " + applesPerBox + " apples per box. ");
```

C++ 没有 System.in 或 System.out 对象；相反，您分别使用 cin 和 cout 对象进行键盘输入和控制台显示输出。要使用 cin 和 cout，请在程序开头包含以下语句：

```
#include <iostream>
using namespace std;
```

以下 C++ 语句与前面的 Java 语句等效：

```
cout << "How many apples are in a box? ";
int applesPerBox = 0;
cin >> applesPerBox;
cout << "You entered " << applesPerBox << " apples per box. " << endl;
```

请注意使用输出流运算符 << 将字符串字面量和变量发送到输出对象 cout。同样，输入流运算符 >> 将来自输入对象 cin 的输入发送到变量。如果将它们想象成指向数据流方向的箭头，就很容易记住使用哪个运算符。

常量 endl 在 iostream 中定义，表示换行符。有关 iostream 库以及 C++ 中基本输入和输出的更多信息，请参见附录 A 的第 A.2 节。

## 面向 Python 程序员的 C++

## 目录

- L.1 一般概念 789
- L.2 语言元素比较 790
- L.3 函数 792
- L.4 类 793

本附录介绍了初学者可能遇到的 Python 与 C++ 之间的一些差异。虽然还有许多其他差异，但它们要么不适用于本教材中使用的代码和示例，要么在需要时会加以说明。本附录应与附录 A 一起使用，以充分了解 C++ 提供的功能。

### L.1 一般概念

从 Python 编程语言转到 C++ 类似于高中毕业并接受军事基础训练。Python 是一种弱类型、解释型语言，具有可读的语法。另一方面，C++ 是一种强类型、编译型语言，其语法遵循严格的标点规则。好消息是，完成新兵训练后，你有机会成为陆军游骑兵或海军海豹突击队员。本教材可以帮助你成为一名出色的计算机科学家和 C++ 程序员。

Python 程序是解释执行的，可以在任何安装了 Python 解释器的计算机上运行。Python 解释器甚至已用 JavaScript 编写，因此您可以在 Web 浏览器窗口中运行 Python 代码！另一方面，C++ 程序被编译为特定于操作系统的目标代码。这意味着您需要为希望程序运行的每个操作系统重新编译 C++ 代码。本书中的代码遵循最近的 ANSI/ISO C11 标准，因此如果您的编译器支持该标准，您应该能够在所选的任何操作系统上编译和运行程序。

### L.2 语言元素比较

在编写 C++ 程序时，有几个重要的差异需要牢记。

**注释。** 注释是任何程序的重要组成部分，C++ 支持使用不同分隔符的单行和多行注释：

```
// This is a comment that appears on its own line.
int sum = 0; // This is a comment that appears within a C++ statement.
/* The following comment begins with /* and ends with */.
/** This is a special multiline comment used for documentation systems
such as doxygen. See Appendix I for details. */
// The following comment begins with // and ends with /.
/* This is a multiline comment that is often used to temporarily
disable a group of statements during debugging. */
```

**语句。** C++ 中的空白和缩进没有意义。C++ 语句以分号结束。块（称为复合语句）中的语句类似于 Python 中的套件，并由大括号 { } 分组在一起。

**变量。** 在 Python 中，变量一旦赋值即可使用。C++ 中的变量必须在使用前声明并指定类型。虽然 C++ 编译器不要求这样做，但变量在使用前也应赋予初始值。一旦变量以给定类型声明，它在声明所在的作用域内始终保持该类型。

**关系运算符。** C++ 中的变量一次只能与一个关系运算符一起使用。Python 表达式如 5 < x < 10 必须在 C++ 中写为 (5 < x) && (x < 10)。运算符 && 用于逻辑 AND，|| 用于逻辑 OR。

**谓词表达式。** 条件和迭代流程控制语句中的谓词表达式必须放在括号中。

**赋值语句。** C++ 不允许多重赋值。无法使用 x, y = 5, 6 这样的 Python 语句。

**迭代语句。** C++ 有 while 语句，其行为类似于 Python 的 while 语句。C++ 的 for 语句是 while 语句的一种特例。要像使用 Python for 语句一样使用 C++ for 语句，必须使用迭代器，这些迭代器将在 C++ Interlude 6 中解释。C++ 有 do-while 语句，这是一种后测试循环。Python 没有等效语句。

**基本输入和输出。** 在 Python 应用程序中，您使用 raw_input 函数接受来自键盘的输入。该函数返回一个字符串。如果需要整数或其他数据类型的值，必须使用另一个函数将字符串转换为所需的输入。向显示器输出是通过调用 print 函数来完成的。例如，以下 Python 代码为用户显示提示，接受作为整数的响应，并将响应回显给用户：

```
userNumber = int (raw_input ("How many apples are in a box? "))
print "You entered %d apples per box."%(userNumber)
```

C++ 分别使用 cin 和 cout 两个对象进行键盘输入和控制台显示输出。要使用 cin 和 cout，应在程序开头包含以下语句：

```
#include <iostream>
using namespace std;
```


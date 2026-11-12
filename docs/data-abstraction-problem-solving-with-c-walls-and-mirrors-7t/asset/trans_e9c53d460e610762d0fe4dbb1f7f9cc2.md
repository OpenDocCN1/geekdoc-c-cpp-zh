

以下 C++ 语句与前面的 Python 语句等价：

```
cout << "How many apples are in a box? ";
int applesPerBox = 0;
cin >> applesPerBox;
cout << "You entered " << applesPerBox << " apples per box." << endl;
```

注意输出流运算符 << 的用法，用于将字符串字面量和变量发送到输出对象 cout。同样，输入流运算符 >> 用于将输入对象 cin 的输入发送到变量。如果将它们想象为指向数据流方向的箭头，就很容易记住使用哪个运算符。

常量 endl 在 iostream 中定义，表示换行符。有关 iostream 库和 C++ 中基本输入和输出的更多信息，请参见附录 A 的第 A.2 节。

示例。清单 L-1 给出了一个使用刚才讨论的语句和表达式的简短交互式 Python 程序。清单 L-2 显示了等效的 C++ 程序。C++ 程序从 main 函数开始执行。在这个示例中，你也可以看到用户输入和输出的一些差异。

```
LISTING L-1 Short Python program to test and modify a user-entered value

small, large = 1, 1000
print "Your number was between %d and %d large."%(small, large)
userNumber = int (raw_input ("Enter something: "))
if small < userNumber < large :
    print "Your number was between %d and %d large."%(small, large)
elif userNumber < small :
    while userNumber <= small :
        userNumber = userNumber + 1
else :
    while True :
        userNumber = userNumber - 1
        if userNumber < 1000 :
            break
        print "I fixed your number to be between %d and %d!"%(small, large)
```

```
LISTING L-2 Short C++ program equivalent to the Python program in Listing L-1.

#include <iostream>
using namespace std;
int main()
{
    int small = 1;
    int large = 1000;
    int userNumber = 0;
    cout << "Enter something: ";
    cin >> userNumber;
if ( (small < userNumber) && (userNumber < large) )
{
    cout << "Your number was between " << small << " and ";
    cout << large << endl;
}
else if (userNumber < 1)
{
    while (userNumber <= 1)
    {
        userNumber++;
    }
}
else
{
    do
    {
        userNumber--;
    } while (userNumber >= 1000);
    cout << "I fixed your number to be between " << small << " and ";
    cout << large << endl;
}
```

## L.3 函数

与变量一样，C++ 函数是强类型的。定义 C++ 函数时，参数会被赋予类型。如果函数返回值，函数必须指明返回值的类型。这些信息在函数的头部（即第一行）中给出。如果函数不返回值，其返回类型为 void。函数定义紧随头部之后，并用 { } 括起来，与其他 C++ 块一样。

以下是一个计算其单个参数立方的简短 Python 函数：

```
def realCube(x) :
    return x * x * x
```

以下是等效的 C++ 函数：

```
double realCube(double x)
{
    return x * x * x;
}
```

请注意，函数及其参数都被赋予了类型。C++ 函数将在附录 A 的第 A.2 节中更详细地讨论。

文件中在 realCube 之后定义的任何函数都可以调用 realCube。但是，如果一个函数在 realCube 之前定义并且需要调用它，该怎么办？在这种情况下，编译器会发出错误，指出 realCube 未定义。C++ 要求每个函数、常量、变量或类在被调用之前必须先定义。

在只有少数函数的简单程序中，很容易对函数定义进行排序，以便编译器在遇到函数调用之前看到每个定义。在更复杂的程序中，要做到这一点更加困难，甚至不可能。但是，编译器在处理对函数的调用之前只需要函数的头部，而 C++ 提供了一种方法让你满足编译器的要求。你只需在调用函数的程序开头写出函数的头部，后面跟一个分号——即其原型。例如，函数 realCube 的原型是

```
double realCube(double x);
```

然后你可以将函数定义放在程序中的任何位置。

在较大的程序中，函数原型被放入一个或多个头文件中，如附录 K 的第 K.1 节所述。然后你将头文件包含到程序中。原型在类的创建中也很重要，如下一节所示。附录 A 的第 A.8.1 节也讨论了头文件。

请注意，你可以将函数作为参数传递给另一个函数或方法。这在第 15 章的第 15.2.1 节中讨论。

## L.4 类

Python 类允许类的客户端访问所有数据字段和方法。在 C++ 中，这称为**公共访问**，且仅推荐用于方法。在 Python 中，当你创建一个仅供类方法使用的类成员时，通常会在成员名称前加上两个下划线 __ 。这只是对程序员的一个信号；Python 解释器不会强制执行此约定。C++ 允许类设计者通过将某些数据字段和方法标记为**私有**来限制对它们的访问，编译器通过仅允许类方法访问私有成员来强制执行此限制。

C++ 中的类具有构造函数，类似于 Python 类中的 __init__ 方法。

在 Python 类中编写方法时，你会在数据字段名称前加上 self 以指示它们是类的实例变量。如果在类的方法内部引用，C++ 类中的实例变量不需要特殊前缀。

以下是一个简单的 Python 类 PlainBox：

```
class PlainBox
    def __init__(self, theItem):
        self.item = theItem

    def setItem(self, theItem):
        self.item = theItem

    def getItem(self) :
        return self.item
```

你也可以以更接近 C++ 类的形式定义同一个类：

```
class PlainBox
    __item = ""

    def __init__(self, theItem):
        self.__item = theItem

    def setItem(self, theItem):
        self.__item = theItem

    def getItem(self) :
        return self.__item
```

虽然可以在 C++ 的单个文件中定义类，但我们将使用两个文件，因为这是一种更常见且更灵活的方法。第一个文件是类头文件；它包含类的数据字段以及类中定义的所有方法的原型。它是类的描述，通常不包含可执行代码。例如，以下是前一个 Python 类的 C++ 版本的头文件：

```
/* @ file PlainBox.h */
#include <string> // Needed because we use string objects.
using namespace std; // Strings are part of the system std library.
class PlainBox // This is a class declaration for PlainBox.
{
private: // Items defined below have private access.
string item; // Items defined below have public access.
public: // Prototypes for constructors and methods:
PlainBox();
PlainBox(string theItem);
void setItem(string theItem);
string getItem();
}; // end PlainBox - Note semi-colon after declaration.
```

请注意，每个数据成员和方法不需要带有访问修饰符。私有数据成员和方法被分组在一起，公共方法彼此分组。每个访问修饰符后面跟一个冒号。可以有多个私有、受保护或公共节，但这并不常见。类声明必须在右花括号后以分号结束，如上所示。

类的实现文件（或源文件）通常与头文件同名，但以 .cpp 结尾以表明它是 C++ 文件。实现文件包含随附头文件中声明的方法的定义。以下是 C++ 类 PlainBox 的实现文件：

```
/* @ file PlainBox.cpp */
#include "PlainBox.h" // We need to tell the compiler about our data
// fields and methods.
PlainBox::PlainBox()
{ // end default constructor
PlainBox::PlainBox(string theItem)
{ // end constructor
void PlainBox::setItem(string theItem)
{ // end setItem
string PlainBox::getItem()
{ return item;
} // end getItem
```


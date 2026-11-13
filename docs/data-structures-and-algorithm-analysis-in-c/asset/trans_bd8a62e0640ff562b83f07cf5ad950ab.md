

## explicit Constructor

IntCell 构造函数是显式的。你应该将所有单参数构造函数声明为显式的，以避免幕后的类型转换。否则，有一些宽松的规则会允许在没有显式转换操作的情况下进行类型转换。通常，这是不希望的行为，它破坏了强类型，并可能导致难以查找的错误。作为示例，请考虑以下内容：

```
IntCell obj;    // obj is an IntCell
obj = 37;       // Should not compile: type mismatch
```

上面的代码片段构造了一个 IntCell 对象，然后执行一条赋值语句。但是赋值语句不应该工作，因为赋值运算符的右侧不是另一个 IntCell。相反，应该使用 obj 的 write 方法。但是，C++ 有宽松的规则。通常，单参数构造函数定义了一个隐式类型转换，其中创建一个临时对象，使赋值（或函数参数）兼容。在这种情况下，编译器会尝试转换

```
obj = 37;       // Should not compile: type mismatch
```

转换为

```
IntCell temporary = 37;
obj = temporary;
```

请注意，临时对象的构造可以使用单参数构造函数来执行。使用 explicit 意味着单参数构造函数不能用于生成隐式临时对象。因此，由于 IntCell 的构造函数被声明为 explicit，编译器将正确地抱怨存在类型不匹配。

## Constant Member Function

检查但不更改其对象状态的成员函数是访问器。更改状态的成员函数是修改器（因为它会改变对象的状态）。例如，在典型的集合类中，isEmpty 是访问器，而 makeEmpty 是修改器。

在 C++ 中，我们可以将每个成员函数标记为访问器或修改器。这样做是设计过程的重要组成部分，不应被视为仅仅是注释。事实上，有重要的语义后果。例如，修改器不能应用于 const 对象。默认情况下，所有成员函数都是修改器。要使成员函数成为访问器，必须在结束参数类型列表的右括号后添加关键字 const。const 属性是签名的一部分。const 可以有多种不同的含义。函数声明可以在三种不同的上下文中使用 const。只有右括号后的 const 表示访问器。其他用法在 1.5.3 节和 1.5.4 节中描述。

在 IntCell 类中，read 显然是访问器：它不会更改 IntCell 的状态。因此，它在第 9 行被设为常量成员函数。如果成员函数被标记为访问器，但其实现更改了任何数据成员的值，则会生成编译器错误。3

## 1.4.3 接口与实现分离

图 1.6 中的类包含所有正确的语法结构。但是，在 C++ 中，更常见的是将类接口与其实现分开。接口列出类及其成员（数据和函数）。实现提供函数的实现。

图 1.7 显示 IntCell 的类接口，图 1.8 显示实现，图 1.9 显示使用 IntCell 的 main 例程。接下来是一些重要要点：

## 预处理器命令

接口通常放在以 .h 结尾的文件中。需要了解接口的源代码必须 #include 接口文件。在我们的情况中，这既是实现文件，也是包含 main 的文件。偶尔，复杂的项目会有文件包含其他文件，并且存在在编译文件过程中接口可能被读取两次的危险。这可能是非法的。为了防止这种情况，每个头文件在读取类接口时都使用预处理器定义一个符号。这在图 1.7 的前两行中显示。符号名称 IntCell_H 不应出现在任何其他文件中；通常，我们从文件名构造它。接口文件的第一行

```
1 #ifndef IntCell_H
2 #define IntCell_H
3
4 /**
5 * A class for simulating an integer memory cell.
6 */
7 class IntCell
8 {
9 public:
10 explicit IntCell( int initialValue = 0 );
11 int read( ) const;
12 void write( int x );
13
14 private:
15 int storedValue;
16 };
17
18 #endif
```

**图 1.7** 文件 IntCell.h 中的 IntCell 类接口

3 数据成员可以标记为 mutable，以指示 const 属性不应应用于它们。

```cpp
#include "IntCell.h"
/**
 * Construct the IntCell with initialValue
 */
IntCell::IntCell( int initialValue ) : storedValue{ initialValue }
{
}
/**
 * Return the stored value.
 */
int IntCell::read( ) const
{
    return storedValue;
}
/**
 * Store x.
 */
void IntCell::write( int x )
{
    storedValue = x;
}
```

**图 1.8** 文件 IntCell.cpp 中的 IntCell 类实现

```cpp
#include <iostream>
#include "IntCell.h"
using namespace std;

int main( )
{
    IntCell m;

    m.write( 5 );
    cout << "Cell contents: " << m.read( ) << endl;

    return 0;
}
```

**图 1.9** 文件 TestIntCell.cpp 中使用 IntCell 的程序

测试符号是否未定义。如果是，我们可以处理该文件。否则，我们不处理该文件（通过跳转到 #endif），因为我们知道已经读取过该文件。

## 作用域解析运算符

在实现文件中（通常以 .cpp、.cc 或 .c 结尾），每个成员函数必须标识它所属的类。否则，将假设该函数在全局作用域中（并会导致无数错误）。语法是 ClassName::member。:: 称为作用域解析运算符。

## 签名必须完全匹配

已实现成员函数的签名必须与类接口中列出的签名完全匹配。请记住，成员函数是访问器（通过末尾的 const）还是修改器是签名的一部分。因此，例如，如果图 1.7 和 1.8 中 read 的签名恰好有一个省略了 const，就会导致错误。请注意，默认参数仅在接口中指定。在实现中省略它们。

## 对象声明如同原始类型

在经典 C++ 中，对象声明就像原始类型一样。因此，以下是 IntCell 对象的合法声明：

```
IntCell obj1; // Zero parameter constructor
IntCell obj2( 12 ); // One parameter constructor
```

另一方面，以下是不正确的：

```
IntCell obj3 = 37; // Constructor is explicit
IntCell obj4( ); // Function declaration
```

obj3 的声明是非法的，因为单参数构造函数是 explicit 的。否则它是合法的。（换句话说，在经典 C++ 中，使用单参数构造函数的声明必须使用括号来表示初始值。）obj4 的声明表明它是一个函数（在其他地方定义），不带参数并返回一个 IntCell。

obj4 的混淆是使用花括号的统一初始化语法的原因之一。在构造函数初始化列表（图 1.6，第 8 行）中用零参数初始化需要带有无参数的括号，但相同的语法在其他地方（对于 obj4）是非法的，这很丑陋。在 C++11 中，我们可以改为编写：

```
IntCell obj1; // Zero parameter constructor, same as before
IntCell obj2{ 12 }; // One parameter constructor, same as before
IntCell obj4{ }; // Zero parameter constructor
```

obj4 的声明更好，因为用零参数构造函数初始化不再是特殊语法案例；初始化风格是统一的。

```
#include <iostream>
#include <vector>
using namespace std;

int main( )
{
    vector<int> squares( 100 );

    for( int i = 0; i < squares.size( ); ++i )
        squares[ i ] = i * i;

    for( int i = 0; i < squares.size( ); ++i )
        cout << i << " " << squares[ i ] << endl;

    return 0;
}
```

![](img/e449061a0cac9cafaefd979fab665b33_37_0.png)

## 1.4.4 vector 和 string

C++ 标准定义了两个类：vector 和 string。vector 旨在替换内置的 C++ 数组，后者带来无穷的麻烦。内置 C++ 数组的问题在于它不表现得像一等对象。例如，内置数组不能用 * 复制，内置数组不记得它可以存储多少项，并且其索引运算符不检查索引是否有效。内置字符串只是一个字符数组，因此具有数组的缺点再加上更多缺点。例如，== 不能正确比较两个内置字符串。

STL 中的 vector 和 string 类将数组和字符串视为一等对象。vector 知道它有多大。两个 string 对象可以用 ==、< 等进行比较。vector 和 string 都可以用 = 复制。如果可能，应避免使用内置的 C++ 数组和字符串。我们在第 3 章中讨论内置数组，以展示如何实现 vector。

vector 和 string 易于使用。图 1.10 中的代码创建一个存储一百个完全平方数的 vector 并输出它们。还要注意，size 是一个返回 vector 大小的方法。我们在第 3 章中探讨的 vector 的一个好特性是很容易更改其大小。在许多情况下，初始大小为 0，vector 会根据需要增长。

C++ 长期以来一直允许初始化内置 C++ 数组：

```
int daysInMonth[] = { 31, 28, 31, 30, 31, 30, 31, 30, 31, 30, 31 };
```

令人恼火的是，这种语法对 vector 不合法。在旧版 C++ 中，vector 要么用大小 0 初始化，要么可能通过指定大小来初始化。例如，我们会编写：


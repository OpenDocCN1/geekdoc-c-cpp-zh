

char MyName[];
cout << "a:" << a << endl;
cout << "b:" << b << endl;
cout << "Your name please:";
cin >> MyName;
cout << "Welcome dear " << MyName << " to the world of C++!";
}
Output:
a: 110
b: 0.11
Your name please: Saurabh
Welcome dear Saurabh to the world of C++!

关键字 cin 用于 C++ 中的输入。运算符 >> 用于分隔正在输入或输出的变量。空白字符用于分隔标准输入设备上对应不同变量的项目。C++ 为此目的重载了右移运算符 >>。它也称为输入运算符或提取运算符。程序代码 A.3 使用 cin 和 cout 从用户处接受两个整数，然后显示这两个输入数字的和。

```
//A sample C++ program for illustrating cin and cout
#include<iostream.h>
main()
{
int a, b;
cout << "Enter values of a & b:";
cin >> a >> b;
cout << a << " + " << b << " = " << a + b;
}
Output:
Enter values of a & b: 5 6
5 + 6 = 11
```

C++ 中 I/O 的一个优点是它是无格式的，也就是说，程序员不需要使用格式符号来指定正在输入或输出的项目的类型和顺序。与其他 C++ 运算符类似，I/O 运算符也可以被重载。

## A.3 C++ 中的函数

C++ 中有两种函数，即普通函数和成员函数。成员函数是与特定 C++ 类相关联的函数。这两种函数在所有特征上都相似，除了它们的作用域。

函数由函数名、参数列表（输入）、返回类型（输出）和函数体（实现函数的代码）组成。在程序代码 A.4 中，Max 是函数名，float a 和 float b 是参数列表，其中 float 是返回类型，{ 和 } 之间的语句构成函数体。同样，Square() 是一个以 int a 为参数、int 为返回类型的函数。这里，SayHello() 是另一个没有参数且不返回任何值的函数，因此其返回类型是 void。

```
PROGRAM CODE A.4
// A sample C++ program-function
void SayHello()
{
cout << "Hello, welcome to the world of C with classes";
}
int Square(int a)
{
return a * a;
}
float max(float a, float b)
{
if(a > b)
return a;
else
return b;
}
void main()
{
int x, y, z;
SayHello();
cout << endl;
cout << "Enter number";
cin >> x;
cout << "Square of " << x << " is " << Square(x);
cout << "\nEnter two integers";
cin >> y >> z;
cout << "Maximum between " << y << " and " << z << " is " << max(y, z);
}
Output:
Hello, welcome to the world of C with classes
Enter number 5
Square of 5 is 25
Enter two integers 9 4
Maximum between 9 and 4 is 9
```

C++ 中的所有函数都返回一个值。如果函数不打算返回任何内容，我们使用 void 来表示其返回类型。值通过使用 return 语句从函数返回。return 语句必须返回与函数返回类型相同类型的值，或者应将其转换为所需类型。当遇到 return 语句时，函数终止。通过提供实际参数来调用函数。一些示例如下：

- 对函数 max(55.23, 76.89) 的调用返回 76.89。
- 对函数 Square(5) 的调用返回 25。
- 对函数 SayHello 的调用显示消息“Hello, welcome to the world of C with classes”。

### A.3.1 内联函数

内联函数是通过在函数定义中添加关键字 inline 来声明的，如程序代码 A.5 所示。函数 PrintLine() 是一个内联函数，而函数 PrintLine(int n, char ch) 不是。

```
PROGRAM CODE A.5
// A sample C++ program-inline function
inline void PrintLine()
{
    cout << "---------";
    cout << endl;
}
void PrintLine(int n, char ch)
{
    for(i = 1; i <= n; i++)
        cout << ch;
    cout << endl;
}
// calling function
void main()
{
    PrintLine();
    PrintLine(10, 'S');
}
Output:
---------
SSSSSSSSSS
```

inline 关键字指示编译器，对内联函数 PrintLine() 的任何调用都必须由被调用函数的函数体替换。这消除了程序执行时执行函数调用和复制参数的开销。当成员函数在类定义内定义时，如程序代码 A.6 所示，它会自动成为内联函数。

inline 和 const 关键字的目的是避免使用 #define 等预处理器指令。该预处理器指令传统上用于执行宏替换。宏与函数类似，区别在于函数被调用而宏被替换。过度使用预处理器指令会使调试器和分析器（用于调试）等编程工具难以高效使用。

使用内联函数对于较短的代码是有益的。但是，由于内联函数调用被函数定义替换，这种展开会导致冗长函数的代码更大。在某些情况下，当函数是递归的或包含静态变量或循环、switch 或 goto 语句时，编译器可能会忽略将函数设为内联的要求。

```
PROGRAM CODE A.6
// A sample C++ program-inline function
#include<iostream.h>
class ABC
{
    int a, b, c;
public:
    void GetData()
    {
        cin >> a >> b >> c;
    }
};
void ABC :: ShowData()
{
    cout << a << "\t" << b << "\t" << c;
}
```

这里，ShowData() 是一个成员函数，其代码写在类定义之外。函数 GetData() 在类定义内部定义，因此被视为内联函数。如果用户希望在类外部定义函数，但仍希望将其设为内联函数，可以通过显式指示编译器来实现，如程序代码 A.7 所示。

```
PROGRAM CODE A.7

// A sample C++ program with inline function outside class
#include<iostream.h>
class ABC
{
    int a, b, c;
    public:
        void GetData()
        {
            cin >> a >> b >> c;
        }
};

inline void ABC :: ShowData()
{
    cout << a << "\t"<< b << "\t" << c;
}
```

我们已经讨论过，内联函数调用会被其代码替换，类似于宏展开。但是，内联函数与宏之间有一个主要区别。让我们考虑程序代码 A.8 中的代码。

```
PROGRAM CODE A.8

// A sample C++ program with macro and inline function
#include<iostream.h>
#define Square1(x) x * x
inline int Square2(int x)
{
    return x * x;
}
int main()
{
    cout << "\n Using macro" << Square1(5 + 5);
    cout << "\n Using inline function" << Square2(5 + 5);
}
Output:
Using macro 30
Using inline function 100
```

如果我们观察代码的输出，我们会发现预期的输出是由内联函数正确提供的，而不是由宏提供的。这一差异使得内联函数远优于宏。

## A.4 C++ 类和抽象数据类型

C++ 中的类是 C 语言 struct 表示法的自然演进。C++ 也有结构体的概念。C++ 中结构体和类的唯一区别是，默认情况下，类的成员是私有的，而结构体的成员是公有的。面向对象编程将数据（属性）和函数（行为）封装为称为类的包。

### A.4.1 类

类是一种用户定义的数据类型，其变量是对象。它使用关键字 class 创建。类类似于蓝图。根据蓝图，建造者可以建造一座或多座房屋。同样，根据类，程序员可以创建一个或多个对象。一个类可以被多次重用以创建同一类的许多对象。类使程序员能够建模具有某些属性（数据成员）和行为（操作）的对象。程序代码 A.9 给出了一个示例类定义。

```
// A sample C++ class definition
class Time
{
 private:
 int Hour;
 int Minute;
 int Second;
 public:
 Time();
 void SetTime(int, int, int);
 void DisplayTime();
};


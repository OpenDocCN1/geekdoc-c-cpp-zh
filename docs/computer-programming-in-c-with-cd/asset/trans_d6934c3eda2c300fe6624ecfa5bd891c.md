
**▶ 清单 7：在类外部创建内联函数**

```cpp
#include<iostream.h>

class MyClass
{
  int x,y,z;
  public:
  void getData();
  void displayData();
};
inline void MyClass :: getData()
{
  cout<<"Enter any two numbers";
  cin>>x>>y;
  z=x+y;
}
inline void MyClass :: displayData()
{
  cout<<"The sum of two numbers is="<<z<<endl;
}

int main()
{
  MyClass o;
  o.getData();
  o.displayData();
  return 0;
}
```

**输出：**

```text
Enter any two numbers19
26
The sum of two numbers is=45
```

在清单 7 中，MyClass 类的 getData() 和 displayData() 函数被定义为类规范之外的内联函数。这些函数的定义仅使用 inline 关键字。

在以下情况下，内联函数会被当作普通函数处理：

- 内联函数是递归函数。
- 内联函数包含静态变量。
- 内联函数包含 return 语句，且函数的返回类型为 void。请注意，返回类型为 void 的函数可以包含 return 语句，以将控制权转回调用函数。
- 内联函数包含循环结构、switch 或 goto 语句，并且会返回一个值。

现在让我们学习内联函数与宏之间的区别。

## 内联函数与宏之间的区别

与内联函数类似，宏是另一种使 C++ 程序紧凑的函数，但它本身由 C++ 编译器展开。宏包含一段代码序列，C++ 编译器会通过为程序生成实际的机器代码来替换它。使用宏的一个缺点是，与函数相比，它占用更多内存。然而，宏执行所需时间更少。

清单 8 展示了在类中使用宏以及内联函数（你可以在随书光盘的 code\chapter6 文件夹中的 MacroAndInline.cpp 文件里找到这个示例）：

**▶ 清单 8：在类中使用宏和内联函数**

```cpp
#include<iostream.h>

#define cube1(num) num*num*num        //Creating a macro
/* Creating an inline function */
inline int cube2(int x)
{
return (x*x*x);
}
int main()
{
cout<<"cube1 (5) ="<<cube1(5)<<endl;          //Calling macro
cout<<"cube1 (5+10) ="<<cube1(5+10)<<endl;    //Calling macro
cout<<"cube2 (5) ="<<cube2(5)<<endl;          //Calling inline function
cout<<"cube2 (5+10) ="<<cube2(5+10)<<endl;    //Calling inline function
return 0;
}
```

**输出：**

```text
cube1 (5) =125
cube1 (5+10) =115
cube2 (5) =125
cube2 (5+10) =3375
```

在清单 8 中，我们使用 #define 预处理指令创建一个宏 cube1；并使用 inline 关键字创建一个内联函数 cube2。在 main() 函数中，调用 cube1(5) 和 cube1(5+10) 宏分别显示结果为 125 和 115。然而，调用 cube2(5) 和 cube2(5+10) 内联函数分别显示结果为 125 和 3375。

请注意，cube1(5) 宏和 cube2(5) 内联函数的结果相同，都是 125。然而，cube1(5+10) 宏和 cube2(5+10) 内联函数的结果不同，分别是 115 和 3375。这是因为，cube1(5+10) 宏被求值为 5+10*5+10*5+10；而 cube2(5+10) 内联函数被求值为 15*15*15。

建议你使用内联函数而不是宏，原因如下：

- 宏的调用不执行类型检查；而内联函数的调用会执行类型检查
- 宏不能使用 return 关键字；而内联函数可以使用 return 关键字

![](img/8a6886c00caa6a1651a6c0e62bff341f_359_0.png)

> 什么是内联函数？讨论其优缺点。编写一个程序来演示内联函数（孟买大学，2008 年 12 月）

在解释了宏和内联函数之间的区别之后，让我们探讨类的构造函数和析构函数。

## 6.6 使用构造函数和析构函数

构造函数和析构函数是类的特殊成员函数，分别用于初始化或取消初始化类的成员变量。创建类的对象时，需要为该对象分配内存。然而，分配内存并不能确保对象内的成员变量被初始化。类的成员变量不能在声明类时初始化。例如，以下代码片段中成员变量的初始化是无效的：

```cpp
class GreatestNumber
{
  int variable=10;
  int variable=20;
};
```

通过在类中编写一个初始化函数，为每个成员变量赋予初始值，可以克服声明类时未初始化成员变量的问题。创建对象时可以调用这个初始化函数。清单 9 展示了一个初始化函数（你可以在随书光盘的 code\chapter6 文件夹中的 InitializeFunction.cpp 文件里找到这个示例）：

**▶ 清单 9：创建初始化函数**

```cpp
#include<iostream.h>

class GreatestNumber
{
  private:
    int variable1, variable2, variable3;
  public:
    void initialize();
    void greaterNum();
    void displayNum();
};
void GreatestNumber::initialize()
{
    variable1=10;
    variable2=20;
}
void GreatestNumber::greaterNum()
{
    if(variable1>=variable2)
        variable3=variable1;
    else
        variable3=variable2;
}
void GreatestNumber::displayNum()
{
    cout<<"The greatest number is:"<<variable3<<endl;
}

int main()
{
    GreatestNumber gnObject1;
    gnObject1.initialize();
    gnObject1.greaterNum();
    gnObject1.displayNum();
    return 0;
}
```

**输出：**

```text
The greatest number is:20
```

在清单 9 中，GreatestNumber 类的 gnObject1 对象必须调用成员函数 initialize() 来初始化数据成员 variable1 和 variable2。这种方法的唯一缺点是，如果用户忘记调用初始化函数，程序就会操作一个成员变量含有无意义值（垃圾字符）的对象。这是因为，在类中声明变量时，它内部只会存储一些垃圾字符（无意义的值）。

C++ 为这个问题提供了一种解决方案。在设计类时，可以在类中包含一个特殊成员函数，每当创建该类的对象时都会执行它。这类函数称为构造函数。构造函数是类的成员函数，当创建它们所属类的实例时会被调用。构造函数的显著特征是它们与类同名。

另一方面，析构函数在对象被销毁时取消初始化对象。当类的对象超出作用域时，析构函数会自动被调用。因此，程序员无需在每次对象超出作用域时清理数据成员占用的内存空间。

让我们解释如何在类中声明和使用构造函数。

### 声明和使用构造函数

构造函数是一种特殊成员函数，它分配内存并初始化其所属类的对象。构造函数不同于类的其他成员函数，因为它与类同名。它不包含返回类型（甚至不包括 void），这一点与函数不同。当类被实例化（创建对象）时，它会自动执行。清单 10 展示了类中构造函数的声明（你可以在随书光盘的 code\chapter6 文件夹中的 SimpleConstructor.cpp 文件里找到这个示例）：

**清单 10：在类中创建构造函数**

```cpp
#include<iostream.h>

class NumberInitialization
{
  int x,y;
  public:
  NumberInitialization()
  {
    cout<<"Constructor calling"<<endl;
    x=1;
    y=2;

    cout<<"x="<<x<<endl;
    cout<<"y="<<y<<endl;
    cout<<"Program Over\n";
  }
};

int main()
{
  NumberInitialization n1;
  //Constructor invoked
  return 0;
}
```

**输出：**

```text
Constructor calling
```

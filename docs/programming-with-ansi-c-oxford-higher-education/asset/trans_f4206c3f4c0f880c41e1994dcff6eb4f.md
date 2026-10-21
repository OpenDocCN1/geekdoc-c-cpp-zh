

这个例子也说明了如何让一个类成为另一个类的友元以及其有用性。另一种可能性是拥有一个友元类，该友元类提供有用的通用工具，例如使用消息框进行 GUI 输入/输出，如前所述。

## 4.12 const 和 volatile 函数

与 C 类似，const 和 volatile 变量在 C++ 中可用。然而，与 C 不同的是，C++ 中也可以拥有 const 和 volatile 函数。下面各节提供了简要介绍。

### 4.12.1 const 函数

常量对象已在第 3 章中讨论过，第 3.12 程序中也展示了 const 函数的定义。它们是通过将关键字 const 放在函数参数列表和函数体之间来定义的。

> 注意 const 函数可以操作常量或非常量对象；然而，它不能修改类对象。

```
<return type><function name>(argument1, argument2, ...) const
{
    <The body of the function>
}
```

第 3 章中的程序 3.12 包含以下函数：

```
void PrintDetails()const
/* This function is now constant; it cannot modify
an object of the class student */
{
    cout << "Roll number is " << RollNumber << "\n";
    cout << "Name is " << Name << "\n";
    cout << "Address is " << Address << "\n";
}
```

如果将此函数修改如下，编译程序时会出现错误。

```
void PrintDetails()const
{
    cout << "Roll number is" << RollNumber << " \n";
    cout << "Name is " << Name << "\n";
    cout << "Address is " << Address << "\n";
    RollNumber = 4;    // This is erroneous
}
```

> 注意 将成员函数定义为常量是一种良好的编程实践，当它们不应修改调用对象时。如此一来，如果函数后来被意外修改以更改数据成员的值，错误可以在编译期间被捕获。

### 4.12.2 可变数据成员

我们已经看到，普通数据成员不能被 const 函数修改。如果我们希望某个特殊数据成员能够被函数修改怎么办？如果我们不将
函数声明为 const，它就无法访问常量对象。声明特殊数据成员为 mutable 是解决此问题的方法。当数据成员被声明为 mutable 时，即使是 const 函数也可以修改它。

一个可变成员即使由 const 函数也可以被修改。

在给出的示例中，如果 RollNumber 定义被更改为

```
mutable int RollNumber;
```

在 student 类中，那么语句

```
void PrintDetails() const
{
    ...
    RollNumber = 4;
}
```

将不再导致错误。对于普通成员函数来说，可变数据成员与普通数据成员之间没有区别。

### 4.12.3 volatile 函数

如果成员函数由 volatile 对象调用，则该成员函数也可以声明为 volatile。volatile 对象的值可以由程序无法控制的外部参数更改。例如，从网络接口卡获取输入的对象并不从我们的程序获取输入。随着硬件中断的发生，与之相关的数值会在程序不知情的情况下发生变化。

以下代码中展示了 volatile 函数和 volatile 对象的示例定义：

静态函数仅处理静态变量。始终可以用普通函数替换静态函数；然而使用静态函数使程序更具可读性，并减少了意外更改的可能性。

```
class NICClass
{
public:
    void CheckValuesForNIC volatile
    // A volatile function definition
    {
        // Function body
    }
    ...
};
volatile NICClass NICObject;
// A volatile object definition
```

## 4.13 静态函数

某些工具对于一组对象是通用的。我们已经看到了处理对象集合的情况。工具或操作并不针对单个对象，而是作用于多个对象。有时，我们需要提供涉及所有对象的操作，例如找出当前创建了多少个对象。这种情况需要静态变量，在第 3 章中讨论过。我们可以看到，静态变量是表示当前存活对象数量的理想选择。程序 4.11 显示了如何使用静态函数代替成员或非成员函数。

> 注意 非成员函数类似于普通的 C 函数。如果我们将它们定义为 static，它们就成为定义它们的源文件本地的函数。换句话说，该函数的范围是定义该函数的文件体。

程序 4.11 是第 3 章中用于统计当前定义的学生数量的程序的修改版本。这里使用了一个静态函数来显示学生的总数。

### 程序 4.11 用于统计学生数量的静态函数

```
// StaticFunction.cpp
#include <iostream>
#include <string>
using namespace std;

class student
{
public:
    static int TotalStudents;
    static void DispTotal();
    // Declaration of a static member function

private:
    int RollNumber;
    string Name;
    string Address;

public:
    void SetDetails(int Roll, string StudentName, string StudentAddress)
    {
        RollNumber = Roll;
        Name = StudentName;
        Address = StudentAddress;
        TotalStudents++;
    }

    void PrintDetails()
    {
        cout << "Roll number is " << RollNumber << "\n";
        cout << "Name is " << Name << "\n";
        cout << "Address is " << Address << "\n";
    }
};

int student::TotalStudents;
void student::DispTotal()
/* See how the function name is preceded with the class name similar to a member function */
{
    cout << "Total students at the moment" << student::TotalStudents << "\n";
}

void main()
{
    student::DispTotal();
    student Robin;

    Robin.SetDetails(1, "Robin Singh", "New Delhi");
    Robin.PrintDetails();
    student::DispTotal();

student Sonia;
Sonia.SetDetails(2, "Mathur", "Mumbai");
Sonia.PrintDetails();
student::DispTotal();

if(true)
{
    student Anita;
    Anita.SetDetails(3, "Sharma", "Indore");
    Anita.PrintDetails();
    student::DispTotal();
}
cout << "Anita departs! \n";
/* The following will not work as expected. Total students are still three */
student::DispTotal();
}
```

### 程序的工作原理

DispTotal() 是一个新定义的静态函数。静态函数非常类似于非成员函数，唯一的区别是它现在仅绑定并已知于定义它的类。应记住，非成员函数对程序中的所有类都是已知的。静态函数类似于成员函数，只能由声明它们为静态的类的对象调用。它们可以通过其名称直接调用，并在其前面加上类名和作用域解析运算符。

> 注意 在 C 中，如果函数声明为 static，它将被视为定义它的文件本地。相同的概念适用于非成员的情况。静态非成员函数是文件本地的，不能在该物理文件之外访问。

静态函数如何定义和使用应予注意。像非成员函数一样，静态函数在类外定义。同时，它前面加上类名和作用域解析运算符，就像在类外定义的成员函数一样。

```
void student::DispTotal()
```

DispTotal() 是一个用于显示学生总数的静态函数，TotalStudents 也是一个静态变量。这并非偶然；静态函数只能作用于类的静态变量，不能访问类的其他数据成员。它也可以访问全局函数和数据。

静态函数最重要的优点是它们提高了程序的可读性。与调用 Shyam.DispTotal 不同，其中 Shyam 只是用于统计学生总数的虚拟对象，我们可以调用 student::DispTotal，即它前面应加上类名，可读性更强。

### 4.13.1 静态函数的限制

静态函数也有一些限制。其中一些重要限制如下：

- 1. 它们没有 this 指针，因为它们在真正意义上不是成员函数。这就是为什么它们无法访问成员变量。
- 2. 它们无法访问类的其他数据成员，因为这样做会隐式调用 this 指针。记住：RollNumber 等同于 this -> RollNumber。


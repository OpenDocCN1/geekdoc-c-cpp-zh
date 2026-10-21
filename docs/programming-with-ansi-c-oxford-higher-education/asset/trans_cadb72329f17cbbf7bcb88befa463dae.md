

C++ 对象模型更偏好以灵活性为代价的效率，因此有时即使程序本身没有变化，只要它使用的库发生了变化，就需要重新编译程序。

假设一个类库要在链接时（编译后、执行前）被包含到程序中。假设一个应用程序是使用这些类开发的，并且类成员是通过指向成员运算符来访问的。后来，如果库有一个新版本，其中只有一种类的格式不同，理想情况下它应该只进行链接而不重新编译。这是因为应用程序本身没有改变，只是它使用的库发生了改变。然而，在我们的情况下，应用程序需要重新编译，因为如果类格式发生变化，则偏移值也会相应改变。应用程序在任何指向成员表达式的地方都使用这些偏移量。

尽管这似乎是一个很大的缺点，但 C++ 设计者选择这种方案用于 C++ 对象模型的原因很简单。如果我们有一个真正的指针，每次通过它访问成员时都需要检查并遍历它。如果只有一个类，这不会太困难。然而，当存在一条很长的继承链时，一个类继承自另一个类，又一个继承自它，等等，实际的链接可能非常深。遍历这样一条很长的链是一个非常缓慢的过程。在这种情况下，C++ 对象模型更偏好效率而非灵活性。

VC++ 和 CORBA 的动态链接库（DLLs）模型与这里讨论的 C++ 对象模型不同。两者都更灵活，显然效率更低。VC++ 扩展了原始对象模型以适应 DLLs。在这里，DLLs 是在运行时添加到应用程序中并从中移除的对象集合。CORBA 是一种从应用程序访问对象的机制，而无需真正知道对象在哪里（它可以是远程机器的一部分）以及它是用什么语言实现的。CORBA 对象模型在功能性方面更先进，并提供更强的灵活性。然而，它是以效率为代价的。

## 3.12 嵌套类

可以在另一个类内部定义一个类，如以下示例所示。

```
//NestedClasses.cpp
#include <iostream>
using namespace std;
class Outside
{
private:
    /* The nested class (Inside) is private, hence only the nesting class (Outside) can access it, others cannot. */
    class Inside
    {
        int InsideInt;
    public:
        void SetInsideInt(int TempInside)
        {
            InsideInt = TempInside;
        }
    }; // End of inner class definition
public:
}
}; // End of outer class definition
int main()
{
    Outside OuterClass;
    OuterClass.OutsideInt = 5;
    OuterClass.UseInside();
    Outside::Inside InnerPublicClass;
    InnerPublicClass.SetInsideInt(5);
}
```

如果我们在嵌套类的公共部分定义一个嵌套类，它对所有有权访问嵌套类的人都是可用的。在这种情况下，最好将其作为单独的类在嵌套类之外定义，而不是作为嵌套类。

也可以在嵌套（外）类之外定义嵌套（内）类。以下是一个相同的例子，其中嵌套（内）类再次被定义为私有。

```
//DefineOutsideNC.cpp
#include <iostream>
using namespace std;
class Outside
{
private:
    class Inside;
public:
    int OutsideInt;
    void UseInside();
}; // End of outer class definition
class Outside::Inside
{
    int InsideInt;
public:
    void SetInsideInt(int TempInside)
    {
        InsideInt = TempInside;
    }
}; // Inner class is defined outside the class
/* The following function uses the Inside class and so the compiler must allocate appropriate size for the Inside class for the statement Inside InsideObject; This is why this function is also defined outside the class after the definition of Inside class */
void Outside::UseInside()
{
    Inside InsideObject;
    InsideObject.SetInsideInt(OutsideInt);
    cout << OutsideInt;
}
int main()
{
    Outside OuterClass;
    OuterClass.OutsideInt=5;
    OuterClass.UseInside();
}
```

需要注意的是，当嵌套类在外部定义时，定义不能在嵌套（外）类的作用域内。它不能在外类的主体中定义，而必须在其外部。此外，还可以观察到，外类在其主体中只有该类的原型。

## 嵌套类的需求

在外部定义内部类并将其设为私有有一些优点。大项目首先需要组件的开发。然后，这些组件被其他程序员在开发应用程序时使用。开发这些关键组件的团队通常由经验丰富且才华横溢的程序员组成。内部或嵌套类是一个由该团队中的某人开发并可能维护的组件，其定义在库中可用。

在项目中工作的其他团队“更接近”项目，对应用程序开发有更深入的了解。这些开发人员可以访问这些组件，并通过在外类或嵌套类的主体内部定义该类的原型来使用它们。这也确保了开发人员可以访问组件（内部类或嵌套类），但最终用户无法看到该类。

如果组件用于执行某些非常复杂的操作，则确保即使开发人员也无法访问代码。这是因为这些组件已编译并以对象代码的形式从库提供给开发人员。这类似于拥有字符串类对象并在程序中使用它们，其中我们无法访问定义字符串类的代码。

## 3.13 局部类

为了完整性，C++ 允许在函数内部定义类。这些类称为局部类。

以下示例可用于理解局部类。再次考虑 student 类。它现在在函数内部定义。TestStudent() 是定义该类并在自身内部使用它的函数。类在函数内部定义的一个后果是相当合乎逻辑的；该类在函数外部不可见。换句话说，类的作用域局限于函数的主体。

另一个需要注意的点是，定义类的函数不是该类的成员函数。它无法访问类的私有变量。

> 局部类是指在函数内部定义的类。

> 注意 访问类的私有变量的一种方法是成为它的友元。友元函数将在第 4 章中讨论。

```
//LocalClasses.cpp
#include <iostream>
#include <string>
using namespace std;
void main()
{
    int RollNo = 3;
    void TestStudent(int);
    /* Prototype of TestStudent function; class student is not known here */
    TestStudent(RollNo);
}
void TestStudent(int Roll)
{
    int TestValue = 100;
    static int StaticTestValue = 200;
    /* This is a local class and is available only inside the TestStudent() function */
    class student
    {
    public:
        int RollNumber;
        string Name;
        string Address;
        void PrintDetails()
        // This function cannot be defined outside the class
        {
            // The following line does not work
            // cout << TestValue;
            /* This class cannot use TestValue because it is a private variable of the class, so it is to be commented. */
            // The following works
            cout << ::StaticTestValue;
            cout << "Roll number is " << RollNumber << "\n";
            cout << "Name is " << Name << "\n";
            cout << "Address is " << Address << "\n";
        }
    };
    student Student1;
    Student1.RollNumber = Roll;
    Student1.Name = "Robin Singh";
    Student1.Address = "New Delhi";
    Student1.PrintDetails();
}
```

### 局部类的限制

以下是使用局部类的一些限制：
- 1. 它们不能使用容器函数的 auto 局部变量（例如，TestValue）。
- 2. 它们可以访问容器函数的静态局部变量或外部变量（全局定义）（例如，StaticTestValue）。
- 3. 它们本身不能包含静态成员。
- 4. 它们不能在其类边界之外定义其函数。这里，PrintDetails() 函数必须在类内部定义。
- 5. 除非声明为友元，否则它们的私有变量对容器函数不可用。



设置函数有时也称为修改器（因为它们会修改或更改值），而 *获取* 函数也称为访问器（因为它们访问值）。

回顾一下，使用访问说明符 private 声明数据成员可强制实现数据隐藏。提供公有的 *设置* 和 *获取* 函数允许类的客户访问隐藏数据，但只能间接访问。客户知道它正试图修改或获取对象的数据，但客户不知道对象如何执行这些操作。在某些情况下，类可能在内部以某种方式表示一项数据，但以另一种方式向客户公开该数据。例如，假设一个 Clock 类将一天中的时间表示为私有 int 数据成员 time，该成员存储自午夜以来的秒数。然而，当客户调用 Clock 对象的 *getTime* 成员函数时，该对象可以以 "HH:MM:SS" 格式的字符串返回时、分、秒形式的时间。类似地，假设 Clock 类提供一个名为 *setTime* 的 *设置* 函数，该函数接受 "HH:MM:SS" 格式的字符串参数。利用第 18 章介绍的 string 功能，*setTime* 函数可以将此字符串转换为秒数，并将该秒数存储在其私有数据成员中。*设置* 函数还可以检查它接收的值是否表示有效时间（例如，"12:30:45" 有效，但 "42:85:70" 无效）。*设置* 和 *获取* 函数允许客户与对象交互，但对象的私有数据仍安全地封装（即隐藏）在对象自身中。

类的 *设置* 和 *获取* 函数也应由类内的其他成员函数用来操作类的私有数据，尽管这些成员函数可以直接访问私有数据。在图 3.5 中，成员函数 *setCourseName* 和 *getCourseName* 是公有成员函数，因此类的客户以及类本身都可以访问它们。成员函数 *displayMessage* 调用成员函数 *getCourseName* 来获取数据成员 *courseName* 的值以进行显示，尽管 *displayMessage* 可以直接访问 *courseName*——通过其 *获取* 函数访问数据成员可创建更好、更健壮的类（即更易于维护且更不易发生故障的类）。如果我们决定以某种方式更改数据成员 *courseName*，则 *displayMessage* 的定义不需要修改——只需要更改直接操作该数据成员的 *获取* 和 *设置* 函数的函数体。例如，假设我们希望将课程名称表示为两个单独的数据成员——*courseNumber*（例如 "CS101"）和 *courseTitle*（例如 "Introduction to C++ Programming"）。成员函数 *displayMessage* 仍可以只调用一次成员函数 *getCourseName*，以将完整课程名称作为欢迎消息的一部分显示。在这种情况下，*getCourseName* 需要构造并返回一个包含 *courseNumber* 后跟 *courseTitle* 的字符串。成员函数 *displayMessage* 可以继续显示完整课程标题（“CS101 Introduction to C++ Programming”）。从同一个类的另一个成员函数调用 *设置* 函数的好处，将在第 3.8 节讨论验证时变得清楚。

![](img/bfd978e7e9b192bab46ec2a89e481263_109_0.png)

> **良好的编程实践 3.1**
>
> *始终尽量通过获取和设置函数访问和操作数据成员，从而将类数据成员更改的影响局部化。*

![](img/bfd978e7e9b192bab46ec2a89e481263_109_1.png)

> **软件工程观察 3.2**
>
> *编写清晰且易于维护的程序。变化是常态而非例外。你应该预料到自己的代码会被修改。*

## 带数据成员及设置和获取函数的 GradeBook UML 类图

图 3.6 包含图 3.5 中类 GradeBook 版本的更新 UML 类图。该图将 GradeBook 的数据成员 courseName 建模为中间隔间中的一个属性。UML 通过列出属性名，后跟冒号和属性类型，将数据成员表示为属性。属性 courseName 的 UML 类型为 String，对应于 C++ 中的 string。数据成员 courseName 在 C++ 中是私有的，因此类图在相应属性名前列出减号（−）。UML 中的减号等价于 C++ 中的 private 访问说明符。类 GradeBook 包含三个公有成员函数，因此类图在第三个隔间中列出三个操作。操作 setCourseName 有一个名为 name 的 String 参数。UML 通过在操作名后的圆括号之后放置冒号和返回类型来表示操作的返回类型。类 GradeBook 的成员函数 getCourseName 在 C++ 中具有 string 返回类型，因此类图在 UML 中显示 String 返回类型。操作 setCourseName 和 displayMessage 不返回值（即它们在 C++ 中返回 void），因此 UML 类图在这些操作的圆括号之后不指定返回类型。

![](img/bfd978e7e9b192bab46ec2a89e481263_110_0.png)

**图 3.6** | 类 *GradeBook* 的 UML 类图，包含私有 *courseName* 属性和公有操作 *setCourseName*、*getCourseName* 以及 *displayMessage*。

## 3.5 用构造函数初始化对象

如第 3.4 节所述，当创建类 GradeBook（图 3.5）的对象时，其数据成员 courseName 默认初始化为空字符串。如果希望在创建 GradeBook 对象时提供课程名称，该怎么办？你声明的每个类都可以提供一个构造函数，用于在创建对象时初始化该类的对象。构造函数是一种特殊的成员函数，必须与类同名定义，以便编译器能将其与类的其他成员函数区分开。构造函数与其他函数的一个重要区别是构造函数不能返回值，因此不能指定返回类型（甚至不能指定 void）。通常，构造函数声明为公有。

C++ 要求为每个创建的对象调用构造函数，这有助于确保每个对象在程序中使用之前被正确初始化。构造函数调用在创建对象时隐式发生。如果类没有显式包含构造函数，编译器会提供一个默认构造函数——即没有参数的构造函数。例如，当图 3.5 的第 41 行创建一个 GradeBook 对象时，会调用默认构造函数。编译器提供的默认构造函数在创建 GradeBook 对象时不会为该对象的基本类型数据成员提供任何初始值。[注意：对于作为其他类对象的数据成员，默认构造函数会隐式调用每个数据成员的默认构造函数，以确保该数据成员被正确初始化。这就是为什么 `string` 数据成员 `courseName`（在图 3.5 中）被初始化为空字符串——类 `string` 的默认构造函数将字符串的值设置为空字符串。你将在第 10.3 节中了解更多关于初始化作为其他类对象的数据成员的内容。]

在图 3.7 的示例中，我们在创建 GradeBook 对象时为该对象指定课程名称（例如第 46 行）。在这种情况下，实参 "CS101 Introduction to C++ Programming" 被传递给 GradeBook 对象的构造函数（第 14–17 行），并用于初始化 courseName。图 3.7 定义了一个修改后的 GradeBook 类，其中包含一个带 string 参数的构造函数，该参数接收初始课程名称。

```cpp
// Fig. 3.7: fig03_07.cpp
// Instantiating multiple objects of the GradeBook class and using
// the GradeBook constructor to specify the course name
// when each GradeBook object is created.
#include <iostream>
#include <string> // program uses C++ standard string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
   // constructor initializes courseName with string supplied as argument
   GradeBook( string name )
   {
      setCourseName( name ); // call set function to initialize courseName
   } // end GradeBook constructor

   // function to set the course name
   void setCourseName( string name )
   {
      courseName = name; // store the course name in the object
   } // end function setCourseName

   // function to get the course name
   string getCourseName()
   {
      return courseName; // return object's courseName
   } // end function getCourseName

   // display a welcome message to the GradeBook user
   void displayMessage()
   {
      // call getCourseName to get the courseName
      cout << "\nWelcome to the grade book for\n" << getCourseName()
           << "!" << endl;
   } // end function displayMessage
private:
   string courseName; // course name for this GradeBook
}; // end class GradeBook
```

**图 3.7** 实例化 GradeBook 类的多个对象，并在创建每个 GradeBook 对象时使用 GradeBook 构造函数指定课程名称。（第 1 部分，共 2 部分。）

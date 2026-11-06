

```cpp
// Fig. 10.12: Employee.h
// Employee class definition showing composition.
// Member functions defined in Employee.cpp.
#ifndef EMPLOYEE_H
#define EMPLOYEE_H

#include <string>
#include "Date.h" // include Date class definition
using namespace std;

class Employee
{
public:
   Employee( const string &, const string &,
      const Date &, const Date & );
   void print() const;
   ~Employee(); // provided to confirm destruction order
private:
   string firstName; // composition: member object
   string lastName; // composition: member object
   const Date birthDate; // composition: member object
   const Date hireDate; // composition: member object
}; // end class Employee

#endif
```

图 10.12 | 展示组合关系的 Employee 类定义。

```cpp
// Fig. 10.13: Employee.cpp
// Employee class member-function definitions.
#include <iostream>
#include "Employee.h" // Employee class definition
#include "Date.h" // Date class definition
using namespace std;

// constructor uses member initializer list to pass initializer
// values to constructors of member objects
Employee::Employee( const string &first, const string &last,
   const Date &dateOfBirth, const Date &dateOfHire )
   : firstName( first ), // initialize firstName
     lastName( last ), // initialize lastName
     birthDate( dateOfBirth ), // initialize birthDate
     hireDate( dateOfHire ) // initialize hireDate
{
   // output Employee object to show when constructor is called
   cout << "Employee object constructor: "
      << firstName << ' ' << lastName << endl;
} // end Employee constructor
```

图 10.13 | Employee 类成员函数定义，包括带有成员初始化列表的构造函数。（第 1 部分，共 2 部分。）

```cpp
1  // Fig. 10.14: fig10_14.cpp
2  // Demonstrating composition--an object with member objects.
3  #include <iostream>
4  #include "Employee.h" // Employee class definition
5  using namespace std;
6
7  int main()
8  {
9     Date birth( 7, 24, 1949 );
10    Date hire( 3, 12, 1988 );
11    Employee manager( "Bob", "Blue", birth, hire );
12
13    cout << endl;
14    manager.print();
15
16    cout << "\nTest Date constructor with invalid values:\n";
17    Date lastDayOff( 14, 35, 1994 ); // invalid month and day
18    cout << endl;
19 } // end main
```

```text
Date object constructor for date 7/24/1949
Date object constructor for date 3/12/1988
Employee object constructor: Bob Blue
Blue, Bob  Hired: 3/12/1988  Birthday: 7/24/1949

Test Date constructor with invalid values:
Invalid month (14) set to 1.
Invalid day (35) set to 1.
Date object constructor for date 1/1/1994

Date object destructor for date 1/1/1994
Employee object destructor: Blue, Bob
Date object destructor for date 3/12/1988
Date object destructor for date 7/24/1949
Date object destructor for date 3/12/1988
Date object destructor for date 7/24/1949
```

实际上，构造一个 Employee 对象时会有五次构造函数调用——两次调用 string 类的构造函数（图 10.13 的第 12–13 行）、两次调用 Date 类的默认复制构造函数（图 10.13 的第 14–15 行），以及一次调用 Employee 类的构造函数。

图 10.14 | 演示组合——一个带有成员对象的对象。

Date 类和 Employee 类各自包含一个析构函数（分别是图 10.11 的第 35–40 行和图 10.13 的第 33–37 行），当类的对象被析构时会打印一条消息。这使我们能够在程序输出中确认对象是**从内向外**构造的，并以相反的顺序、**从外向内**销毁的（也就是说，Date 成员对象在包含它们的 Employee 对象之后被销毁）。请注意图 10.14 输出中的最后四行。最后两行分别是 Date 析构函数对对象 hire（第 10 行）和 birth（第 9 行）运行时的输出。这些输出确认了在 main 中创建的三个对象是按照构造顺序的相反顺序被销毁的。Employee 析构函数的输出位于倒数第五行。输出窗口的倒数第四行和第三行显示了 Employee 的成员对象 hireDate（图 10.12，第 22 行）和 birthDate（图 10.12，第 21 行）的析构函数运行。这些输出确认了 Employee 对象是**从外向内**被销毁的——即 Employee 析构函数首先运行（输出显示在输出窗口的倒数第五行），然后成员对象按照构造顺序的*逆序*被销毁。string 类的析构函数没有输出语句，因此我们看不到 *firstName* 和 *lastName* 对象被销毁的过程。同样，图 10.14 的输出没有显示成员对象 *birthDate* 和 *hireDate* 的构造函数运行，因为这些对象是用编译器提供的默认 *Date* 类复制构造函数初始化的。

### 如果不使用成员初始化列表会发生什么？

如果成员对象没有通过成员初始化器进行初始化，则会隐式调用该成员对象的默认构造函数。默认构造函数设置的任何值（如果有）都可以通过 *set* 函数覆盖。然而，对于复杂的初始化，这种方法可能需要大量的额外工作和时间。

**常见编程错误 10.6**

*如果成员对象未使用成员初始化器进行初始化，并且该成员对象的类没有提供默认构造函数（即该成员对象的类定义了一个或多个构造函数，但其中没有一个是默认构造函数），则会发生编译错误。*

**性能提示 10.2**

*通过成员初始化器显式初始化成员对象。这消除了“双重初始化”成员对象的开销——一次是在成员对象的默认构造函数被调用时，另一次是在构造函数体内（或之后）调用 set 函数来初始化成员对象时。*

**软件工程观察 10.7**

*如果类的成员是另一个类的对象，将该成员对象设为 public 并不会违反该成员对象私有成员的封装和隐藏。但是，它确实违反了包含该成员对象的类的实现的封装和隐藏，因此类类型的成员对象仍应像所有其他数据成员一样是 private 的。*

## 10.4 friend 函数和 friend 类

类的 *friend* 函数定义在该类的作用域之外，但有权访问该类的非公有（和公有）成员。独立函数、整个类或其他类的成员函数都可以声明为另一个类的友元。

使用 friend 函数可以提高性能。本节通过一个机械示例演示 friend 函数的工作原理。在本书后面，friend 函数被用于重载操作符以用于类对象（第 11 章），以及创建迭代器类（第 20 章，数据结构）。迭代器类的对象可以依次选择容器类对象中的项目，或对项目执行操作。容器类的对象可以存储项目。当成员函数无法用于某些操作时，使用友元通常是合适的，我们将在第 11 章中看到这一点。

要将一个函数声明为类的友元，请在类定义中的函数原型前加上关键字 *friend*。要将类 *ClassTwo* 的所有成员函数声明为类 *ClassOne* 的友元，请在类 *ClassOne* 的定义中放置如下形式的声明：

```cpp
friend class ClassTwo;
```

**软件工程观察 10.8**

尽管 friend 函数的原型出现在类定义中，但友元不是成员函数。

**软件工程观察 10.9**

private、protected 和 public 的成员访问概念与友元声明无关，因此友元声明可以放置在类定义中的任何位置。

**良好编程实践 10.1**

将所有友元声明放在类定义体的最前面，并且不要在其前面添加任何访问说明符。

友元关系是被授予的，而不是被索取的——也就是说，要使类 B 成为类 A 的友元，类 A 必须显式声明类 B 是其友元。此外，友元关系既不对称也不传递；也就是说，如果类 A 是类 B 的友元，且类 B 是类 C 的友元，你不能推断出类 B 是类 A 的友元（同样，友元关系不是对称的），也不能推断出类 C 是类 B 的友元（也因为友元关系不是对称的），更不能推断出类 A 是类 C 的友元（友元关系不是传递的）。

**软件工程观察 10.10**

面向对象编程社区中的一些人认为“友元”破坏了信息隐藏，并削弱了面向对象设计方法的价值。在本书中，我们指出了几个负责任地使用友元的示例。

### 使用 friend 函数修改类的 private 数据

图 10.15 是一个机械示例，其中我们定义了 friend 函数 setX 来设置类 Count 的私有数据成员 x。友元声明（第 9 行）按照惯例出现在类定义的最前面，甚至在公有成员函数声明之前。同样，该友元声明可以出现在类的任何位置。

```cpp
// Fig. 10.15: fig10_15.cpp
// Friends can access private members of a class.
#include <iostream>
using namespace std;

// Count class definition
class Count
{
    friend void setX( Count &, int ); // friend declaration
public:
    // constructor
    Count()
        : x( 0 ) // initialize x to 0
    {
        // empty body
    } // end constructor Count
```

**图 10.15**  |  友元可以访问类的私有成员。（第 1 部分，共 2 部分。）


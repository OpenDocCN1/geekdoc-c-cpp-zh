

## 程序 12.34 文件 `student.h`（续）

```cpp
#include "stdtype.h"

class Student: public Person, public StdType
{
public:
    Student (string name, double gpa);
    void printGPA();
    void print();
};
#endif
```

程序 12.35 展示了*Professor*类的接口文件。请注意，该类没有自己的数据成员；它只继承了*Person*类和*PrfType*类的数据成员。

## 程序 12.35 文件 `professor.h`

```cpp
/***************************************************************
 * The interface file for Professor concrete class. This class   *
 * inherits from two classes: Person and PrfType.               *
 ***************************************************************/
#ifndef PROFESSOR_H
#define PROFESSOR_H
#include "person.h"
#include "prftype.h"

class Professor : public Person, public PrfType
{
public:
    Professor (string name, double salary);
    void printSalary();
    void print ();
};
#endif
```

程序 12.36 展示了TA类的接口文件。请注意，该类没有自己的数据成员；它只继承了*Person*类、*StdType*类和*PrfType*类的数据成员。

## 程序 12.36 文件 `ta.h`

```cpp
/***************************************************************
 * The interface file for TA concrete class. This class          *
 * inherits from three classes: Person and StdType and PrfType.  *
 ***************************************************************/
#ifndef TA_H
#define TA_H
#include "person.h"
#include "stdtype.h"
#include "prftype.h"

class TA: public Person, public StdType, public PrfType
{
public:
    TA (string name, double gpa, double salary);
    void printGPA ();
    void printSalary();
    void print ();
};
#endif
```

程序 12.37 展示了Person类的实现文件。程序 12.38 展示了Student类的实现文件。请注意，它从*StdType*类继承了作为受保护数据成员的*gpa*数据成员。该数据成员可以在*Student*类中访问，但无法在此类中初始化。我们必须在构造函数中为它赋值。

## 程序 12.37 文件 `person.cpp`

```cpp
/***************************************************************
 * The implementation file for Person concrete class            *
 ***************************************************************/
#include "person.h"

// Constructor
Person :: Person (string nm)
: name(nm)
{
}
// Print member function
void Person :: print ( )
{
    cout << "Name: " << name << endl;
}
```

## 程序 12.38 文件 `student.cpp`

```cpp
/***************************************************************
 * The implementation file for Student concrete class           *
 ***************************************************************/
#include "student.h"

// Constructor
Student :: Student (string na, double gp)
: Person (na)
{
    gpa = gp;                 // Assignment, not initialization
}
// PrintGPA member function
void Student :: printGPA()
{
    cout << "GPA: " << fixed << setprecision (2) << gpa << endl;
}
// Print member function
void Student :: print()
{
    Person :: print();
    printGPA();
}
```

程序 12.39 展示了*Professor*类的实现文件。请注意，它从*PrfType*类继承了作为受保护数据成员的*salary*数据成员。该数据成员可以在*Professor*类中访问，但无法在此类中初始化；我们必须在构造函数中为它赋值。

## 程序 12.39 文件 `professor.cpp`

```cpp
/********************************************************
 * The implementation file for Professor concrete class *
 ********************************************************/
#include "professor.h"

// Constructor
Professor :: Professor (string nm, double sal)
: Person (nm)
{
    salary = sal;             // Assignment, not initialization
}
// PrintSalary member function
void Professor :: printSalary()
{
    cout << "Salary: ";
    cout << fixed << setprecision (2) << salary << endl;
}
// General print function
void Professor :: print()
{
    Person::print();
    printSalary();
}
```

程序 12.40 展示了TA类的实现文件。请注意，它从*PrfType*类继承了作为受保护数据成员的*salary*数据成员，并从*StdType*类继承了作为受保护数据成员的*gpa*数据成员。这些数据成员可以在TA类中访问，但无法在此类中初始化。我们必须在构造函数中为它们赋值。

## 程序 12.40 文件 `ta.cpp`

```cpp
/****************************************************
 * The implementation file for TA concrete class    *
 ****************************************************/
#include "ta.h"

// Constructor
TA :: TA (string nm, double gp, double sal)
: Person (nm)
{
    gpa = gp;                 // Assignment, not initialization
    salary = sal;             // Assignment, not initialization
}
// member function to print GPA
void TA :: printGPA ()
{
    cout << "GPA: " << gpa << endl;
}
// member function to print salary
void TA :: printSalary ()
{
    cout << "Salary: ";
    cout << fixed << setprecision (2) << salary << endl;
}
// General print function
void TA :: print ()
{
    Person :: print();
    printGPA ();
    printSalary();
}
```

程序 12.41 展示了一个用于测试混合类思想的非常简单的应用程序文件。应用程序由用户定义。

## 程序 12.41 文件 `application.cpp`

```cpp
/******************************************************************
 * The application file to test the three classes                 *
 ******************************************************************/
#include "student.h"
#include "professor.h"
#include "ta.h"

int main( )
{
    // Instantiation of our objects
    Person per ("John");
    Student std ("Linda", 3.9);
    Professor prof("George", 89000);
    TA ta ("Lucien", 3.8, 23000);
    // Printing information about a person
    cout << "Information about person" << endl;
    per.print();
    cout << endl << endl;
    // Printing information about a student
    cout << "Information about student" << endl;
    std.print();
    cout << endl << endl;
    // Printing information about a professor
    cout << "Information about professor" << endl;
    prof.print();
    cout << endl << endl;
    // Printing information about a teaching assistant
    cout << "Information about teaching assistant" << endl;
    ta.print();
    cout << endl << endl;
    return 0;
}
```

```text
运行：
关于人员的信息
姓名：John

关于学生的信息
姓名：Linda
GPA：3.90
```

![](img/d68f6199646ca63591a6d8419e0ed4ba_612_0.png)

## 关键术语

- 抽象类
- 具体类
- 动态绑定
- 混合类
- 多重继承
- 多态
- 纯虚函数
- 静态绑定
- 虚基类继承

## 总结

多态使我们能够编写同一个函数的多个版本，每个版本位于不同的类中。然后，当我们调用该函数时，会执行与被引用对象相适应的版本。多态需要满足三个条件：指针或引用、继承层次结构以及虚函数。与多态相关的一个问题是*绑定*。我们可以使用*静态绑定*和*动态绑定*。

在C++中，我们可以使用*具体*类和*抽象*类。具体类可以被实例化，并且能够创建其类型的对象。

抽象类可以作为具体类遵循的通用基类。抽象类必须至少包含一个纯虚函数，其声明被设置为0，并且没有函数定义。我们不能从抽象类实例化对象，但可以继承抽象类。接口是抽象类的一种特殊情况，其中所有成员函数都是纯虚函数。

## 习题

- PR-1. 假设我们有一个名为*Base*的类，以及两个从*Base*类继承而来的名为*Derived1*和*Derived2*的类。我们希望在多态关系中使用这些类。如果每个类都有一个虚拟的*print*函数和一个虚析构函数，请展示这些类的虚函数表条目。
- PR-2. 假设我们有以下两个类。展示如何使用栈内存以多态方式实例化这两个类的对象。


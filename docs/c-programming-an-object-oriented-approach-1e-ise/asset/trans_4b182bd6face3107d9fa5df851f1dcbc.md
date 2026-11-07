
类的成员。当我们使用私有数据成员时，数据对类外部的实体以及派生类都是隐藏的。另一方面，使用私有数据成员意味着在派生类中创建更多代码。因此，私有数据成员的优点是封装性更强；其缺点是在派生类中创建更多代码。如果我们是基类的设计者，并且希望保护我们的数据成员不被直接访问，就应该使用私有数据成员。

## 使用受保护的数据成员

使用受保护的数据成员会使派生类的编码更简单。然而，它破坏了封装的思想。我们将会看到，有时我们必须使用受保护的数据成员，因为如果使用私有数据成员，编码会变得非常复杂。

## 阻止继承

有时我们可能想要阻止继承——例如，当我们（作为设计者）定义了一个类，并且不希望用户从这个类继承并创建派生类时。C++ 标准允许我们使用 `final` 修饰符来做到这一点，如下所示。

```cpp
class First final
{
    ...
};
```

我们也可以使用 final 修饰符来阻止继承层次结构中任何位置的继承。例如，我们可能有一个从基类派生的派生类，但不希望该层次结构继续下去，如下所示。

```cpp
class First
{
    ...
};
class Second final : public First
{
    ...
};
```

*Second* 类继承自 *First* 类，但继承在这里被阻止了。我们不希望有人尝试从 *Second* 类创建另一个子类。final 修饰符会阻止进一步继承。

## 里氏替换原则（LSP）

一个有时被忽视的设计原则是由 Barbara Liskov 提出的**里氏替换原则**（LSP）。该原则指出，超类的对象必须始终能够被子类的对象替换，而不改变超类的任何属性。在现实生活中，我们可能认为一个对象是另一种对象的特殊类型，但在面向对象编程中，我们必须在编写代码之前检查 LSP。

![](img/d68f6199646ca63591a6d8419e0ed4ba_531_0.png)

图 11.14 里氏替换原则

### 示例 11.5

为了更好地理解里氏替换原则，我们考虑两个对象：*正方形* 和 *长方形*。在现实生活中，我们可能会说正方形是一种特殊的长方形，其长度和宽度相同。我们也可能会说长方形是一种正方形，其中长度和边长不相同。这两种定义都不符合面向对象编程中的 *is-a* 关系。为了理解原因，我们研究图 11.14 所示的两种方法。

在图 11.14 中，左侧的情况里，我们可能认为 *Square* 类可以派生自 *Rectangle* 类，因为正方形是一种特殊的长方形。然而，我们看到 *Square* 类型的对象只有一个数据成员，而不是两个。*Square* 类型的对象无法封装 *Rectangle* 类型的对象，因此它不可替换。

同样在图 11.14 中，右侧的情况里，*Rectangle* 类的对象比 *Square* 类的对象拥有更多数据成员，但它们都不能从 *Square* 类复制。换句话说，*Rectangle* 类的对象与 *Square* 类的对象没有关系，也不能替代它。

这并不意味着我们不能在继承层次结构中拥有 *Square* 类和 *Rectangle* 类。这意味着它们不能相互继承；它们可以处于同一层级，并继承自一个共同的基类。

## 继承树

在 C++ 中，我们可以拥有继承树。例如，我们可以有两个继承自 *Person* 类的类：*Student* 和 *Employee*。显然，学生是一个人，雇员也是一个人。图 11.15 展示了这棵继承树。在本章后面，我们还会定义其他类，例如继承自 *Student* 类的 *Undergraduate* 类和 *Graduate students* 类。我们还会定义继承自 *Employee* 类的 *Staff* 类和 *Professor* 类。

### 示例 11.6

在本例中，我们为图 11.15 所示的类创建接口文件、实现文件和应用文件。参见程序 11.7 至 11.13。

![](img/d68f6199646ca63591a6d8419e0ed4ba_531_1.png)

图 11.15 继承树

### 程序 11.7 文件 person.h

```cpp
/**********************************************************
 * The interface file to define the Person class
 **********************************************************/

#ifndef PERSON_H
#define PERSON_H
#include <iostream>
#include <string>
using namespace std;

// Definition of Person class
class Person
{
    private:
        string name;
    public:
        Person (string nm);
        ~Person();
        void print () const;
};
#endif
```

### 程序 11.8 文件 person.cpp

```cpp
/**********************************************************
 * The implementation file for the Person class
 **********************************************************/

#include "person.h"

// Constructor for Person class
Person :: Person (string nm)
:name (nm)
{
}
// Destructor for Person class
Person :: ~Person()
{
}
// Definition of print member function
void Person :: print () const
{
    cout << "Name: " << name << endl;
}
```

### 程序 11.9 文件 `student.h`

```cpp
/*************************************************************
 * The interface file to define the Student class             *
 *************************************************************/
#ifndef STUDENT_H
#define STUDENT_H
#include "person.h"

// Definition of the Student class
class Student : public Person
{
private:
    string name;
    double gpa;
public:
    Student (string name, double gpa);
    ~Student ();
    void print () const;
};
#endif
```

### 程序 11.10 文件 `student.cpp`

```cpp
/*************************************************************
 * The implementation file for the Student class             *
 *************************************************************/
#include "student.h"

// Constructor for Student class
Student :: Student (string nm, double gp)
:Person (nm), gpa (gp)
{
}
// Destructor for Student class
Student :: ~Student ()
{
}
// Definition of the print member function
void Student :: print () const
{
    Person :: print();
    cout << "GPA: " << gpa << endl;
}
```

### 程序 11.11 文件 employee.h

```cpp
/************************************************************
 * The interface file to define the Employee class           *
 ************************************************************/
#ifndef EMPLOYEE_H
#define EMPLOYEE_H
#include "person.h"

// Definition of the Employee class
class Employee : public Person
{
private:
    string name;
    double salary;
public:
    Employee (string name, double salary);
    ~Employee ();
    void print () const;
};
#endif
```

### 程序 11.12 文件 employee.cpp

```cpp
/************************************************************
 * The implementation file for the Employee class           *
 ************************************************************/
#include "employee.h"

// Constructor for Employee class
Employee::Employee (string nm, double sa)
:Person (nm), salary (sa)
{
}
// Destructor for Employee class
Employee::~Employee()
{
}
// Definition of print member function
void Employee::print () const
{
    Person::print();
    cout << "Salary: " << salary << endl;
}
```

### 程序 11.13 文件 application.cpp

```cpp
/***************************************************************
 * The application file to use classes                            *
 ***************************************************************/
#include "student.h"
#include "employee.h"

int main ()
{
    // Instantiation and using an object of the Person class
    cout << "Person: " << endl;
    Person person ("John");
    person.print ();
    cout << endl << endl;
    // Instantiation and using an object of the Student class
    cout << "Student: " << endl;
    Student student ("Mary", 3.9);
    student.print ();
    cout << endl << endl;
    // Instantiation and using an object of the Employee class
    cout << "Employee: " << endl;
    Employee employee ("Juan", 78000.00);
    employee.print ();
    cout << endl << endl;
    return 0;
}
```

```text
Run:
Person:
Name: John

Student:
Name: Mary
GPA: 3.9

Employee:
Name: Juan
Salary: 78000
```

## 11.1.4 三种继承类型

尽管 *public* 继承是迄今为止最常见的派生类型，但 C++ 允许我们使用另外两种派生类型：*private* 和 *protected*。在讨论这两种派生的应用之前，我们使用图 11.16 展示每种派生中元素的状态。表中的术语 *hidden* 意味着该成员不能由派生类的公有成员函数访问。它必须通过基类的公有成员函数访问。

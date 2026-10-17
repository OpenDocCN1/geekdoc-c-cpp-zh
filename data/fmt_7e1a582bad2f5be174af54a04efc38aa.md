
程序 12.4 显示了 `Person` 类的实现文件。

`Student` 类程序 12.5 显示了 `Student` 类的接口文件。程序 12.6 显示了 `Student` 类的实现文件。

### 程序 12.5 文件 `student.h`

```cpp
************************************************
* Student 类的接口文件
************************************************/
#ifndef STUDENT_H
#define STUDENT_H
#include "person.h"

class Student: public Person
{
private:
    double gpa;
public:
    Student (string name, double gpa);
    virtual void print () const;
};
#endif
```

### 程序 12.6 文件 `student.cpp`

```cpp
1 *****************************************************
2 * Student 类的实现文件 *
3 *****************************************************/
4 #include "Student.h"
5 
6 // Student 类构造函数的定义
7 Student ::Student (string nm, double gp)
8 : Person (nm), gpa (gp)
9 {
10 
11 // Student 类虚 print 函数的定义
12 void Student ::print () const
13 {
14 Person ::print();
15 cout << "GPA: " << gpa << endl;
16 }
```

程序 12.7 显示了应用程序。

### 程序 12.7 文件 `app.cpp`

```cpp
1 *****************************************************
2 * 测试 Person 和 Student 类的应用程序文件 *
3 *****************************************************/
4 #include "Student.h"
5 
6 int main ()
7 {
8 // 创建多态变量的指针
9 Person *ptr;
10 // 在堆中实例化 Person 对象
11 ptr = new Person("Lucie");
12 cout << ptr << "Information";
13 cout << ptr->print();
14 delete ptr;
15 // 在堆中实例化 Student 对象
16 ptr = new Student("John", 3.9);
17 cout << ptr << "Information";
18 cout << ptr->print();
19 cout << endl;
20 delete ptr;
21 return 0;
22 }
```

### 程序 12.7 文件 `app.cpp` (续)

| 运行结果: Person 信息 \n Name: Lucie \n Student 信息 \n Name: John, GPA: 3.9 |

## 多态的更好用法

正如你所注意到的，在程序 12.3 中并不需要多态。我们可以在不需要指向不同对象的指针的情况下相同的结果。我们可以使用 `*person.print()*` 代替 `*ptr->print()*`，也可以使用 `*student.print()*` 代替 `*ptr->print()*`。然而，该程序仅通过一个可以指向不同对象的指针就展示了多态的思想。

更好的演示是当我们**必须**使用多态时。假设我们需要一个对象数组。我们知道数组的所有元素必须是相同类型；但但是，如果对象的类型不同，我们就无法使用对象数组。我们可以使用指针数组，其中每个指针都可以指向基类对象（上一个示例中的 `Person`）。换句话说，我们可以拥有一个*多态变量*的数组。程序 12.8 与程序 12.7 相同，不同之处在于使用了指针数组。

### 程序 12.8 在多态中使用指针数组

| 1 ********************************************************************* |

| 2 * 修改应用程序文件以展示使用指针数组的 |

| 3 * 多态实际用法。 |

| 4 ********************************************************************* |

| 5 #include "student.h" |

| 6 |

| 7 int main () |

| 8 { |

| 9 // 声明一个多态变量（指针）数组 |

| 10 Person* ptr[4]; |

| 11 // 在堆中实例化四个对象 |

| 12 ptr[0] = new Student("Joe", 3.7); |

| 13 ptr[1] = new Student("John", 3.9); |

| 14 ptr[2] = new Person("Bruce"); |

| 15 ptr[3] = new Person("Sue"); |

| 16 // 调用 Student 类的虚 print 函数 |

| 17 for (int i = 0; i < 4; i++) { |

| 18 ptr[i]->print(); |

| 19 delete ptr[i]; |

| 20 } |

| 21 return 0; |

| 22 } |

## 表 12.1 对 `type_info` 对象的的操作

| | |

|---|---|

| t1 == t2 | 如果 t1 和 t2 为相同类型，则返回 true |

| t1 != t2 | 如果 t1 和 t2 类型不同，则返回 true |

| t1.name() | 返回一个 C 字符串（t1 的名称） |

| t1.before (t2) | 如果 t1 位于 t2 之前（在继承关系中），则返回 true |

在编译期间进行。例如，在程序执行期间，不同的对象被插入到一个多态变量中，程序需要调用适当的函数，但这种绑定必须在运行时完成。出于这个原因，我们需要一个虚函数来创建一个显示对象需求的表，并将调用绑定到相应的函数。多态与我们希望能够执行相应的函数定义的动态行为紧密相关。

## 12.14 运行时信息 (RTTI)

在处理类层次结构时，有时我们需要知道我们正在处理的对象的类型，并且想要更改对象的类型。

## 使用运算符

如果我们想在运行时查找对象的类型，可以使用 `<typeinfo>` 头文件来访问类型为 `type_info` 的类对象（注意类名有下划线，但头文件名称没有）。`type_info` 类没有构造函数、析构函数或拷贝构造函数。创建 `type_info` 类型对象的唯一方法是使用重载的运算符 `typeid`。我们可以通过向运算符 `typeid` 传递一个可以被求值为类型的表达式来创建一个 `type_info` 类型的对象；例如：`typeid(5)`、`typeid(object_name)`、`typeid(6 + 2)` 等。然后我们可以使用 `type_info` 类中定义的四个成员函数或运算符之一，如表 12.1 所示，其中 t1 和 t2 是 `type_info` 类的对象。

程序 12.9 显示了如何找到这些对象的类型。

## 程序 12.9 测试 type 运算符

```
*****************************************************************
* 一个使用 typeid 运算符查找类名称的程序 *
*****************************************************************
#include <iostream>
#include <string>
#include <typeinfo>
using namespace std;

class Animal {};
class Horse {};

int main () {
{
(续)
```

## 程序 12.9 测试 `typeid` 运算符（续）

```cpp
|| 14 Animal a;
| 15 Horse h;
| 16 cout << typeid(a).name() << endl;
| 17 cout << typeid(h).name();
| 18 return 0;
| 19 }
```

运行结果：

6Animal

5Horse

注意，类名的前缀是每个用例中字符的数量（6 和 5）。

## 使用动态转换运算符 (`dynamic_cast`)

我们已经看到在多态关系中，我们可以对指针进行向上转换（upcast），这意味着我们在派生类中创建一个指针使其指向基类，如下：

```
Person* ptr1 = new Student
```

在这里，从 `new` 运算符返回的指针是一个指向 `Student` 对象的指针，但我们将其赋值为指向 `Person` 对象（指针被向上转换）。

C++ 也可以对指针进行向下转换（downcast），使其指向层次结构中较低层的对象。可以使用所示的 `dynamic_cast` 运算符来实现：

```
Student* ptr2 = dynamic_cast<Student*>(ptr1)
```

这证明了 `Student` 是派自 `Person` 类的类，因为 `ptr1` 可以向下转换为 `ptr2`。一些程序员认为这是类型检查的形式。然而，我们不建议程序员使用 `dynamic_cast` 运算符进行类型检查，因为它涉及大量的开销。

## 12.2 其他问题

在本节中我们将讨论类和多继承。我们包含了一个使用多层继承类的项目。

### 12.2.1 抽象类

我们到目前设计的类都是具体类。具体类可以被实例化并创建对象。当我们创建一组类时，有时会发现有一组行为对所有类都是相同的。例如，我们定义了两个名为 `Rectangle` 和 `Square` 的类。这两个类至少有两个共同行为：`getArea()` 和 `getPerimeter()`。我们是否能强迫这两个类的创建者（特别是当每个类由不同的实体创建时）为每个类提供这两个成员函数的定义？我们知道，寻找每个类的公式必须创建它们各自的 `getArea` 和 `getPerimeter` 版本。

面向对象编程的解决方案是创建一个抽象类，它强迫所有派生类的设计者向它们的类中添加这两个定义。一个包含抽象类的类集必须具有纯虚函数的声明和定义。

## 抽象类是至少包含一个纯虚函数的类

## 纯虚函数的定义

抽象类是至少包含一个纯虚函数的类。纯虚函数是一个声明被设置为零的虚函数，且在抽象类中没有定义。以下显示了 `Shape` 类的两个虚成员函数：

```
virtual double getArea () = 0;
virtual double getPerimeter() = 0;
```

## 纯虚函数的定义（续）

抽象类不定义其纯虚函数，但继承自抽象类的每个类必须提供每个纯虚函数的定义，或者将其声明为纯虚以便在层次结构的更低层中定义。

## 不可实例化

抽象类不定义其纯虚函数，因此无法被实例化。

# 程序 12.12 文件 `square.cpp` (续)

```cpp
// Finding the area
double Square ::getArea () const
{
    return (side * side);
}
// Finding the perimeter
double Square ::getPerimeter () const
{
    return (4 * side);
}
// Private isValid function
bool Square ::isValid () const
{
    return (side > 0.0);
}
```

程序 12.13 是 `Rectangle` 类的接口文件。它有两个数据成员、一个私有成员函数和三个公共成员函数。

# 程序 12.13 文件 `rectangle.h`

```cpp
/* The interface file for the Rectangle class */
#ifndef RECTANGLE_H
#define RECTANGLE_H
#include "shape.h"
// Class definition
class Rectangle : public Shape
{
private:
    double length;
    double width;
    bool isValid () const;
public:
    Rectangle (double length, double width);
    ~Rectangle ();
    void print () const;
    double getArea () const;
    double getPerimeter () const;
};
#endif
```

# 程序 12.14 文件 `rectangle.cpp`

```cpp
| 1 | *****************************************************|
| 2 | * The implementation file the Rectangle class    * |
| 3 | ***************************************************** / |
| 4 | #include "rectangle.h" |
| 5 | |
| 6 | // Constructor |
| 7 | Rectangle :: Rectangle (double lg, double wd) |
| 8 |     length (lg), width (wd) |
| 9 | { |
| 10 |     if (isValid()) |
| 11 |     { |
| 12 |         cout << "Invalid rectangle"; |
| 13 |         assert(false); |
| 14 |     } |
| 15 | } |
| 16 | // Destructor |
| 17 | Rectangle :: ~Rectangle() |
| 18 | {} |
| 19 | |
| 20 | // Definition of print function |
| 21 | void Rectangle :: print () const |
| 22 | { |
| 23 |     cout << "Rectangle of " << length << " X" << width << endl; |
| 24 | } |
| 25 | // Finding the area |
| 26 | double Rectangle :: getArea() const |
| 27 | { |
| 28 |     return length * width; |
| 29 | } |
| 30 | // Finding the perimeter |
| 31 | double Rectangle :: getPerimeter() const |
| 32 | { |
| 33 |     return 2 * (length + width); |
| 34 | } |
| 35 | // Private isValid function |
| 36 | bool Rectangle :: isValid() const |
| 37 | { |
| 38 |     return (length > 0.0 && width > 0.0); |
| 39 | } |
```

程序 12.14 是 `Rectangle` 类的实现文件。

程序 12.15 是 `Triangle` 类的接口文件。它有三个私有数据成员、一个私有成员函数和三个公共成员函数。

# 程序 12.15 文件 `triangle.h`

```cpp
/* *****************************************
* The interface file for the Triangle class
* ******************************************/
#ifndef TRIANGLE_H
#define TRIANGLE_H
#include "shape.h"

// Class definition
class Triangle : public Shape
{
    private:
    double side1;
    double side2;
    double side3;
    bool isValid() const;
public:
    Triangle(double side1, double side2, double side3);
    Triangle();
    void print() const;
    double getArea() const;
    double getPerimeter() const;
};
#endif
```

程序 12.16 是 `Triangle` 类的实现文件。

# 程序 12.16 文件 `triangle.cpp`

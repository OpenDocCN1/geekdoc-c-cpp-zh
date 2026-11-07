
（单例模式），但暂时假设只创建一个注册器对象。程序 11.42 然后创建三个 Student 对象和三个 Course 对象。注册器对象负责将学生注册到他们想要的课程中。注意，我们没有从 *StudentSchedule* 或 *CourseRoster* 类实例化任何对象。第一个在 *Student* 类中实例化，第二个在 *Course* 类中实例化。

## 程序 11.42 文件 application.cpp

```cpp
 1 /********************************************************
 2  * The application file to test classes in Registration project *
 3  ********************************************************/
 4 #include "registrar.h"
 5
 6 int main ( )
 7 {
 8     // Instantiation of a Registrar object
 9     Registrar registrar;
10     // Instantiation of three student objects
11     Student student1 ("John");
12     Student student2 ("Mary");
13     Student student3 ("Ann");
14     // Instantiation of three course objects
15     Course course1 ("CIS101", 4);
16     Course course2 ("CIS102", 3);
17     Course course3 ("CIS103", 3);
18     // Let the registrar object enroll students in the courses
19     registrar.enroll (student1, course1);
20     registrar.enroll (student1, course2);
21     registrar.enroll (student2, course1);
22     registrar.enroll (student2, course3);
23     registrar.enroll (student3, course1);
24     // Printing the information about each student
25     student1.print();
26     student2.print();
27     student3.print();
28     // Printing information about each course
29     course1.print();
30     course2.print();
31     course3.print();
32     return 0;
33 }
Run:
Student name: John
List of Courses
CIS101
CIS102

Student name: Mary
List of Courses
CIS101
CIS103

Student name: Ann
List of Courses
CIS101

Course Name: CIS101
Number of Units: 4
List of Students
John
Mary
Ann

Course Name: CIS102
Number of Units: 3
List of Students
John

Course Name: CIS103
Number of Units: 3
List of Students
Mary
```

## 关键术语

- aggregation
- association
- base class
- composition
- dependency
- derived class
- inheritance
- inheritance tree
- Liskov substitution principle
- multiplicity
- private inheritance
- protected inheritance
- protected member
- public inheritance
- subclass
- superclass

## 小结

面向对象编程中的*继承*从更一般的概念派生出更具体的概念。更一般的类称为基类，更具体的类称为派生类。派生类继承基类的所有成员，但参数构造函数、默认构造函数、复制构造函数、析构函数和赋值运算符除外。继承类型有三种：公有、保护和私有；默认是私有，但最常见的是公有。

两个类之间的*关联*表示它们之间的关系。*聚合*是一种特殊关联，其中关系涉及所有权，即“has-a”关系。*组合*是一种特殊聚合，其中被包含对象的生命周期取决于容器对象的生命周期。

*依赖*是类之间的一种弱关系。它建模“uses”关系。

## 问题

**PR-1.** 假设我们已经定义了以下两个类。使用委托为这两个类编写 *set* 和 *print* 函数的定义。

```cpp
// Declaration of the class First
class First
{
    private:
        int a;
    public:
        void set (int a);
        void print () const;
};
// Declaration of the class Second
class Second : public First
{
    private:
        int b;
    public:
        void set (int a, int b);
        void print () const;
};
```

**PR-2.** 假设我们已经定义了以下两个类。不使用委托为这两个类编写 *set* 和 *print* 函数的定义。

```cpp
// Declaration of the class First
class First
{
    protected:
        int a;
    public:
        void set (int a);
        void print () const;
};
// Declaration of the class Second
class Second : public First
{
    private:
        int b;
    public:
        void set (int a, int b);
        void print () const;
};
```

**PR-3.** 假设我们有一个如下定义的类 *First*。如果类 *Second* 是类 *First* 的公有派生类，那么成员 *one*、*two* 和 *set* 在类 *Second* 中的可访问性是什么？

```
class First
{
    private:
        int one;
    protected:
        int two;
    public:
        void set (int one, int two);
}
```

**PR-4.** 重复 PR-3，但假设类 *Second* 是类 *First* 的保护派生类。

**PR-5.** 重复 PR-4，但假设类 *Second* 是类 *First* 的私有派生类。

**PR-6.** 我们有以下三个类定义。为所有三个类编写构造函数和 print 函数的定义。

```
// Definition of class First
class First
{
    private:
        int a;
    public:
        First (int a);
        void print ( ) const;
};
// Definition of class Second
class Second : public First
{
    private:
        int b;
    public:
        Second (int a, int b);
        void print ( ) const;
};
// Definition of class Third
class Third : public Second
{
    private:
        int c;
    public:
        Third (int a, int b, int c);
        void print ( ) const;
};
```

**PR-7.** 我们有以下三个类定义。为所有三个类编写构造函数和 print 函数的定义。

```cpp
// Definition of class First
class First
{
    private:
        int a;
    public:
        First (int a);
        void print ( ) const;
};
// Definition of class Second
class Second : public First
{
    private:
        int b;
    public:
        Second (int a, int b);
        void print ( ) const;
};
// Definition of class Third
class Third : public First
{
    private:
        int c;
    public:
        Third (int a, int c);
        void print ( ) const;
};
```

**PR-8.** 我们有以下两个类定义。为这两个类编写构造函数和 print 函数的定义。

```cpp
// Definition of class First
class First
{
    private:
        int a;
        double b;
    public:
        First (int a, double b);
        void print ( ) const;
};
// Definition of class Second
class Second
{
    private:
        First f;
        char c;
    public:
        Second (First f, char c);
        void print ( ) const;
};
```

- **PR-9.** 为程序 11.6 中 *main* 与 *Person* 和 *Student* 对象的交互绘制序列图。
- **PR-10.** 为程序 11.6 中 *main* 与 *Person* 和 *Date* 对象的交互绘制序列图。注意，我们有两个 *Person* 类的实例和两个 *Date* 类的实例。
- **PR-11.** 为程序 11.21 中对象的交互绘制序列图。

## 编程项目

**PRG-1.** 设计一个名为 *Square* 的类，它定义正方形几何形状。该类必须有一个名为 *side* 的数据成员，用于定义每条边的长度。然后定义两个成员函数 *getPeri* 和 *getArea*，用于求正方形形状的周长和面积。现在定义一个 *Cube*，它定义立方体形状，并从 *Square* 类继承。类 *Cube* 不需要新的数据成员，但需要成员函数 *getArea* 和 *getVolume*。为这两个类提供适当的构造函数和析构函数。

**PRG-2.** 设计一个名为 *Rectangle* 的类，它有两个私有数据成员：*length* 和 *width*。为该类定义构造函数和析构函数，并编写成员函数来求矩形的周长和面积。然后定义一个名为 *Cuboid*（表示长方体盒子）的类，它从 *Rectangle* 类继承，并额外有一个数据成员：*height*。然后为 *Cuboid* 类编写构造函数和析构函数，并编写成员函数来求 *Cuboid* 对象的表面积和体积。

**PRG-3.** 创建一个 *Sphere* 类，它从 *Circle* 类继承。我们知道，可以通过让圆绕其直径旋转来创建球体对象。

- a. 为名为 *circle* 的类设计一个接口，该类有一个私有数据成员：*radius*。为该类定义参数构造函数和析构函数，并使用以下关系编写成员函数来求圆的周长和面积。

| `perimeter = 2 * π * radius` | `area = π * radius * radius` |
| --- | --- |

- b. 为名为 *Sphere* 的类定义接口文件。同时为该类定义参数构造函数和析构函数，并编写成员函数来求球体的表面积和体积。

- c. 为类 *Sphere* 定义实现文件，使用以下公式求球体的表面积和体积；在公式中，*perimeter* 是圆的周长，*area* 是第 (b) 部分中定义的圆的面积。

| `surface = 2 * radius * perimeter` | `volume = (4 / 3) * radius * area` |
| --- | --- |

- d. 编写一个应用程序文件来测试 *Circle* 和 *Sphere* 类。

**PRG-4.** 创建一个 *Cylinder* 类，它从 *Circle* 类继承。我们知道，可以通过给圆对象增加高度来创建圆柱体对象。

- a. 按 PRG-3 中的方式为名为 *circle* 的类设计一个接口。

- b. 为名为 *Cylinder* 的类定义接口文件。同时为该类定义参数构造函数和析构函数，并编写成员函数来求球体的表面积和体积。


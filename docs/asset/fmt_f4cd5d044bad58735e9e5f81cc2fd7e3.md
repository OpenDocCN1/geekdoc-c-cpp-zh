
运行结果：
Person Information:
Person's Identity: 11111111

Student Information:
Student's identity: 222222222
Student's GPA: 3.9

- a. 该程序中有三个要点：我们实例化了一个 `Person` 类的对象，同时也实例化了一个 `Student` 类的对象。
- b. 然而，如果我们没有为 `Student` 类定义数据成员 `identity`，则该类的对象将从 `Person` 类继承 `identity`。
- c. 我们使用 `identity`（身份标识）而不是 `name`（名称）来标识一个人。我们使用 `identity` 是因为 `name` 的类型是 `string`，这是一种类类型；如果我们使用 `name`，实际上是在继承关系中增加了一个组合关系，但我们尚未定义这种组合关系。

## 私有数据成员

在深入研究继承主题之前，我们先讨论基类对象和派生类对象的内容。如图 11.7 所示，基类只有一个数据成员，而派生类有两个成员：一个是继承的，另一个是创建的。

在继承中，基类中的私有数据成员会被继承到派类类，但派生类无法直接访问它。必须通过基类的公有或保护成员函数来访问。如图 11.7 所示，基类只有一个数据成员，而派生类有两个成员：一个是继承的，另一个是创建的。

在继承中，基类中的私有数据成员会被继承到派生类，但派生类无法直接访问它。必须通过基类的公有或保护成员函数来访问。如图 11.7 所示，基类只有一个数据成员，而派生类有两个成员：一个是继承的，另一个是创建的。

## 公有成员

图 11.8 为派生类增加了公有函数。我们可以看到，基类有两个成员函数，而派生类有四个成员函数，其中两个是继承的，两个是新定义的。基类的成员对派生类可见。

## 访问私有成员

以下列表显示了如何访问私有成员：

- 在基类中，我们可以通过基类的公有函数访问私有成员。
- 在派生类中，我们需要通过基类的公有函数来访问私有成员：
  - a. 在基类中，我们可以通过基类的公有函数访问![](img/11.7)
  - b. 在派生类中，我们需要通过基类的公有函数来访问私有成员：
    - a. 在基类中，我们可以通过基类的公有函数访问![](img/11.7)
    - b. 在派生类中，我们需要通过基类的公有函数来访问私有成员：
      - a. 在基类中，我们可以通过基类的公有函数访问![](img/11.7)
      - b. 在派生类中，我们需要通过基类的公有函数来访问私有成员。

## 派生类中的同名函数

在之前的类中，*Person* 和 *Student* 具有用于设置成员的 `set` 函数和用于获取成员的 `get` 函数。在派生类中，我们可以使用基类中的同名 `set` 和 `get` 函数吗？答案是肯定的，我们必须使用重载或重写函数。

### 重载函数

正如第 6 章所述，重载函数具有相同的名称但不同的签名。例如：

```cpp
// Person 类
void set (long id);
// Student 类
void set (double);
```

### 重写函数

如果基类和派生类的函数签名相同，则该函数被重写。如下：

```cpp
// Person 类
double get ();
// Student 类
double get ();
```

## 类作用域

如果我们知道基类和派生类，就可以理解继承的作用域。基类具有作用域，派生类也有自己的作用域。然而，嵌套的层级没有限制。图11.9

## 类之间的关系

在 C++ 中，基类的作用域在派生类中也是可见的，但反之不然。系统如何区分调用哪个函数？也就是说，如果 `person` 和 `student` 是类对象，我们使用以下语句：

| Person 对象 | Student 对象 |
|---|---|
| `person.set(11111111);` | `student.set(3);` |
| `person.get();` | `student.get();` |

编译器根据以下规则调用函数：
- a. 编译器尝试在调用函数的类中查找匹配的函数。
- b. 如果没有找到，编译器将查看继承自父类的函数。
- c. 如果没有找到，搜索将继续直到到达基类。
- d. 如果在任何类中都未找到，则将发布编译错误。

## 委托职责

派生类中的重载或重写成员函数可以通过调用相应的成员函数，将其部分功能委托给上层类；对于 `void` 成员函数很容易实现，但对于返回值函数则需要返回两个值，这需要一个 `struct` 或类对象。

例如，派生类中的 setter 函数可以设计为设置 `Person` 类的数据成员 `identity` 以及其自身类的数据成员 `gpa`。然而，正如我们所说，`identity` 数据成员在 `Student` 类中是隐藏的，`Student` 类中的 `set` 函数无法访问，但它可以调用 `Person` 类的 `set` 函数。同样可以我们可以为 `Student` 类设计一个 `print` 函数来调用 `Person` 类的 `print` 函数来实现部分功能。以下显示了带有委托的 `set` 函数和 `print` 函数的定义。

| Person 对象 | Student 对象 |
|---|---|
| `void Person::set (long id)` | `void Student::set (long id, double gpa)` |
| `{` | `{` |
| `identity = id;` | `Person ::set(id); // 委托` |
| `}` | `gpa = gpa` |
| `}` | `}` |
| `void Person::print ()` | `void Student::print ()` |
| `{` | `{` |
| `cout << name;` | `Person ::print(); // 委托` |
| `}` | `cout << gpa` |
| `}` | `}` |

注意：要调用基类中的 `set` 函数或 `print` 函数，我们必须使用作用域解析符 `Person::set(...)` 或 `Person::print()`。

## 不继承的成员：调用

派生类中有五个成员函数是不继承的：默认构造函数、带参数的构造函数、拷贝构造函数、析构函数和赋值运算符。我们将赋值运算符的讨论推到了第 11 章，但在本章中将讨论另外四个。

构造函数和析构函数是不继承的，因为派生类对象自然比对应的基类对象拥有更多的成员。派生类的构造函数必须构造更多内容；派生类的析构函数必须销毁更多内容。

| 构造函数、析构函数和赋值运算符是不继承的；它们必须重定义。 |

然而，我们在这里面临一个困境：派生类的构造函数无法初始化基类的数据成员，因为它们在派生类中是 Format隐藏的。同样，派生类的析构函数无法删除基类的数据成员，因为它们在派生类中也是被隐藏的。

如果派生类的构造函数在初始化时调用基类的构造函数并初始化派生类的数据成员，问题就可以解决。同样，如果派生类的析构函数删除派生类的数据成员并调用基类的析构函数，问题也可以解决，如图 11.4 所示。

注意，构造函数和析构函数的执行顺序是相反的。由于析构函数是由系统而非用户调用的，这些操作在后台完成，除非用户使用了可能需要用户干预的指针或文件。

## 示例 11.4

表 11.1 并列了了 `Person` 和 `Student` 类的默认构造函数、带参数构造函数、拷贝构造函数和析构函数。注意派生类使用了基类的构造函数（调用）。调用基类构造函数后，初始化列表可以初始化派生类的私有成员。

调用拷贝构造函数时的 `st` 指的是一个 `Student` 对象。我们如何将这个对象传递给需要 `Person` 对象参数的 `Person` 拷贝构造函数呢？如果我们知道每当在使用基类对象的地方使用派生类对象时，对象会被切片（sliced），且属于派生类的数据成员会被丢弃，那么这个谜就可以解决了。换句话说，`Person (st)` 中的对象只是 `Student` 类中继承自 `Person` 的部分。

| 调用基类构造函数 | 删除继承的成员 | 初始化继承的成员 | 调用基类析构函数 |

图 11.10 继承中的构造函数和析构函数

## 表 11.1 构造函数和析构函数的定义

| 基类 | 派生类 |
| --- | --- |
| // 默认构造函数 | // 默认构造函数 |
| `Person::Person()` | `Student::Student()` |
| `: Identity(0)` | `: Person(0), gpa(0.0)` |
| `}` | `}` |
| // 带参数的构造函数 | // 带参数的构造函数 |
| `Person::Person(long id)` | `Student::Student(long id, double gp)` |
| `: identity(id),` | `: Person(id), gpa(gp)` |
| `{` | `}` |
| // 拷贝构造函数 | // 拷贝构造函数 |
| `Person::Person(const Person& obj)` | `Student::Student(const Person& st)` |
| `Identity(obj.identity)` | `: Person(st), gpa(std.gpa)` |
| `}` | `}` |
| // 析构函数 | 析构函数 |
| `Person::~Person()` | `Student::~Student()` |
| `}` | `}` |

图 11.11 显示了如何使用带参数的构造函数构造基类和派生类对象。在基类（`Person`）的情况下，我们必须初始化数据成员。在派生类（`Student`）中，我们可以通过调用基类的构造函数来构造继承部分，然后初始化新的数据成员。构造函数是公共成员，可以在派生类中访问。

## 委托与调用

委托（Delegation）和调用（Invocation）是不同的概念，实现方式也不同。在委托中，派生类成员使用类作用解析符 `(:)` 将其职责委托给基类。在调用中，派生类的构造函数在初始化期间直接调用基类的构造函数，这不需要类作用解析符。

![](img/ce9c99d45f71111839bc062830bd19fd_524_0.png)

## 11.1 继承 507

![](img/ce9c99d45f71111839bc062830bd19fd_525_0.png)

图 11.12 独立编译

## 独立编译

我们之前讨论过独立编译，但看到它在继承情况下是如何运作是非常有趣的，如图 11.12 所示。
该图揭示了几个点。`Person` 类和 `Student` 类由两个不同的实体编译，仅使用该类。`Person` 类和 `Student` 类可以访问 `Person` 的接口文件，因为 `Student` 类的接口文件包含了 `Person` 类的接口文件。

## 使用独立编译的示例

我们现在为这个包含构造函数、析构函数和其他函数的简单继承示例提供接口文件、实现文件和应用程序。我们增加了更多数据字段，但删除了 `set` 和 `get` 函数，仅使用 `print` 函数来打印人员或学生的信息。

### Person 类的接口文件和实现文件 我们首先给出 `Person` 类的接口文件和实现文件。该类是独立的，可以与应用程序配合使用。程序 11.2 显示了 `Person` 类的接口文件。

## 程序 11.2 文件 person.h

```cpp
****************************************************

/* Person 类的接口文件

****************************************************/

#ifndef PERSON_H

#define PERSON_H

#include <cassert>

#include <iostream>

#include <iomanip>

using namespace std;

class Person

{

(continued)
```

## 程序 11.2 文件 person.h (续)

```cpp
14 private:
15 long identity;
16 public:
17 Person();
18 Person(long identity);
19 ~Person();
20 Person(const Person& person);
21 void print() const;
22 };
23 #endif
```

程序 11.3 显示了 `Person` 类的实现文件。

## 程序 11.3 文件 person.cpp

```cpp
1 *************************************/
2 * Person 类的实现文件
3 *************************************/
4 #include "person.h"
5 // 默认构造函数
6 Person::Person()
7 {
8 }
9 // 带参数的构造函数
10 Person::Person(long id)
11 : identity(id)
12 {
13 assert(identity >= 100000000 && identity <= 999999999);
14 }
15 // 拷贝构造函数
16 Person::Person(const Person& person)
17 : identity(person.identity)
18 {
19 }
20 // 析构函数
21 Person::~Person()
22 {
23 }
24 // 访问成员函数
25 void Person::print() const
26 {
27 cout << "Identity: " << identity << endl;
28 }
```

## 程序 11.4 文件 student.h

```cpp
/* Student 类的接口文件 */
#ifndef STUDENT_H
#define STUDENT_H
#include "person.h"
class Student: public Person {
private:
    double gpa;
public:
    Student();
    Student(long identity, double gpa);
    ~Student();
    Student(const Student& student);
    void print() const;
};
#endif
```

### Student 类的接口文件和实现文件 我们现在给出继承自 `Person` 类的 `Student` 类的接口文件和实现文件。程序 11.5 显示了 `Student` 类的实现文件。

## 程序 11.5 文件 student.cpp

```cpp
/* Student 类的实现文件 */
#include "student.h"
// 默认构造函数
Student::Student() : Person( ), gpa(0.0)
{
}
// 带参数的构造函数
Student::Student(long identity, double gpa) : Person (id), gpa (gpa)
{
    assert (gpa >= 0.0 && gpa <= 4.0);
}
// 拷贝构造函数
Student::Student(const Student& student)
```
(continued)

## 第 11 章 类之间的关系

## 程序 11.5 文件 student.cpp (续)

```cpp
19 : Person (student), gpa (student.gpa)
20 {
21 }
22 // 析构函数
23 Student ::~Student()
24 {
25 }
26 // 访问器成员函数
27 void Student::print() const
28 {
29 Person :: print();
30 cout << "GPA: " << fixed << setprecision(2) << gpa << endl;
31 }
```

使用这些类的应用程序程序 11.6 显示了应用程序文件的简单示例。客户端可以创建任何应用程序文件并使用 `Person` 和 `Student` 类。

## 程序 11.6 文件 app.cpp

运行：
关于人的信息：
身份: 111111111

关于学生的信息：
身份: 222222222
GPA: 3.90

### 11.1.3 关于公继承的更多内容

在本节中，我们将讨论关于公继承的额外问题。

### 保护成员

到为止，我们只讨论了类中的私有成员和公共成员。C++ 还为成员定义了另一种类型，*protected*（保护）。*protected* 成员在基类中的作用类似于私有成员（或者在没有派生的情况下）。当我们扩展一个类时，*protected* 成员的作用就会体现出来。*protected* 成员在派生类以及所有派自派生类的类中都是可访问的。换句话说，保护成员像私有成员一样被继承，但它不会在派生类中隐藏。派生类中定义的函数可以轻松访问 *protected* 成员，而无需调用继承自基类的函数。图 11.13 显示了这种差异。

图 11.13 显示了两种情况。在第一种，我们只有一个数据成员和一个公共成员。当我们使用派生时，私有成员被隐藏了。虽然函数 `set(x)` 是公有的并且在派生类中可见，但无法直接调用，因为参数 `x` 是不可见的。我们需要创建另一个函数，使用占位变量 `y` 来访问 `x`，如下所示：

```cpp
void Derived::set (int y)
{
    Base::set (y); // 调用继承的函数
}
```


- 11.40 假设有两个类 `Big` 和 `Small`。编写一个将 `Small` 类型对象转换为 `Big` 对象的构造函数。

## 聚合与组合

概念：当一个类拥有另一个类的对象时，发生了类聚合。组合是聚合的形式，其中所有者控制被包含对象的生命周期。

在第 7 章中，你学习了类可以包含其他类。当类 `C` 包含一个另一个类 `D` 的成员时，每个 `C` 对象都拥有一个 `D` 对象。这在 `C` 和 `D` 之间创建了“拥有”关系。在这种关系中，`C` 的实例拥有 `D` 的实例。在 C++ 中，所有权通常由于 `C` 拥有类型为 `D` 的成员产生，但也可能是由于 `C` 拥有指向 `D` 对象的指针。聚合术语被泛用于描述类对象拥有类对象的情况。

## 初始化列表

考虑以下 `Person` 和 `Date` 类。

```cpp
class Date
{
    string month;
    int day, year;
public:
    Date(string m, int d, int y)
    {
        month = m;
        day = d;
        year = y;
    }
}
```

```cpp
class Person
{
    string name;
    dateOfBirth;
public:
    Person(string n, Date d)
    {
        name = n;
        dateOfBirth = d;
    }
}
```

以下代码展示了如何使用初始化列表来初始化成员变量。这比在构造函数体内赋值更高效。

```cpp
class Date
{
    string month;
    int day, year;
public:
    Date(string m, int d, int y) : month(m), day(d), year(y)
    {
    }
}
```

```cpp
class Person
{
    string name;
    dateOfBirth;
public:
    Person(string n, Date d) : name(n), dateOfBirth(d)
    {
    }
}
```

注意，初始化列表中的变量顺序应与它们在类中声明的顺序一致。如果不匹配，编译器将按照声明的顺序进行初始化，这可能会导致意想不到的结果。

# 第 11 章 更多关于类与面向对象编程

## 程序 11-21（续）

```cpp
{
  cout << "Date-Of-Birth object for person "
  << personID << " has been destroyed.\n";
}
class Country {
  string name;
public:
  Country(string name) : name(name) {
    cout << "A Country object has been created.\n";
  }
  ~Country() { cout << "A Country object has been destroyed.\n"; }
};
class Person {
  string name;
  DateOfBirth dateOfBirth;
  int personID; // 人员身份号 (PID)
  shared_ptr<Country> pCountry;
public:
  Person(string name, string month, int day,
    int year, shared_ptr<Country>& pC )
  : name(name), dateOfBirth(month, day, year), personID(uniquePersonID),
    pCountry(pC) {
    cout << "Person object "
    << personID << " has been created.\n";
    Person::uniquePersonID++;
  }
  ~Person() {
    cout << "Person object "
    << personID << " has been destroyed.\n";
  }
  static int uniquePersonID; // 用于生成 PID
};
// 定义静态类变量
int Person::uniquePersonID = 1;
int main() {
  // 创建一个 Country
```

## 11.11 聚合与组合

### “有一个”关系 (Has-A Relation)

当一个类包含另一个类的实例时，第一个类被认为与第二个类之间存在着“有一个”（has-a）的关系。例如，`Acquaintance` 类以 `dob` 成员的形式拥有一个 `Date` 类，而 `Date` 类以 `month` 成员的形式拥有一个 `string` 对象。在面向对象系统的设计过程中，“有一个”关系对于建模类与对象之间的关系至关重要。程序中类之间的另一个重要关系是“是一个”（is-a）关系，我们将在讨论完继承概念后的后续章节中讨论它。因此，对象组合实现了“有一个”关系，而正如我们后面看到的，继承是实现“是一个”关系的一种方式。

## 继承

### 一般化与特化 (Generalization and Specialization)

在现实世界中，你可以找到许多其他对象的特化版本。例如，“昆虫”一词描述了一种具有众多特征的非常通用生物。因为蝗虫和大蜜蜂都是昆虫，所以它们具有昆虫的所有通用特征。此外，它们还有自己的特殊特征。例如，蝗虫具有跳跃能力，而蜜蜂有刺针。蝗虫和蜜蜂都是昆虫的特化版本。这在图 11-5 中所示。

### 图 11-5

![](img/1c095ef63c71a34f9802f104f947be57_816_0.png)

### 继承与“是一个”关系

当一个对象是另一个对象的特化版本时，它们之间就存在“是一个”（is-a）的关系。例如，蝗虫是一种昆虫。以下是“是一个”关系的其他例子：

- 贵宾是一种狗。
- 汽车是一种车辆。
- 矩形是一种形状。

当对象之间存在“是一个”关系时，意味着特化对象具有通用对象的所有特征，以及使其变得特殊的额外特征。在面向对象编程中，继承被用于在类与类之间创建“是一个”关系。

继承涉及基类和派生类。基类是通用类，派生类是特化类。派生类基于基类或源自基类。你可以将基类视为父类，派生类视为类。这在图 11-6 中所示。

### 图 11-6

| 昆虫类 | 基类 |
| :--- | :--- |
| 成员 | (父) |
| 蝗虫类 | 派生类 |
| | 成员 | (子) |

派生类继承基类的成员变量和成员函数，而无需重写其中任何一个。此外，可以在派生类中添加新的成员变量和函数，使其比基类更具特化。举个具体的例子，考虑学院或大学环境，其中既有学生也有教职员工。假设我们有一个 `Person` 类，包含一个 `name` 数据成员以及用于处理该成员的成员函数：

```cpp
class Person {
  private:
    string name;
  public:
    Person() { setName(""); }
    Person(const string& pName) { setName(pName); }
    void setName(const string& pName) { name = pName; }
    string getName() const { return name; }
};
```

假设我们列出了以下类型

```cpp
enum class Discipline {ARCHEOLOGY, BIOLOGY, COMPUTER_SCIENCE};
enum class Classification {FRESHMAN, SOPHOMORE, JUNIOR, SENIOR};
```

来定义所提供的学科范围以及学生的分类。我们可以使用这些类型来定义继承自 `Person` 的 `Student` 和 `Faculty` 类。这是合理的，因为学生是“人”，教职员工也是“人”。

要通过继承定义一个类，我们需要指定基类以及派生类为基类添加的额外成员。

```cpp
class Student : public Person {
  private:
    Discipline major;
    shared_ptr<Person> advisor;
  public:
    void setMajor(Discipline d) { major = d; }
    Discipline getMajor() const { return major; }
    void setAdvisor(shared_ptr<Person> p) { advisor = p; }
    shared_ptr<Person> getAdvisor() const { return advisor; }
};
```

## 11.12 继承

每当涉及继承时，所有对象都应该动态分配并通过指针访问。为了理解原因，考虑一个处理 `Student` 和 `Person` 类型的程序。因为 `Student` 是 `Person`，我们应该能够将 `Student` 对象传递给期望 `Person` 参数的函数，或者将 `Student` 对象赋值给 `Person` 变量：

```cpp
Person p;
Student s;
p = s;
```

然而，带有额外成员的 Student 对象无法放入 Person 对象分配的内存位置。为了执行这种赋值，编译器将切掉不属于 `Person` 的 `Student` 部分，只保留继承的部分，从而导致信息丢失。如果我们处理的是大小相同的指针，这种情况就不会发生。

# 第11章 更多关于类和面向对象编程

```cpp
31 class Faculty : public Person
{
private:
  Discipline department;
public:
  void setDepartment(Discipline d) { department = d; }
  Discipline getDepartment() const { return department; }
};
```

# 程序 11-22

### 程序输出

印第纳·琼斯教授在考古系授课

# 基类与派生类

我们可以将一个类看作是描述具有某些特征的所有对象的集合。派生类的对象继承了基类的所有特征，因此可以被视为属于基类。由于这个原因，派生类通常被称为基类的子类（subclass），而基类被称为派生类的超类（superclass）。

# 多重继承

C++ 支持多重继承，即派生类同时派自两个或多个基类。虽然多重继承很有趣，但它可能导致程序非常难以理解，在实践中很少使用。你可以在书籍辅助网站的附录 H 中找到关于它的讨论。

书籍辅助网站上的附录 F 展示了如何使用 UML 表示继承。

# 11.13 保护成员与类访问

> 概念：基类的保护成员与私有成员相似，但它们可以被派生类访问。基类的访问修饰符决定了私有、保护和公共类成员在被派生类继承时如何被访问。

现在你在类内部使用了两种访问修饰符：`private`（私有）和 `public`（公共）。C++ 提供了第三种访问修饰符：`protected`（保护）。基类的保护成员与私有成员相似，但可以被派生类的成员函数访问。保护成员对程序中的所有其他代码都是不可访问的。

假设我们想为 `Faculty` 类添加一个构造函数，接收教授的名字和部门作为参数。实现此点的最佳方法是让构造函数继承 `Person` 类的 `setName()`。然而，为了说明保护成员的使用，我们将 `Person` 类 `name` 的访问修饰符改为保护，并让 `Faculty` 构造函数访问它。我们对 `Student` 类进行了简单的修改，添加了一个接收参数并设置保护成员 `name` 的构造函数。结果代码存储在 `inheritance.h` 文件中：

Inheritance.h 内容

```cpp
#include <string>
#include <memory>
using namespace std;
enum class discipline (ARCHEOLOGY, BIOLOGY, COMPUTER_SCIENCE);
enum class Classification (FRESHMAN, SOPHOMORE, JUNIOR, SENIOR);
```

友元函数和友元类可以访问私有和保护成员

```cpp
class Person
{
protected:
  string name;
public:
  Person() : setName(""); }
  Person(const string& pname) : setName(pname);
  void setName(const string& pname) { name = pname; }
  string getName() const { return name; }
};

class Student : public Person
{
private:
  Discipline major;
  shared_ptr<Person>* advisor;
public:
  // 构造函数
  Student(const string& sname, Discipline d, shared_ptr<Person>* adv);

  void setMajor(Discipline d) { major = d; }
  Discipline getMajor() const { return major; }
  void setAdvisor(const shared_ptr<Person>& p) { advisor = p; }
  shared_ptr<Person> getAdvisor() const { return advisor; }
};

class Faculty:public Person
{
private:
  Discipline department;
public:
  // 构造函数
  Faculty(const string& fname, Discipline d)
  {
    // 访问保护基类成员
    name = fname;
    department = d;
  }
  // 其他成员函数
  void setDepartment(Discipline d) { department = d; }
  Discipline getDepartment() const { return department; }
};
```

inheritance.cpp 内容

```cpp
#include "inheritance.h"
//********************************
// Student 类的构造函数。
//********************************
Student::Student(const string& sname, Discipline d, shared_ptr<Person>* adv)
{
  // 访问保护成员
  name = sname;
  // 访问其他成员
  major = d;
  advisor = adv;
}
```

程序 11-23 展示了这些类的使用。

```cpp
// 此程序演示了派生类对象的使用。
#include "inheritance.h"
#include <iostream>
#include <memory>
using namespace std;

// 这些字符串数组用于打印枚举类型的值
const string dName[] = { "Archeology", "Biology", "Computer Science" };
const string cName[] = { "Freshman", "Sophomore", "Junior", "Senior" };

int main()
{
  // 创建 Faculty 和 Student 对象
  shared_ptr<Faculty> prof = Faculty("Indiana Jones", ARCHEOLOGY);
  shared_ptr<Student> st = make_shared<Student>("Sean", ARCHEOLOGY, prof);

  cout << "Professor " << prof->getName() << " teaches " << dName[(int)prof->getDepartment()] << endl;

  // 获取学生的导师
  shared_ptr<Person> pAdvisor = st->getAdvisor();
  cout << "advisor is " << pAdvisor->getName() << "." << endl;

  return 0;
}
```

### 程序输出

印第纳·琼斯教授教的是考古学。

Sean 的导师是印第纳·琼斯。

虽然我们的示例没有显示，但基类的成员函数也可以被声明为保护。保护成员函数也可以被访问。

# 访问修饰符

除了 `public`，C++ 允许允许使用 `protected` 和 `private` 作为访问修饰符，如下例（不完整）所示

```cpp
class Cat : protected Feline
class Dog : private Canine
```

不要混淆访问修饰符和成员修饰符。访问修饰符决定了基类成员在被派生类继承时的访问类型。表 11-3 和图 11-8 展示了这种关系。

# 表 11-3 访问修饰符

| 基类访问修饰符 | 继承情况 |
|---|---|
| `private` | 基类的私有成员对派生类不可访问。基类的保护成员变为派生类的私有成员。基类的公共成员变为派生类的私有成员。 |

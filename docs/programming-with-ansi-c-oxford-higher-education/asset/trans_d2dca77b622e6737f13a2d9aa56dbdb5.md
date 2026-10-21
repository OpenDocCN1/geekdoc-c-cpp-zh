

## 程序 9.5 访问声明以将特定继承成员用于不同目的

```
//AccessDeclaration.cpp
#include <iostream>
using namespace std;

class Base
{
protected:
    int SpecialProtectedInt;
public:
    int SpecialInt;
    int NormalInt;
};

class Derived : private Base
{
protected:
    Base::SpecialProtectedInt;
    /* Making this protected integer specially available to the object of the derived class */
public:
    Base::SpecialInt;
    /* Making this integer specially available to the object of the derived class */
    // Using Base::SpecialInt;
    /* Newer way of writing the same */
    void SetSpecialProtectedIntOfBase()
    {
        SpecialProtectedInt = 10;
    }
};

void main()
{
    Derived DerivedObject;
    // DerivedObject.NormalInt = 10;
    /* This statement, if not commented, would not be compiled */
    DerivedObject.SpecialInt = 20;
    DerivedObject.SetSpecialProtectedIntOfBase();
}
```

## 程序的工作原理

语句 Base::SpecialInt; 重新定义了派生类 public 访问说明符头中的 SpecialInt，从而使其特别公开。所有其他数据仍保持私有。因此，NormalInt 仍为私有。请注意，SpecialProtectedInt 也已被重新定义为在派生类中保持受保护。访问声明是一个很好的功能；然而，它有以下限制：

- 1. 访问说明符不能被修改以提高原始访问说明符的状态。这意味着如果基类中有私有或受保护成员，则不能在派生类中将其重新定义为 public。

- 2. 前一条陈述的后果是，具有 public 访问指定的成员可以用 public 或 protected 访问重新定义，而受保护的成员只能重新定义为 protected。

如程序 9.5 所示形式的访问声明已被弃用，即不建议在新程序中使用；访问声明的相同效果也可以通过关键字 using 实现。对于编写新程序，必须使用此关键字。using Base::SpecialProtectedInt; 和 using Base::SpecialInt; 是替换旧定义的方法（即在旧定义前加上关键字 using）。我们在第 14 章学习命名空间时将讨论如何使用此关键字。

## 9.9 从单个类派生多个类

可以从单个类派生多个类。假设有一些 Student 类，例如 SchoolStudent、UndergraduateStudent 和 PostgraduateStudent。从设计角度来看，必须查看所有此类可能的类并找出它们中的共同元素。然后，用这些元素创建 Student 类（它们所有类的基类）。因此，基类的内容是在确定派生类内容之后决定的。在程序 9.6 中，我们有从 student 类继承的艺术、商业和科学学生。假设需要为艺术学生存储以下信息：

- 1. 姓名
- 2. 地址
- 3. 高中社会科学科目的成绩
- 4. 高中的排名
- 5. 高中的学校名称

此外，可能需要添加有关创意艺术作品（如诗歌或故事）的信息。

> 注 有些书称之为分层继承，这是不标准的；因此，我们更喜欢不使用该短语来描述从单个类派生多个类的情况。

对于科学学生，应考虑高中科学科目和实践科目的成绩，除语言科目外。不仅要考虑讲座时间表，还要考虑实践时间表。为简单起见，两个时间表都假定为字符串；在现实场景中，它们可能是一个从文件中读取的表格。

对于商业学生，应考虑商业科目详情。可能需要添加有关在某些私营公司实习的详情。此信息也假定包含在字符串中。

可以观察到，详情的一些部分特定于学科类型，而其他详情是共同的。应创建包含共同详情的学生类，然后继承这三个类。请考虑程序 9.6。

## 程序 9.6 从单个类继承多个类

```
//StudentInherited.cpp
#include <iostream>
#include <string>
using namespace std;
const int Languages = 2;
const int Science = 3;
const int Commerce = 2;
```

```
class student
{
protected:
    string Name;
    string Address;
    char Grade;
    string NameofSchool;
public:
    student(string TempName, string TempAddress, char TempGrade, string TempNameofSchool)
    {
        Name = TempName;
        Address = TempAddress;
        Grade = TempGrade;
        NameofSchool = TempNameofSchool;
    }
};

// Derived class ArtsStudent
class ArtsStudent : public student
{
    int marks[Languages];
    string LanguageName;
public:
    /* Note how the members are initialized using a member initialization list */
    ArtsStudent(string TempName, string TempAddress,
    char TempGrade, string TempNameofSchool,
    int TempMarks[], string TempLanguageName) : student(TempName, TempAddress, TempGrade,
    TempNameofSchool)
    {
        for(int i = 0; i < Languages; ++i)
        marks[i] = TempMarks[i];
        LanguageName = TempLanguageName;
    }
};

// Derived class ScienceStudent
class ScienceStudent : public student
{
    int marks[Science];
    string ScienceName;
    string PractSchedule;
public:
    ScienceStudent(string TempName, string TempAddress, char TempGrade, string
    TempNameofSchool, int TempMarks[], string TempScienceName, string TempPractSchedule) :
    student(TempName, TempAddress, TempGrade, TempNameofSchool)
    {
        for(int i = 0; i < Science; i++)
        marks[i] = TempMarks[i];
        ScienceName = TempScienceName;
        PractSchedule = TempPractSchedule;
    }
};

// Derived class CommerceStudent
class CommerceStudent : public student
{
    int marks[Commerce];
    string CompanyName;
```

```
public:
CommerceStudent(string TempName, string TempAddress, char TempGrade, string TempNameofSchool, int TempMarks[], string TempCompanyName) : student(TempName, TempAddress, TempGrade, TempNameofSchool)
{
for(int i = 0; i < Commerce; i++)
marks[i] = TempMarks[i];
CompanyName = TempCompanyName;
};
```

```
void main()
{
int ArtsMarks[] = {55,75};
int ScienceMarks[] = {89,78,97};
int CommerceMarks[] = {54,78};
CommerceStudent Lara("Lara", "West Indies", 'A', "Trinidad beach", CommerceMarks, "Under the sun");
ScienceStudent Beckham("David Beckham", "Karnataka", 'A', "Bangalore school", ScienceMarks, "Physics", "12to2daily");
ArtsStudent Steff("Steff", "C/o Agassi's address", 'A', "Germany school", ArtsMarks, "Silence");
}
```

## 程序的工作原理

该程序包含一个 student 类，并且有三个从它继承的类，即 ArtsStudent、CommerceStudent 和 ScienceStudent。student 类包含派生类共有的所有数据，即姓名、地址等。为所有这些类提供了构造函数，并在定义 student 时定义并使用它们。

这是一个非常简化的示例，尽管它在一定程度上变得有些复杂，特别是派生类中基类构造函数的调用。重要的是要注意，基类构造函数是使用成员初始化列表（MIL）调用的，这在第 5 章学习构造函数时已经讨论过。已经提到成员可以使用 MIL 初始化。当成员是一个类时（这里派生类具有基类作为成员），它使用 MIL 初始化。还要注意，基类对象只能使用 MIL 初始化，而不能在派生类对象的构造函数体中初始化。还要注意，派生类构造函数必须为基类对象（它是派生类的一部分）和派生类的其他成员的构造函数提供足够数量的参数。

> 注
> 基类对象只能使用 MIL 初始化。派生类构造函数必须有足够数量的参数来构造嵌入在派生类对象中的基类子对象以及派生类的其他成员。

继承的一个重要优点是将通用属性存储在基类的一个位置的便利。

该程序强调了当基类被多次继承时的优点。单个基类与所有从它继承的类共享。如果大学想在学生数据中添加所有学科所有学生的电子邮件地址，信息只需在一个地方添加，即 student 类。这就是继承的主要优点。假设在进一步的时期，需要处理工程学生，也是


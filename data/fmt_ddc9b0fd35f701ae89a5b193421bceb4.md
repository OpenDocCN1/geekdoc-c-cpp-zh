
```cpp
// 我们获得默认构造函数、析构函数
// 无声明
// Id(const Id &id) = default;
// ~Id() = default;
const string &GetId() const { return idNumber; }
}
```

在之前的代码片段中，我们定义了一个 `id` 类。`id` 将是一个可以被其他类包含`string`完全功能 `id` 能力的类。`id` 将成为任何选择包含它的整体对象的一部分。

让我们继续构建一组最终包含此 `id` 的类。我们将从一个我们熟悉的类开始，`Person`：

```cpp
class Person
{
private:
    string firstName;
    string lastName;
    char middleInitial = '\0'; // 类内初始化
    string title; // Mr., Ms., Mrs., Miss, Dr., 等。
protected:
    void ModifyTitle(const string&);
public:
    Person() = default; // 默认构造函数
    Person(const string&, const string&, char,
        const string&);
    // 我们获得无声明的默认构造函数
    // Person(const Person &) = default; // 拷贝构造函数
    // 但是，我们需要声明析构函数来添加“虚拟”
    virtual ~Person() = default; // 虚拟析构函数
    const string &GetFirstName() const
    {
        return firstName;
    }
    const string &GetLastName() const { return lastName; }
    const string &GetTitle() const { return title; }
    char GetMiddleInitial() const { return middleInitial; }
    // 虚函数
    virtual void Print() const;
```

```cpp
virtual void IsA() const;
virtual void Greeting(const string &) const;
// 假设 Person 的成员函数存在这里
// (它们与之前的章节中相同)
```

在上一段代码中，我们已经按照习惯的描述方式定义了 `Person` 类。为了简短这个示例，让我们假设伴随的成员函数已如上述类定义中的原型声明的形式存在。你可以通过之前提供的 GitHub 链接中的在线代码来引用这些成员函数。

现在，让我们来定义 `Student` 类。虽然它将包含一些我们熟悉的元素，但 `Student` 还将包含一个作为嵌入式对象的 `Id`：

```cpp
class Student : public Person // “整体”对象
private:
    float gpa = 0.0; // 类内初始化
    string currentCourse;
    static int numStudents;
    Id studentId; // 由一个“部分”组成
public:
    Student(); // 默认构造函数
    Student(const string &, float, const string &, char,
        const string &, const string &,
        const string &);
    Student(const Student &); // 拷贝构造函数
    ~Student() override; // 析构函数
    // 各种成员函数（许多是内联的）
    void EarnPhd() { ModifyTitle("Dr."); }
    float GetGpa() const { return gpa; }
    const string &GetCurrentCourse(const string &) const
        { return currentCourse; }
    void SetCurrentCourse(const string &); // 仅原型
    void Print() const override;
    void IsA() const override;

{ cout << "Student" << endl; }
static int GetNumberStudents() { return numStudents; }
// 嵌入 Id 对象的访问函数
const string &GetStudentId() const; // 仅原型
};
int Student::numStudents = 0; // 静态数据成员
inline void Student::SetCurrentCourse(const string &c)
{
    currentCourse = c;
}
```

在前面的 `Student` 类中，我们经常注意到 `Student` 派自 `Person`。正如我们所知，这意味着 `Student` 实例将包含一个作为 `Person` 子对象的 `Person` 内存布局。

然而，注意 `Student` 类定义中的数据成员 `Id studentId;`。在这里，`student` 的类型是 `Id`。它既不是指针，也不是 `Id` 的引用。数据成员 `studentId` 是一个嵌入对象（即聚合对象或成员对象）。这意味着当实例化 `Student` 类时，不仅会包含继承自类的内存，还将包含任何嵌入对象的内存。我们需要提供一种方法来初始化这个嵌入对象 `studentId`。请注意，我们之前见过成员对象，例如类型为 `string` 的成员；即类型为另一个类的数据成员。

让我们继续通过 `Student` 成员函数，以了解我们如何初始化、操作和访问嵌入对象：

```cpp
Student::Student() : studentId(to_string(numStudents + 100) + "Id")
{
    numStudents++; // 增加静态计数器
}
Student::Student(const string &fn, const string &ln,
char mi, const string &t, float avg,
const string &course, const string &id):
Person(fn, ln, mi, t), gpa(avg),
currentCourse(course), studentId(id)
{
    numStudents++;
}
Student::Student(const Student &): Person(s),
gpa(s.gpa), currentCourse(s.currentCourse),
studentId(s.studentId)
{
    numStudents++;
}
Student::~Student() // 析构函数定义
{
    numStudents--;
// 嵌入对象 student 也会被析构
}
void Student::Print() const
{
    cout << GetTitle() << " " << GetFirstName() << " ";
    cout << GetMiddleInitial() << " " << GetLastName();
    cout << " with id: " << studentId.GetId() << " " GPA: ";
    cout << setprecision(3) << " " << gpa;
    cout << " Course: " << currentCourse << endl;
}
const string &GetStudentId() const
{
    return studentId.GetId();
}
```

在之前列出的 `Student` 成员函数中，让我们从构造函数开始。注意在默认构造中，我们利用成员初始化列表 `:` 来指定 `studentId(to_string(numStudents + 100) + "Id")`。由于 `studentId` 是一个成员对象，我们有机会（通过成员初始化列表）选择使用哪个构造函数来对其进行初始化。在这里，我们仅选择了带有 `Id(const string &)` 签名的那个。在没有特定值来初始化 `Id` 的情况下，我们制造了一个字符串值作为所需的 ID。

同样，在 `Student` 的可选构造函数中，我们使用成员初始化列表指定 `studentId(id)`，这也会选择 `Id(const string &)` 构造函数，并将参数 `id` 传递给该构造函数。

`Student` 的拷贝构造函数通过成员初始化列表中的 `studentId(s.studentId)` 指定了如何初始化 `studentId` 成员对象。在这里，我们简单地调用了 `Id` 的拷贝构造函数。

在 `Student` 的析构函数中，我们不需要释放 `studentId`。由于此数据成员是一个嵌入（聚合）对象，当外部对象的内存释放时，它的内存随之消失。当然，由于 `studentId` 本身是一个对象，在释放内存之前，会先调用它自己的析构函数。

```cpp
int main ()
{
    Student s1("Cyrus", "Bond", 'I', "Mr.", 3.65, "CS101", "101");
    Student s2("Anne", "Brennan", 'M', "Ms.", 3.95, "CS102", "102");
    s1.Print();
    s2.Print();
}
```

输出:

Cyrus Bond I. with id: 101 GPA: 3.650 Course: CS101

Anne Brennan M. with id: 102 GPA: 3.950 Course: CS102

尽管如此，虽然在某些方面继承一个*部分*是简单的，但它极大地增加了多重继承的复杂度。我们知道多重继承可能会带来许多潜在的复杂性。此外，使用继承时，“整体”只能包含一个每一个*部分*——而不是包含多个同一个*部分*。

此外，当你将使用继承实现的“整体-部分”关系实现与面向对象（OO）设计进行比较时，可能会感到困惑。记住，继承通常意味着“是一个”（*Is-A*），而不是“包含有一个”（*Has-A*）。出于这些原因，通过嵌入对象来实现聚合通常是最典型且最受推崇的方法。

接下来，让我们通过观察更通用的聚合形式来继续后续。

## 定义和实现广义聚合

我们已经查看了 OO 设计中最常用的聚合形式，最著名的是组合（composition），通过组合，我们看到在没有整体的情况下，部分没有存在的理由。尽管如此，还存在一种更通用的（但不太常见）的聚合形式，它有时会在 OO 设计中被指定。现在我们来考虑这种不常见的聚合形式。

在**广义聚合**中，*部分*可以在没有*整体*的情况下存在。部分将被单独创建，然后在之后的某个时间点连接到整体上。当*整体*消失时，*部分*可能会留下来，以便回收并用于另一个外部或*整体*对象。

在广义聚合中，“包含有一个”关系显然适用，“整体-部分”的定义也是如此。区别在于，整体对象不会创建或销毁部分对象。考虑一个简单的例子：汽车“拥有”n个引擎（Engine）。汽车对象也“拥有”一组四个轮胎（Tire）对象。引擎或轮胎对象可以单独制造，然后传递给汽车的构造函数，以为整体提供这些部分。然而，如果引擎被销毁，可以很容易更换一个新引擎（使用成员函数），而无需销毁并重建整辆汽车。

广义聚合等同于“包含有一个”关系，但我们像对待组合那样，以个体部分更具灵性和永久性的角度来考虑这种关系。我们将这种关系视为聚合，仅仅是因为我们希望将对象等同于“包含有一个”的含义。在汽车、引擎和轮胎的例子中，“包含有一个”关系是强性的；引擎和轮胎是组成整个汽车的必要部分。

在这里，实现通常是整体包含指向部分（或多个部分）的指针。需要注意的是，部分将传递给外部对象的构造函数（或另一个成员函数）以建立这种关系。关键标记是，整体不会创建（或销毁）部分，而部分永远不会销毁整体。

顺便提一下，各个部件的寿命（以及基本的实现）——关联（association）。让我们进入下一节，以理解广义聚合与关联之间的相似性，以及它们在 OO 概念上的差异（有时是微妙的）。

## 理解关联

关联模拟了存在于互不相关的类之间的关系。关联可以为对象提供交互方式以满足这些关系。然而，关联并不用于“包含有一个”关系，在某些情况下，对于我们描述的是否真正的“包含有一个”关系，还是仅仅因为该短语在语言上听起来恰当而使用它，存在灰色地带。

关联存在多重性（Multiplicity）：有一对一、一对多、多对一和多对多。例如，一个学生（Student）可能与一个大学（University）关联，而该所大学可能与多个学生实例关联；这是一个一对多的关联。

被关联的对象具有独立的存在性。也就是说，两个或多个对象可以在应用程序的某一部分时间内被实例化并独立存在。在某个点，一个对象可能希望与另一个对象断言依赖或关系。在应用程序的后期，被关联的对象可能会分开并继续它们各自不相关的路径。

例如，考虑课程（Course）和讲师（Instructor）之间的关系。一门课程与一名老师关联。一门课程需要一名老师；老师对于课程是不可或缺的。老师可能与多门课程关联。然而每个部分都是独立存在的——一个不会创建或销毁另一个。老师也可以在没有课程的情况下独立存在；也许一个老师正在花时间写书、正在休假，或者是一个正在进行研究的教授。

在这个例子中，关联与广义聚合非常相似。在两种情况下，相关对象都独立存在。在这种情况下，是说课程“拥有”n个讲师，还是说课程对讲师有依赖关系，这可能存在灰色地带。你可能会问——这仅仅是“包含有一个”的关系吗？无论如何，广义聚合可以被视为关联的特化类型；我们将看到它们的实现是相同的。无论实现如何，当主对象消失时，它不会干涉（即删除）被关联的对象。

例如，考虑大学和老师之间的关系。与其将其想为“包含有一个”关系，我们可能认为认为两者之间的关系是关联；同样，大学与许多学生对象建立了关系。区别在于，大学是由部门（Department）对象、建筑（Building）对象等通过“包含有一个”关系构成的，但它与老师对象、学生对象的关系是使用关联的。

现在我们已经区分了典型的关联和广义聚合，让我们来看看如何实现关联以及其中涉及的一些复杂性。

## 实现关联

通常，两个或多个对象之间的关联是使用指针或指针集来实现的。“一”的一侧使用指向被关联对象的指针实现，而关系的“多”的一侧实现为指向被关联对象的指针集。指针集可以是指针数组、指针链表，或真正的任何指针集合。每种集合类型都有其自己的优缺点。例如，指针数组易于使用，可以直接访问特定成员，但数量是固定的。指针链表可以容纳任何数量的元素，但访问特定元素需要遍历其他元素以找到所需的项。

偶尔，可以使用引用（reference）来实现关联的某一侧。记住，引用必须初始化，且不能在之后重置为另一个对象。使用引用来建模关联意味着，在一个主对象的生存期间，一个实例将与另一个精确的实例关联。这具有极强的限制性，因此极少使用引用来实现关联。

无论实现如何，当主对象消失时，它不会干涉（即删除）被关联的对象。

让我们来看一个典型的例子，说明一对多关联的首优实现方式，在“一”的一侧使用指针，在“多”的一侧使用指针集。在这个例子中，一所大学将与多个学生实例关联。为了简单起见，一个学生将与一所大学关联。

为了节省空间，本程序中与我们上一个示例相同的部分将不再显示；然而，完整的程序可以在我们的 GitHub 上找到，如下：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter10/Chp10-Ex2.cpp

```cpp
#include <iostream>
#include <iomanip>
using std::cout;
using std::endl;
using std::setprecision;
using std::string;
using std::to_string;
// 为了节省空间，这里省略 Id 和 Person 类
// 它们将之前的示例所示：Chp10-Ex1.cpp
class Student; // 前向声明
class University {
private:
    string name;
    static constexpr int MAX = 25; // 允许的最大学生人数
    // 注意：每个 studentBody 元素都被设置为 nullptr
    // 使用类内初始化
    Student *studentBody[MAX] = {}; // 与多个
    // 学生关联
    int currentNumStudents = 0; // 类内初始化
public:
    University();
    University(const string &);
    University(const University &) = delete; // 禁止拷贝
    ~University();
    void EnrollStudent(Student *);
    const string &GetName() const { return name; }
    void PrintStudents() const;
};
```

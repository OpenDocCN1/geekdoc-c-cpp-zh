
在上述的类定义中，我们首先注意到一个简单的接口类 `Charitable`，它是通过一个受限制的抽象类实现的。我们没有包含任何数据成员，并使用一个纯虚函数 `virtual Give(float) = 0` 来定义接口类。我们还包含了一个虚析构函数。

接下来，`Person` 通过公有继承派生自 `Charitable`，以实现 `Charitable` 接口。我们简单地重写了 `virtual Give(float)` 来为捐赠提供默认定义。我们从 `Person` 派生出 `Student`；注意 `Student` 是一个 `Person`，并且混合了（或实现了）`Charitable` 接口。在我们的 `Student` 类中，我们选择重新定义 `virtual Give(float)`，为 `Student` 实例提供一个更合适的 `Give()` 定义。也许学生的财务有限，选择捐出等同于预定货币金额的时间。

在这里，我们使用了 C++ 中的抽象类来建模面向对象（OO）的接口类概念。

让我们继续讨论关于抽象类的整体讨论，通过检查派生类对象如何被抽象类类型收集来探讨。

## 将派生类对象泛化为抽象类型

我们在第 7 章《通过多态利用动态绑定》中已经看到，有时将相关的派生类实例分组并在使用基类指针存储的集合中是合理的。这样做允许使用基类指定的多态操作，对相关的派生类类型进行统一处理。我们还知道，当调用多态基类操作时，得助于 C++ 中实现多态的虚函数和内部虚函数表（v-table），程序将在运行时调用正确的派生类方法。

然而，你可能会思考，是否可以通过一个作为抽象类的基类来收集一组相关的派生类类型。记住，抽象类是不可实例化的，那么我们如何将一个派生类对象存储为无法实例化的对象呢？解决方案是使用指针（甚至是引用）。虽然我们不能在抽象基类实例的集合中收集派生类实例（那些是不可实例化的），但我们可以在抽象类类型指针的集合中收集派生类实例。我们也可以拥有抽象类的引用来指向派生类实例。自从我们学习多态以来，我们一直在进行这种类型的分组（使用基类指针）。

专门化对象的泛化组使用了隐式的**向上转换（upcasting）**。取消向上转换必须使用显式的**向下转换（downcast）**完成，并且程序员需要正确转换到之前泛化的派生类型。对错误的类型进行不正确的向下转换会导致运行时错误。

什么时候有必要通过基类类型（包括抽象基类类型）收集派生类对象呢？答案是，当在你的应用程序中以一种更通用的方式处理相关的派生类是有意义的时，也就是说，当你想要利用的基类类型中指定的操作时。不可否认，你可能会发现许多同样的情况，将派生类实例保留在它们自己的类型中（以利用在派生类级别引入的专门化操作）是合理的。现在你理解什么是可能的。

让我们通过查看一个展示抽象类运行的综合示例来继续讨论。

## 整合所有部分

到本章为止，我们已经理解了抽象类的细微之处，包括纯虚函数，以及如何使用抽象类和纯虚函数创建接口类。看到我们的代码在运行，以及它所有各种组件及其各种细微差别，始终是非常重要的。

让我们来看一个更复杂的、完整的程序示例，以充分说明 C++ 中使用纯虚函数实现的抽象类。在这个示例中，我们不再进一步将抽象类指定为接口类，但我们将利用此机会，使用其抽象基类类型指针的集合来收集相关的派生类类型。此示例将拆分为许多部分；完整程序可以在以下 GitHub 路径找到：

`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter08/Chp8-Ex1.cpp`

```cpp
#include <iostream>
#include <iomanip>
using std::cout;
using std::endl;
using std::setprecision;
using std::string;
using std::to_string;
constexpr int MAX = 5;
class LifeForm
{
private:
    int lifeExpectancy = 0;
public:
    LifeForm() = default;
    LifeForm(int life): lifeExpectancy(life) {}
    LifeForm(const LifeForm&) = default;
    virtual ~LifeForm() = default;
    [[nodiscard]] int getLifeExpectancy() const
        { return lifeExpectancy; }
    virtual void Print() const = 0;
    virtual string IsA() const = 0;
    virtual string Speak() const = 0;
```

在上述类定义中，我们注意到 `LifeForm` 是一个抽象类。它是一个抽象类是因为它包含至少一个虚函数定义。事实上，它包含了包含了纯虚函数，即 `Print()`、`IsA()` 和 `Speak()`。

现在，让我们用一个具体的派生类 `Cat` 来扩展 `Lifeform`：

```cpp
class Cat: public LifeForm
{
private:
    int numberLivesLeft = 9;
    string name;
    static constexpr int CAT_LIFE = 15;
public:
    Cat(): LifeForm(CAT_LIFE) {}
    Cat(int lives): LifeForm(CAT_LIFE), numberLivesLeft(lives) {}
    Cat(const string &)
        ~Cat() override = default;
    const string &GetName() const { return name; }
    int GetNumberLeft() const
        { return numberLivesLeft; }
    void Print() const override;
    string IsA() const override { return "Cat"; }
    string Speak() const override { return "Meow!"; }
};
Cat::Cat(const string &n) : LifeForm(CAT_LIFE), name(n)
{
}
void Cat::Print() const {
    cout << "\t" << name << "has" << numberLivesLeft;
    cout << " lives left" << endl;
}
```

在之前的代码段中，我们看到了 `Cat` 的类定义。注意 `Cat` 重写了 `LifeForm` 的纯虚函数 `Print()`、`IsA()` 和 `Speak()`，通过在 `Cat` 类中为这些函数提供定义。在这些函数有了实现后，`Cat` 的任何派生类都可以选择性地重写这些函数以提供更合适的版本（但它们不再义务这样做）。

注意，如果 `Cat` 未能重写 `LifeForm` 的任何一个纯虚函数，那么 `Cat` 也将被认为是一个抽象类，因此是不可实例。

提醒一下，尽管虚函数 `IsA()` 和 `Speak()` 是为了简化代码而写内联的，但虚函数几乎不会被编译器内联（除非涉及编译器去虚化、final 方法或实例的动态类型所需的少数情况）。

现在，让我们继续查看 `Person` 的类定义及其内联函数：

```cpp
class Person: public LifeForm
{
private:
    string firstName;
    string lastName;
    char middleInitial = '\0';
    string title;
    static constexpr PERSON_LIFE = 80;
protected:
    void ModifyTitle(const string &);
public:
    Person();
    Person(const string &, const string &, char, const string &);
    Person(const Person &) = default;
    ~Person() override = default;
    const string &GetFirstName() const { return firstName; }
    const string &GetLastName() const { return lastName; }
    const string &GetTitle() const { return title; }
    char GetMiddleInitial() const { return middleInitial; }
    void Print() const override;
    string IsA() const override;
    string Speak() const override;
}
```

注意 `Person` 使用公有继承扩展了 `LifeForm`。在之前的章节中，`Person` 是继承层次结构顶顶的基类。现在 `Person` 重定义了来自 `LifeForm` 的纯虚函数，分别命名为 `Print()`、`IsA()` 和 `Speak()`。因此，`Person` 现在是一个具体类，可以被实例化。

现在，让我们复习 `Person` 的成员函数定义：

```cpp
Person::Person(): LifeForm(PERSON_LIFE)
{}
Person::Person(const string &fn, const string &ln, const string &t): LifeForm(PERSON_LIFE), firstName(fn), lastName(ln), middleInitial(mi), title(t)
{
}
Person::Person(const Person &p): LifeForm(p)
{
    firstName(p.firstName), lastName(p.lastName), middleInitial(p.middleInitial), title(p.title)
}
void Person::ModifyTitle(const string &newTitle)
{
    title = newTitle;
}
void Person::Print() const
{
    cout << "\t" << title << " " << firstName << " " ";
    cout << middleInitial << " " << lastName << endl;
}
string Person::IsA() const
{
    return "Person";
}
string Person::Speak() const
{
    return "Hello!";
}
```

在 `Person` 成员函数中，注意我们为 `Print()`、`IsA()` 和 `Speak()` 提供了实现。此外，注意在两个 `Person` 构造函数中，我们在成员初始化列表中选择了 `: LifeForm(PERSON_LIFE)` 来调用 `LifeForm(int)` 构造函数。此调用将给定 `Person` 实例的 `LifeForm` 子对象中的私有继承数据成员 `LifeExpectancy` 设置为 80 (`PERSON_LIFE`)。

接下来，让我们复习 `Student` 类定义及其内联函数定义：

```cpp
class Student: public Person
{
private:
    float gpa = 0.0;
    string currentCourse;
    const string studentId;
    static int numStudents;
public:
    Student();
    Student(const string &, const string &, char, const string &, float, const string &, const string &);
    Student(const Student &);
    ~Student() override;
    void EarnPhD();
    float GetGpa() const { return gpa; }
    const string &GetCurrentCourse() const { return currentCourse; }
    const string &GetStudentId() const { return studentId; }
    void SetCurrentCourse(const string &);
    void Print() const final override;
    string IsA() const override;
    static int GetNumStudents();
};
int Student::numStudents = 0;
inline void Student::SetCurrentCourse(const string &c)
{
    currentCourse = c;
}
inline int Student::GetNumberStudents()
{
    return numStudents;
}
```

上述 `student` 类定义与我们过去看到的非常相似。`Student` 使用公有继承扩展了 `Person`，因为 `Student` 是一个 `Person`（Is-A）。

接下来，我们将回顾非内联的 `Student` 类成员函数：

```cpp
Student::Student() : studentId(to_string(numStudents + 100) + "Id") {
    numStudents++;
}
Student::Student(const string &fn, const string &ln, char mi, const string &t, float avg, const string &course, const string &id) : Person(fn, ln, mi, t), studentId(id), gpa(avg), currentCourse(course)
{
}
Student::Student(const Student &s) : Person(s), studentId(s.studentId), gpa(s.gpa), currentCourse(s.currentCourse)
{}
Student::~Student()
{
}
void Student::EarnPhD()
{
}
void Student::Print() const final
{
    cout << "\t" << title << " " << firstName << " " ";
```

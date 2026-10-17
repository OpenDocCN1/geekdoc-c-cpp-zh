
```cpp
#include <list> // partial list of #includes

#include <iterator>

using std::cout; // preferred to: using namespace std;

using std::endl;

using std::setprecision;

using std::string;

using std::to_string;

using std::list;

constexpr MAXCOURSES = 5, MAXSTUDENTS = 5;

// 状态简单枚举；我们也可以建立状态层级，但让我们保持简单

enum State { Initial = 0, Success = 1, Failure = 2 };

// 为了后续代码的可读性定义的特定状态

enum StudentState { AddSuccess = State::Success,

AddFailure = State::Failure };

enum CourseState { OpenEnrollment = State::Success,

SpaceAvailable = State::Success,

Full = State::Failure };

class Subject; // 前置

class Student;

class Observer // Observer 是一个抽象类
{
private:
  // 将状态表示为 int，以消除特定状态与基础状态之间的
  // 类型转换
  int observerState = State::Initial; // 类内初始化
protected:
  Observer() = default;
  Observer(int s) : observerState(s) { }
  void SetState(int s) { observerState = s; }
public:
  int GetState() const { return observerState; }
  virtual ~Observer() = default;
  virtual void Update() = 0;
}
```

在上一个类定义中，我们引入了一个抽象的 `Observer` 类。在这里，我们包含了一个 `observerState` 和受保护的构造函数来初始化此状态。我们包含了一个受保护的 `SetState()` 方法，以便从派生类的范围内更新此状态。我们还包含了一个公共的 `GetState()` 方法。`GetState()` 的添加将方便我们在 `Subject` 的 `Notify()` 方法中实现，因为它允许我们轻松地检查观察者的状态是否发生了变化。尽管在历史上，状态信息一直添加到 `Observer` 和 `Subject` 的派生类中，但我们将在这些基类中对状态信息进行泛化。这将允许我们的派生类保持更强的模式无关性，专注于应用程序的本质。

注意我们的析构函数是虚的，并且我们引入了一个抽象方法 `void Update() = 0;`，用于指定 `Subject` 在其观察者列表上调用的接口，以便将更新委托给这些 `Observer` 实例。

现在，让我们来看看 `Subject` 基类：

```cpp
class Subject // 被视为抽象类，由于
{
  // 受保护的构造函数。然而，由于
private:
  // 没有纯虚函数
  list<class Observer *> observers;
  int numObservers = 0;
  // 将状态表示为 int，以消除
  // 特定状态与基础状态之间的类型转换
  int subjectState = State::Initial;
  list<Observer *>::iterator newIter;
protected:
  Subject() = default;
  Subject(int s) : subjectState(s) { } // 注意类内
  // 初始化。
  void SetState(int s) { subjectState = s; }
public:
  int GetState() const { return subjectState; }
  int GetNumObservers() const { return numObservers; }
  virtual ~Subject() = default;
  virtual void Register(Observer *);
  virtual void Release(Observer *);
  virtual void Notify();
}
```

在上述 `Subject` 类定义中，我们看到 `Subject` 包含一个 STL `list` 来收集其 `Observer` 实例。它还包含 `subjectState` 和一个反映观察者数量计数计数。此外，我们包含了一个数据成员来跟踪未损坏的迭代器。我们将发现，这在删除元素时非常有用（`list::erase()` 是一个会使当前迭代器失效的操作）。

我们的 `Subject` 类也将具有受保护的构造函数和 `SetState()` 方法，用于初始化或设置主题的状态。尽管该类在技术上不是抽象的（它不包含虚函数），但它的构造函数是受保护的，以模拟抽象类；该类旨在作为派生类实例中的子对象被构造。

在公共接口中，我们有一个虚析构函数以及用于 `Register()`、`Release()` 和 `Notify()` 的虚函数。让我们看看 `Subject` 基类中这三个方法的实现：

```cpp
void Subject::Register(Observer *ob)
{
  observers.push_back(ob); // 将观察者添加到列表
  numObservers++;
}

void Subject::Release(Observer *ob)
{
  bool found = false;
  // 遍历列表直到找到观察者
  for (auto it = observers.begin(); it != observers.end(); ++it) {
    if (*it == ob) {
      // erase() 返回指向下一个元素的迭代器
      newIter = observers.erase(it);
      found = true;
      numObservers--;
      break;
    }
  }
}

void Subject::Notify()
{
  // 更新列表中的所有观察者
  for (auto it = observers.begin(); it != observers.end(); ++it) {
    (*it)->Update();
  }
}
```

为了继续推进这个示例，让我们看看派自 `Subject` 或 `Observer` 的具体类。让我们从派自 `Subject` 的 `Course` 开始：

```cpp
class Course: public Subject
{  // 继承了 Observer 列表；
  // Observer 代表候补名单上的学生
private:
  string title;
  int number = 0; // 课程数量，总学生数
  int totalStudents = 0; // 使用类内初始化
  Student *students[MAXSTUDENTS] = { }; // 初始化为
  // nullptr
public:
  Course(const string title, int num) : number(num)
  {
    this->title = title; // 或者重命名参数
  }
};
```

```cpp
// 析构函数体显示为占位符以便添加更多
// 必要的工作
~Course() override
{
    /* 这里还需要添加更多工作！ */
    int GetCourseNumber() const { return number; }
    const string &GetTitle() const { return title; }
    AddStudent(Student *);
}

void Open()
{
    SetState(Course::OpenForEnrollment);
    Notify();
}

void PrintStudents() const;
bool Course::AddStudent(Student *s)
{
    // 也应该检查学生是否已添加到课程
    if (totalStudents < MAXSTUDENTS) // 课程未满
    {
        students[totalStudents++] = s;
        return true;
    }
    else return false;
}

void Course::operator<<(ostream &os, "Course: (" << GetTitle() << 
")") has the following students: ") << endl;
for (int i = 0; i < totalStudents; i++)
{
    if (students[i] != nullptr)
    {
        os << "\t" << students[i]->GetFirstName() << " ";
        os << students[i]->GetLastName() << endl;
    }
}
```

在我们上述的类中，包含了课程标题、编号的数据成员，以及当前就读学生的总数。我们还有一份当前就读的学生列表，由 `Student *students[MAXNUMBERSTUDENTS];` 表示。此外，请记住，我们从基类 `Subject` 继承了 STL 观察者列表。这个 `Observer` 实例列表将代表组成我们课程候补名单（学生）的 `Student` 实例。

该类还包含一个构造函数、一个虚析构函数和简单的访问函数。注意，虚析构函数要做的工作比显示的要多——如果一个 `Course` 被析构，我们必须先从 `Course` 中移除（但不删除）`Student` 实例。我们的 `Course::AddStudent(Student *)` 接口将允许我们将学生添加到课程中。当然，我们应该在该方法的体体中确保该学生没有添加过该课程。

我们的 `void Course::Open()` 方法将在 `Course` 对象上调用，以指示该课程现在可以添加学生了。在这里，我们首先将状态设置为 `Course::OpenForEnrollment`（使用枚举类型明确地表示开放报名），然后调用 `Notify()`。基类 `Subject` 中的 `Notify()` 方法会遍历每个 `Observer`。每个 `Observer` 都是一个 `Student`；`Student::Update()` 将允许候补名单上的每个学生添加现在已开放接收学生的课程。在成功添加到课程的当前学生列表后，`Student` 将请求 `Release()` 它在候补名单中（作为观察 `Observer`）的位置。

接下来，让我们看看 `Student` 类的定义，它是派生自 `Person` 和 `Observer` 的具体类：

```cpp
class Person { }; // 假设这里是我们典型的 Person 类
class Student: public Person, public Observer
{
private:
    float gpa = 0.0; // 类内初始化
    const string studentId;
    int currentNumCourses = 0;
    Course *courses[MAXCOURSES] = { }; // 设置为 nullptr
    // 我们想选的课程 - 我们在候补名单上。
    Course *waitListedCourse = nullptr; // 我们的 Subject
    // (特化部分)
    static int numStudents;
public:
    Student(); // 默认构造函数
    Student(const string &, const string &, char,
        const string &, float, const string &, Course);
    Student(const string &, const string &, char,
        const string &, float, const string &);
    Student(const Student&) = delete; // 禁止拷贝
    ~Student() override; // 虚析构函数
    void EarnPhD();
    float GetGpa() const { return gpa; }
    const string &GetStudentId() const { return studentId; }
    void Print() override; // 来自 Person
    void IsA() override; // 来自 Person
    void Update() override; // 来自 Observer
    virtual void Graduate(); // 新引入的虚函数
    bool AddCourse(Course *);
    void PrintCourses();
    static int GetNumberStudents() { return numStudents; };
}
```

简要回顾上述的 `Student` 类定义，我们可以看到该类通过多重继承派生自 `Person` 和 `Observer`。假设我们的 `Person` 类正如过去多次使用的那样。

除了 `Student` 常规组件外，我们添加了数据成员 `Course *waitListedCourse`，它将建模与我们 `Subject` 的关联。此数据成员将建模一个我们非常想添加但目前无法添加的课程，即候补名单中的课程。在这里，我们实现了单个候补课程的概念，但我们可以轻松地扩展示例以包含一个支持多个候补课程的列表。注意，此链接（数据成员）是以派生类型 `Course` 的形式声明的，而不是基类型 `Subject`。这是观察者模式中的典型做法，并将帮助我们在于 `Student` 中重写 `Update()` 方法时避免可怕的类型强制转换。正是通过这个链接，我们将与 `Subject` 进行交互，并作为我们在 `Subject` 状态发生变化时接收其更新的手段。

我们还注意到在 `Student` 中声明了 `virtual void Update() override;`。该方法将允许我们重写 `Observer` 指定的纯虚 `Update()` 方法。

接下来，让我们回顾 `Student` 的一些新成员函数：

```cpp
// 假设大多数 Student 成员函数如常
// 看看新添加的：
Student(const string &fn, const string &id, char,
const string &avg, float, const string &mi, Course *c)
    : Person(fn), Observer(this), gpa(avg), studentId(id),
    currentNumCourses(0), waitListedCourse(c)
{
    // 在此构造函数中，假设我们按常设置了大部分
    // 数据成员。这里关键的额外行
    // 是 waitListedCourse = c; 用于将我们的候补
    // 条目指向 Subject，以及 c->Register(this)；
    // 我们将学生 (Observer) 添加到 Subject 的
    // 列表（最终列表）。
    waitListedCourse = c;
    c->Register(this);
    // is(Subject)
    numStudents++;
}

bool Student::AddCourse(Course *c)
{
    // 也应该检查学生是否课程中
    if (currentNumCourses < MAXCOURSES)
    {
        courses[currentNumCourses++] = c; // 设置关联
        c->AddStudent(this); // 成功
        return true;
    }
    else // 如果我们无法添加课程
    {
        c->Register(this); // 将学生 (Observer)
        // 添加到 Subject
        return false;
    }
}
```

```cpp
void Student::Update()
{
 // 课程状态更改为“Open For Enrollment' 等
    // 所以我们现在可以添加了。
    if (waitListedCourse->GetState() ==
        CourseState::OpenForEnrollment ||
        waitListedCourse->GetState() ==
        CourseState::NewSpaceAvailable)
    {
```

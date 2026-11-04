
因此你可以这样写之前的示例：

```csharp
public class Student
{
    public string firstName;
    public string lastName;
    public void SetName(string firstName, string lastName)
    {
        // Explicitly reference the "current object" referenced by this.
        this.SetFirstName(firstName);
        this.SetLastName(lastName);
    }
    public void SetFirstName(string name)
    {
        this.firstName = name;
    }
    public void SetLastName(string name)
    {
        this.lastName = name;
    }
}
```

注意关键字 this 的显式添加。将它添加到成员引用中不会增加任何内容，因为 this 是默认的。然而，当 Main() 进行以下调用时，this 在 SetName() 及其可能调用的任何其他方法中都引用 student1：

第二卷  
第四章  
让我说说这个  
关于 This

```csharp
student1.SetName("John", "Smith");
```

### this 何时显式？

你通常不需要显式引用 this，因为编译器在必要时会理解它。然而，有两种常见情况需要 this。你可能在初始化数据成员时需要它，如本示例所示：

```csharp
class Person
{
    public string name;     // This is this.name below.
    public int id;          // And this is this.id below.
    public void Init(string name, int id)   // These are method arguments.
    {
        this.name = name;   // Argument names same as data member names
        this.id = id;
    }
}
```

Init() 方法的参数名为 name 和 id，与对应的数据成员名称相同。这样方法就很容易阅读，因为你立刻知道哪个参数存储在哪里。唯一的问题是参数列表中的名称 name 掩盖了数据成员的名称。编译器会对此提出抱怨。

添加 this 可以明确指出所指的名称。在 Init() 中，名称 name 指的是方法参数，但 this.name 指的是数据成员。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_281_0.png)

你也在存储当前对象以供以后使用或由其他方法使用时需要 this。考虑这个程序示例 ReferencingThisExplicitly：

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_281_1.png)

~~~csharp
// ReferencingThisExplicitly -- Demonstrates how to explicitly use
//   the reference to 'this'.
using System;
namespace ReferencingThisExplicitly
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Create a student.
            Student student = new Student();
            student.Init("Stephen Davis", 1234);
            // Now enroll the student in a course.
            Console.WriteLine
                ("Enrolling Stephen Davis in Biology 101");
            student.Enroll("Biology 101");
            // Display student course.
            Console.WriteLine("Resulting student record:");
            student.DisplayCourse();
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }

    // Student -- The class for university students.
    public class Student
    {
        // All students have a name and an id.
        public string _name;
        public int _id;
        // The course in which the student is enrolled
        CourseInstance _courseInstance;
        // Init -- Initialize the student object.
        public void Init(string name, int id)
        {
            this._name = name;
            this._id = id;
            _courseInstance = null;
        }
        // Enroll -- Enroll the current student in a course.
        public void Enroll(string courseID)
        {
            _courseInstance = new CourseInstance();
            _courseInstance.Init(this, courseID);   // Here's the explicit reference.
        }
        // Display the name of the student and the course.
        public void DisplayCourse()
        {
        Console.WriteLine(_name);
        _courseInstance.Display();
    }
}
// CourseInstance -- A combination of a student with
//   a university course.
public class CourseInstance
{
    public Student _student;
    public string _courseID;
    // Init -- Tie the student to the course.
    public void Init(Student student, string courseID)
    {
        this._student = student;
        this._courseID = courseID;
    }
    // Display -- Output the name of the course.
    public void Display()
    {
        Console.WriteLine(_courseID);
    }
}
~~~

这个程序相当平凡。Student 对象有空间存放姓名、ID 以及一门大学课程的单个实例（不是一个勤奋的学生）。Main() 创建学生实例然后调用 Init() 来初始化该实例。此时，_courseInstance 引用被设为 null，因为学生尚未注册课程。

Enroll() 方法通过用新对象初始化 _courseInstance 来注册学生。然而，CourseInstance.Init() 方法的第一个参数是 Student 实例，第二个参数是课程 ID。你应该传递哪个 Student？显然，你需要传递当前 Student —— 由 this 引用的 Student。（因此你可以说 Enroll() 将 this 学生注册到 CourseInstance。）

一些程序员（包括我）喜欢通过在每个数据成员名称前加上下划线来更清晰地区分数据成员和其他变量，像这样：_name。你会看到我大多数时候都采用这种约定，但当然这只是一种约定，你可以随意处理。如果你使用这种约定，就不需要用 this 前缀该项，如 this._id。仅凭下划线前缀就完全没有歧义。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_282_0.png)

### 当你没有 this 会发生什么？

混合类（static）方法和实例（nonstatic）方法就像混合牧羊人和牧场主。幸运的是，C# 为两者之间的这些问题提供了一些解决办法。要了解问题，请考虑这个程序片段 MixingStaticAndInstanceMethods：

第二卷

第四章

让我说说这个关于 This

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_283_0.png)

```
// MixingStaticAndInstanceMethods -- Mixing class (static) methods
// and instance (nonstatic) methods can cause problems.
using System;
namespace MixingStaticAndInstanceMethods
{
public class Student
{
public string _firstName;
public string _lastName;
// InitStudent -- Initialize the student object.
public void InitStudent(string firstName, string lastName)
{
_firstName = firstName;
_lastName = lastName;
}
// OutputBanner (static) -- Output the introduction.
public static void OutputBanner()
{
Console.WriteLine("Aren't we clever!");
// Console.WriteLine(? what student do we use ?); * The problem!
}
// OutputBannerAndName (nonstatic) -- Output intro.
public void OutputBannerAndName()
{
// The class Student is implied but no this
// object is passed to the static method.
OutputBanner();
// The current Student object is passed explicitly.
OutputName(this);
}
// OutputName -- Output the student's name.
public static void OutputName(Student student)
{
// Here, the Student object is referenced explicitly.
Console.WriteLine("Student's name is {0}", student.ToNameString());
}
// ToNameString -- Fetch the student's name.
public string ToNameString()
{
// Here, the current object is implicit --
// this could have been written:
// return this._firstName + " " + this._lastName;
return _firstName + " " + _lastName;
}
}
public class Program
{
public static void Main(string[] args)
{
Student student = new Student();
student.InitStudent("Madeleine", "Cather");
// Output the banner and name statically.
Student.OutputBanner();
Student.OutputName(student);
Console.WriteLine();
}
// Output the banner and name again using instance.
student.OutputBannerAndName();
// Wait for user to acknowledge.
Console.WriteLine("Press Enter to terminate...");
Console.Read();
}
}
```

从程序底部的 Main() 开始，这样你能更好地看到问题。程序首先创建一个 Student 对象并初始化其姓名。单例程序现在只想做的事情不外乎输出姓名并在其前面加上简短的消息和横幅。

Main() 首先使用类或 static 方法方法输出横幅和消息。程序调用 OutputBanner() 方法输出横幅行，并调用 OutputName() 方法输出消息和学生姓名。OutputBanner() 方法向控制台输出一条简单消息。Main() 将 student 对象作为参数传递给 OutputName()，以便它可以显示学生的姓名。

接下来，Main() 通过调用 student.OutputBannerAndName() 使用实例方法方法输出横幅和消息。

OutputBannerAndName() 首先调用 static 方法 OutputBanner()。类 Student 被假定。没有对象被传递，因为 static 的 OutputBanner 不需要一个。接下来，OutputBannerAndName() 调用 OutputName() 方法。OutputName() 也是一个 static 方法，但它接受一个 Student 对象作为参数。OutputBannerAndName() 为该参数传递 this。

一个更有趣的案例是 OutputName() 内部对 ToNameString() 的调用。OutputName() 被声明为 static，因此没有 this。它有一个显式的 Student 对象，用它来发起调用。

OutputBanner() 方法也可能想调用 ToNameString()；然而，它没有可用的 Student 对象。因为它是一个 static 方法并且没有显式传递对象，所以它没有 this 引用。注意示例代码中的第一行粗体字：static 方法不能调用实例方法。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_284_0.png)

> **REMEMBER**
> 一个 static 方法不能在没有显式提供对象的情况下调用非 static 方法。没有对象，就没有调用。一般来说，static 方法不能访问类中的任何非 static 项。但非 static（实例）方法可以访问 static 以及实例项：static 数据成员和 static 方法。


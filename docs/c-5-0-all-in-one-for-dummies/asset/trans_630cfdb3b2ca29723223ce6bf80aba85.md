
![](img/80ff26f06fc9ab951e1cd4257b867366_277_0.png)

// ReferencingThisExplicitly -- Demonstrates how to explicitly use
// the reference to 'this'.
// using System;
namespace ReferencingThisExplicitly
{
    public class Program
    {
        public static void Main(string[] strings)
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
    // a university course.
    public class CourseInstance
    {
        public Student _student;
        public string _courseID;
        // Init -- Tie the student to the course.
        public void Init(Student student, string courseID)
        {
            this._student = student;
~~~csharp
        this._courseID = courseID;
    }
    // Display -- Output the name of the course.
    public void Display()
    {
        Console.WriteLine(_courseID);
    }
}
~~~

这个程序相当平凡。`Student` 对象有空间存放姓名、ID 以及一门大学课程的单个实例（不是一个勤奋的学生）。`Main()` 创建学生实例，然后调用 `Init()` 来初始化该实例。此时，`_courseInstance` 引用被设为 null，因为学生尚未注册课程。

`Enroll()` 方法通过用新对象初始化 `_courseInstance` 来注册学生。然而，`CourseInstance.Init()` 方法以 `Student` 实例作为第一个参数，课程 ID 作为第二个参数。你应该传递哪个 `Student`？显然，你需要传递当前的 `Student` —— 由 *this* 引用的 `Student`。（因此你可以说 `Enroll()` 将 *this* 学生注册到 `CourseInstance` 中。）

> > 第二部
> > 第四章
> >
> > 让我谈谈这个 This

![](img/80ff26f06fc9ab951e1cd4257b867366_278_0.png)

一些程序员（包括我）喜欢通过在每个数据成员的名称前加下划线来更清晰地区分数据成员和其他变量，像这样：`_name`。你会看到我大多数时候都采用这种约定，但当然，这只是一种约定，你可以随意处理。如果你使用这种约定，就不需要用 *this* 来前缀该项，如 `this._id`。仅凭下划线前缀就完全没有歧义。

### 当没有 *this* 时会发生什么？

混合类（静态）方法和实例（非静态）方法就像混合牧羊人和牧场主一样。幸运的是，C# 为两者之间的这些问题提供了一些解决办法。要了解这个问题，请考虑这个程序片段 `MixingStaticAndInstanceMethods`：

![](img/80ff26f06fc9ab951e1cd4257b867366_278_1.png)

~~~csharp
// MixingStaticAndInstanceMethods -- Mixing class (static) methods
//   and instance (nonstatic) methods can cause problems.
using System;
namespace MixingStaticAndInstanceMethods
{
    public class Student
    {
        public string _firstName;
        public string _lastName;
        // Init -- Initialize the student object.
        public void InitStudent(string firstName, string lastName)
        {
            _firstName = firstName;
            _lastName = lastName;
        }
    }
}
~~~

```csharp
// OutputBanner (static) -- Output the introduction.
public static void OutputBanner()
{
    Console.WriteLine("Aren't we clever:");
    // Console.WriteLine(" what student do we use ?"); // The problem!
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
        // Output the banner and name again using instance.
        student.OutputBannerAndName();
        // Wait for user to acknowledge.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

从程序底部开始，从 Main() 开始，这样你就能更好地看到问题。程序首先创建 Student 对象并初始化其姓名。这个单例程序现在只想做一件事：输出前面加上简短消息和横幅的姓名。

Main() 首先使用类或静态方法的方式输出横幅和消息。程序调用 OutputBanner() 方法输出横幅行，并调用 OutputName() 方法输出消息和学生姓名。OutputBanner() 方法向控制台输出一条简单的

消息。Main() 将学生对象作为参数传递给 OutputName()，以便它可以显示学生的姓名。

接下来，Main() 通过调用 student.OutputBannerAndName() 使用实例方法的方式输出横幅和消息。

OutputBannerAndName() 首先调用静态方法 OutputBanner()。类 Student 被假定。没有对象被传递，因为静态 OutputBanner 不需要一个。接下来，OutputBannerAndName() 调用 OutputName() 方法。OutputName() 也是一个静态方法，但它接受一个 Student 对象作为参数。OutputBannerAndName() 将 this 作为该参数传递。

第二部
第四章

让我谈谈这个 This

一个更有趣的例子是 OutputName() 内部对 ToNameString() 的调用。OutputName() 被声明为静态，因此没有 this。它有一个显式的 Student 对象，用它来发起调用。

OutputBanner() 方法可能也想调用 ToNameString()；然而，它没有可用的 Student 对象。它没有 this 引用，因为它是一个静态方法，并且没有显式传递对象。请注意示例代码中第一条加粗的行：静态方法不能调用实例方法。

![](img/80ff26f06fc9ab951e1cd4257b867366_280_0.png)

静态方法如果没有显式提供对象，就不能调用非静态方法。没有对象，就不能调用。一般来说，静态方法不能访问类中的任何非静态项。但非静态（实例）方法可以访问静态项以及实例项：静态数据成员和静态方法。

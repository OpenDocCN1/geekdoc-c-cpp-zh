
        if (AddCourse(waitListedCourse)) // 添加

        {

            cout << GetFirstName() << " " << GetLastName();

            cout << " 从候补名单中移除并加入 "

            cout << waitListedCourse->GetTitle() << endl;

            // 将观察者状态设置为 AddSuccess

            SetState(StudentState::AddSuccess);

            // 从课程候补名单中移除学生

            waitListedCourse->Release(this); // 从 Subject

            // 移除

            waitListedCourse = nullptr; // 将 Subject 链接

            // 设置为空

        }

    }

}

void Student::PrintCourses() const

{

    cout << "Student: (" << GetFirstName() << " " <<

    cout << GetLastName() << ") enrolled in " << endl;

    for (int i = 0; i < MAXCOURSES &&

        courses[i] != nullptr; i++)

        cout << "\t" << courses[i]->GetTitle() << endl;

}

（课程）。其中一种变化可能是当课程开放报名时，或者在学生退课后，可能存在“新名额可用”的状态。此时 `Notify()` 会调用每个观察者（Observer）的 `Update()`。我们在 `Student` 中重写了 `Update()` 以获取课程（Subject）的状态。如果状态显示课程现在已开放报名或有“新名额可用”，我们会尝试

`AddCourse(waitListedCourse);`；如果执行成功，我们将学生（Observer）的状态设为 `StudentState::AddSuccess`（**添加成功**（`Add Success`）），这意味着我们已经添加了该课程。接下来，由于我们在 `Update()` 中执行成功了，并且我们已经将所需的课程添加到当前的课程列表中，我们现在可以将自己从课程的等待列表中移除了。也就是说，我们将使用 `waitListedCourse->Release(this);` 将自己（Student）作为观察者从 Subject（课程的等待列表）中移除。现在我们已经添加了所需的课程，也可以删除与 Subject 的连接。最后，上述的 `Student` 包含一个方法，用于打印该学生当前选的课程。该方法非常简单。

## 整合组件

现在让我们通过查看 `main()` 函数来整合所有组件，看看我们的观察者模式是如何协调的：

```cpp

int main()

{

    // 实例化几个课程

    Course *c1 = new Course("C++", 0);

    Course *c2 = new Course("Advanced C++", 0);

    Course *c3 = new Course("C++ Design Patterns", 0);

    // 实例化学生，选择一个课程进入等待列表，

    // 在注册开始时添加

    Student s1("Anne Chu", c1);

    Student s2("Joley Putt", c1);

    Student s3("Geoff Kurt", c1);

    Student s4("Ling Mau", c1);

    Student s5("Jang Wu", c1);

    cout << "Registration is Open" << endl;

    cout << "Waitlist Students to be added to Courses" << endl;

    // 向学生发送消息，告知等待列表已开放。

    c1->Open();

    c2->Open();

    c3->Open();

    // 等待列表中的学生将被自动添加（取决于名额）

    // 现在注册已开放，添加更多课程

    cout << "During registration open, Students now adding additional courses" << endl;

    // 尝试添加更多课程。如果已满，我们将进入等待列表。

    s1.AddCourse(c2);

    s2.AddCourse(c2);

    s4.AddCourse(c2);

    s5.AddCourse(c2);

    s1.AddCourse(c3);

    s3.AddCourse(c3);

    s5.AddCourse(c3);

    cout << "Registration complete\n" << endl;

    // 打印每个课程的名单

    c1->PrintStudents();

    c2->PrintStudents();

    c3->PrintStudents();

    // 打印每个学生的课程列表

    s1.PrintCourses();

    s2.PrintCourses();

    s3.PrintCourses();

    s4.PrintCourses();

    s5.PrintCourses();

    return 0;

}

```

回顾上述的 `main()` 函数，我们首先实例化了三个 `Course` 实例。接着我们实例化了五个 `Student` 实例，利用构造函数允许我们提供每个学生在注册开始时想要添加的初始 `Course`。注意，这些学生（观察者）将被添加到他们心仪课程（Subject）的等待列表中。在这里，一个 Subject（课程）将有一份观察者（学生）列表，这些学生希望在注册开放时添加该课程。

接下来，我们看到许多学生向往的课程通过 `c1->Open()` 变为开放报名。`Course::Open()` 将 Subject 的状态设置为 `CourseState::OpenEnrollment`，易地地指示课程已开放报名，然后调用 `Notify()`。正如我们所知，`Subject::Notify()` 会调用 Subject 观察者列表上的 `Update()`。在这里，处于等待列表的 `Course` 实例将被添加到学生的日程，并随后作为观察者从 Subject 的等待列表中移除。

现在注册已开放，每个 `Student` 都将尝试以通常的方法使用 `bool Student::AddCourse(Course *)` 尝试添加更多课程，例如 `s1.AddCourse(c2)`。如果某个课程已满，学生将被添加到课程的等待列表中（这被建模为继承自 Subject 的观察者列表，这些实际上是派生的 `Student` 类型）。回想 `Course` 继承自 `Subject`，它维护了一个对添加特定课程感兴趣的学生列表（观察者等待列表）。当课程状态变为“新名额可用”时，等待列表上的学生（通过数据成员 `observers`）将收到通知，每个 `Student` 的 `Update()` 方法随后会调用相应的 `AddCourse()`。

一旦我们添加了各种课程，我们将看到每个 `Course` 打印它的学生名单，例如 `c2->PrintStudents()`。同样，我们将看到每个 `Student` 打印他们所选的课程，例如 `s5.PrintCourses()`。

让我们来看这个程序的输出：

```
Registration is Open
Waitlist Students to be added to Courses
Anne Chu removed from waitlist and added to C++
Geoff Kurt removed from waitlist and added to C++
Jiang Wu removed from waitlist and added to C++
Joley Putt removed from waitlist and added to C++
Ling Mau removed from waitlist and added to C++
During open registration, Students now adding more courses
Registration complete
Course: (C++) has the following students:
Anne Chu
Geoff Kurt
Jiang Wu
Joley Putt
Ling Mau
Course: (Advanced C++) has the following students:
Anne Chu
Joley Putt
Ling Mau
Jiang Wu
Course: (C++ Design Patterns) has the following students:
Anne Chu
Geoff Kurt
Jiang Wu
Joley Putt
Ling Mau
```

我们现在已经看到了观察者模式的实现。我们把更通用的 `Subject` 和 `Observer` 类整合到了我们熟悉的类框架中，即 `Course` 和 `Student`。在继续之前之前，让我们简要回顾一下我们学到的关于模式的知识。

## 总结

在本章中，我们通过将知识库从 OOP 概念扩展到包含设计模式，开始了成为更优秀的 C++ 程序员的追求。我们的首要目标是使你能够应用常用模式，利用经过验证的解决方案来解决重复类型的编码问题。

我们首先理解了设计模式的目的，然后具体理解了观察者模式背后的原理以及它对 OOP 的贡献。最后，我们查看了如何在 C++ 中实现观察者模式。

利用常用的设计模式（如观察者模式）将帮助你更更容易以其他程序员能够理解的方式来解决重复类型的编程问题。OOP 的一个核心原则是尽可能追求组件的复用。通过利用设计模式，你将通过更复杂的编程技术贡献可复用的解决方案。

我们现在准备好继续学习第17章中的下一个设计模式：实现工厂模式。在技能库中增加更多模式使我们成为更有多才且受重视的程序员。

## 问题

- 1. 以本章示例的在线代码为起点，并结合之前练习的解答（第10章实现关联、聚合与组合的第3题）：
    - 实现（或修改你先前的）`Student::DropCourse()`。当学生退课某个课程时，此事件将导致课程状态变为状态 2，“新名额可用”。随着状态变化，将在课程（Subject）上调用 `Notify()`，随后将 `Update()`观察者列表（等待列表上的学生）。`Update()` 将间接允许任何等待列表中的 `Student` 实例现在添加该课程。
- 2. 最后，在 `DropCourse()` 中，记得从学生的当前课程列表中移除退掉的课程。
- 2. 你还能想象到哪些可能容易结合观察者模式的例子？

# 17

## 应用工厂模式

本章将继续扩展你的 C++ 编程技能库，超越核心 OOP 概念，目标是使你能够利用常用的设计模式解决重复类型的编码问题。我们知道，引入设计模式可以增强代码的可维护性，并为潜在的代码重用提供途径。

继续演示和解释流行的设计模式与惯用法，并学习如何在 C++ 中有效地实现它们，我们将通过工厂模式（更准确地说是工厂方法模式）继续我们的探索。

在本章中，我们将涵盖以下主要主题：

- 理解工厂方法模式以及它对 OOP 的贡献
- 理解如何在没有对象工厂（Object Factory）的情况下实现工厂方法，并比较对象工厂与抽象工厂

在本章结束时，你将理解流行的工厂方法模式。我们将看到该模式在 C++ 中的两种示例实现。在你的编程技能库中增加额外的核心设计模式将使成为一个更老练、更有价值的程序员。

让我们通过研究另一个常用的设计模式——工厂方法模式来提升我们的编程技能。

## 技术要求

完整程序示例在线代码可以在以下 GitHub URL 找到：https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/tree/main/Chapter17。每个完整程序示例都可以在 GitHub 仓库相应的章节标题（子目录）中找到，文件名与章节号对应，后跟一个连字符，然后是当前章节中的示例编号。例如，本章的第一个完整程序可以在上述 GitHub 目录下的 Chapter17 子目录中 Chp17-Ex.cpp 的文件中找到。

本章的 CiA 视频可以在此处查看：https://bit.ly/3QOmCC1。

## 理解工厂方法模式

工厂模式（或工厂方法模式）是一种创建型设计模式，它允许在不需要指定要实例化的具体（派生）类的情况下创建对象。工厂方法提供了一个创建对象的接口，但允许创建方法内部的细节来决定实例化哪个（派生）类。

工厂方法也被称为虚拟构造函数。正如虚拟析构函数通过动态绑定在运行时确定特定的析构函数（析构序列的入口点）一样，虚拟构造函数的概念是待实例化的目标对象在运行时统一确定。

我们无法总是预测应用程序中所需的相关的派生类对象的特定组合。工厂方法（或虚拟构造函数）可以根据提供的输入，按需创建多个相关派生类类型之一的实例。工厂方法将以其基类类型返回派生类对象，使得对象可以更通用地进行创建和存储。多态操作可以应用于新创建的（向上转换的）实例，从而让相关的派生类行为显现出来。工厂方法通过消除在客户端代码中绑定特定派生类类型的需求，促进了与客户端代码的松耦合。客户端只需利用工厂方法来创建并提供相应的实例。

通过工厂方法模式，我们将指定一个抽象类（或接口）来收集和指定我们想要创建的派生类的通用行为。该模式中的抽象类或接口被称为**产品（Product）**。然后，我们创建可能想要实例化的派生类，重写任何必要的抽象方法。各种具体类被称为**具体产品（Concrete Products）**。

然后，我们指定一个工厂方法，其目的是提供一个统一创建具体产品实例的接口。工厂方法可以放置在抽象产品类中，也可以放在单独的工厂类中；**对象工厂（Object Factory）**代表一个承担创建具体产品任务的类。如果工厂（创建）方法放在抽象产品类中，它将是静态的；如果放在对象工厂类中，则可选为静态的。工厂方法将根据一致的输入参数列表决定制造哪个具体产品。工厂方法将返回一个指向具体产品的通用产品指针。多态方法可以应用于新创建的对象以触发其特定行为。

工厂方法模式将包含以下内容：

- 一个抽象产品类（或接口）。
- 多个具体产品派生类。
- 位于抽象产品类中或单独对象工厂类中的工厂方法。工厂方法将具有统一的接口，用于创建任何具体产品类型的实例。
- 具体产品将作为通用的产品实例由工厂方法返回。

请记住，工厂方法（无论是否在对象工厂中）都会产生产品。工厂方法提供了一种统一的方式来生产多种相关的产品类型。存在多个工厂方法来产生独特的产品线；每个工厂方法都可以通过有意义的名称来区分，即使它们的签名恰好相同。

让我们继续查看工厂方法方法的两个示例实现。

## 实现工厂方法模式

我们将探索工厂方法模式的两种常见实现。每种实现都会有设计权衡，绝对值得讨论！

让我们从将工厂方法放置在抽象产品类中的技术开始。

## 在产品类中包含工厂方法

为了实现工厂方法模式，我们首先需要创建抽象产品类以及我们的具体产品类。这些类定义将为构建我们的模式奠定基础。

在示例中，我们将使用我们熟悉的类——Student（学生）来创建产品。然后，我们将创建具体产品类，即 GradStudent（研究生）、UnderGradStudent（本科生）和 NonDegreeStudent（非学位学生）。我们将在产品（Student）类中包含一个工厂方法，并具有一致的接口来创建任何派生产品类型。

我们将通过添加类来根据教育目标区分学生，从而为现有的 Student 应用程序构建框架进行建模。这些新组件为大学入学（新学生录取）系统提供了基础。

让我们假设，应用程序不是实例化一个 Student，而是根据学习目标实例化不同类型的 Student —— 各种派生类 Student（如 GradStudent、UnderGradStudent 或 NonDegreeStudent）。Student 类将包含一个抽象的 `Graduate()` 操作；每个派生类将重写该方法并有不同的实现。例如，一个寻求博士位的 GradStudent 在 `GradStudent::Graduate()` 方法中需要满足的比 Student 其他派生类更多的学位相关标准。他们可能需要验证学分、验证及格点，并验证其论文已被接受。相比之下，本科生可能只需要验证他们的学分和总平均分。

抽象产品类将包含一个静态方法 `MatriculateStudent()`，作为工厂方法来创建各种类型的学生（具体产品类型）。

## 定义抽象产品类

让我们看看工厂方法实现的机制，从检查我们的抽象产品类 Student 定义开始。此示例可以在我们的 GitHub 仓库找到：

https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter17/Chp17-Ex1.cpp

```cpp

// 假设 Person 类存在并有通常实现

class Student: public Person // 注意 Student 现在是

{

private:

    // 一个抽象类

    float g = 0.0; // 类内初始化

    string currentCourse;

    const string studentId;

    static int numStudents;

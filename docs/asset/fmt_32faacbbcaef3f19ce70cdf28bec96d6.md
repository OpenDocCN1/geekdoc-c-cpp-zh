
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

public class Student
{
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public Student(string firstName, string lastName)
    {
        this.FirstName = firstName;
        this.LastName = lastName;
    }

    public string Name
    {
        return this.FirstName + " " + this.LastName;
    }

    public override string ToString()
    {
        return "Student: " + this.Name;
    }
}

public class Group
{
    public string Name { get; set; }
    public List<Student> Students { get; set; }
    public Teacher Teacher { get; set; }

    public Group(string name)
    {
        this.Name = name;
        this.Students = new List<Student>();
    }

    public override string ToString()
    {
        StringBuilder groupAsString = new StringBuilder();
        groupAsString.Append("Group name: " + this.Name);
        groupAsString.Append("Students in the group: " + 
            string.Join(", ", this.Students.Select(s => s.Name)));
        if (this.Teacher != null)
        {
            groupAsString.Append("Group teacher: " + this.Teacher.Name);
        }
        return groupAsString.ToString();
    }
}

public class Teacher
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public List<Group> Groups { get; set; }

    public Teacher(string firstName, string lastName)
    {
        this.FirstName = firstName;
        this.LastName = lastName;
        this.Groups = new List<Group>();
    }

    public string Name
    {
        get
        return this.FirstName + " " + this.LastName;
    }

    public override string ToString()
    {
        StringBuilder teacherAsString = new StringBuilder();
        teacherAsString.AppendLine("Teacher name: " + this.Name);
        teacherAsString.Append("Groups of this teacher: " + 
            string.Join(", ", this.Groups.Select(s => s.Name)));
        return teacherAsString.ToString();
    }
}

public class School {
    public string Name { get; set; }
    public List<Teacher> Teachers { get; set; }
    public List<Group> Groups { get; set; }
    public List<Student> Students { get; set; }

    public School(string name) 
    {
        this.Name = name;
        this.Teachers = new List<Teacher>();
        this.Groups = new List<Group>();
        this.Students = new List<Student>();
    }

    public override string ToString() 
    {
        StringBuilder schoolAsString = new StringBuilder();
        schoolAsString.Append("School name: " + this.Name);
        schoolAsString.Append("Teachers: " +
            string.Join(", ", this.Teachers.Select(s => s.Name)));
        schoolAsString.Append("Students: " +
            string.Join(", ", this.Students.Select(s => s.Name)));
        schoolAsString.Append("Groups: " +
            string.Join(", ", this.Groups.Select(s => s.Name)));
        foreach (var teacher in this.Teachers) 
        {
            schoolAsString.Append("\n---\n");
            schoolAsString.Append(teacher);
        }
        foreach (var group in this.Groups) 
        {
            schoolAsString.Append("\n---\n");
            schoolAsString.Append(group);
        }
        foreach (var student in this.Students) 
        {
            schoolAsString.Append("\n---\n");
            schoolAsString.Append(student);
        }
        return schoolAsString.ToString();
    }
}

class TestSchool {
    static void Main() 
    {
        // 创建几个学生
        Student studentPeter = new Student("Peter", "Lee");
        Student studentGeorge = new Student("George", "Redwood");
        Student studentMaria = new Student("Maria", "Steward");
        Student studentMike = new Student("Michael", "Robinson");

        // 创建一个小组并向其中添加几个学生
        Group groupEnglish = new Group("English language course");
        groupEnglish.Students.Add(studentPeter);
        groupEnglish.Students.Add(studentMike);
        groupEnglish.Students.Add(studentMaria);
        groupEnglish.Students.Add(studentGeorge);

        // 创建一个小组并向其中添加几个学生
        Group groupJava = new Group("Java Programming course");
        groupJava.Students.Add(studentMaria);
        groupJava.Students.Add(studentPeter);

        // 创建一名老师并将其分配给几个小组
        Teacher teacherNatasha = new Teacher("Natasha", "Walters");
        teacherNatasha.Groups.Add(groupEnglish);
        teacherNatasha.Groups.Add(groupJava);
        groupEnglish.Teacher = teacherNatasha;
        groupJava.Teacher = teacherNatasha;

        // 创建另一个老师和他教授的小组
        Teacher teacherSteve = new Teacher("Steve", "Porter");
        Group groupHTML = new Group("HTML");
        groupHTML.Students.Add(studentMike);
        groupHTML.Students.Add(studentMaria);
        groupHTML.Teacher = teacherSteve;
        teacherSteve.Groups.Add(groupHTML);

        // 创建一个学校并添加学生和老师
        School school = new School("Saint George");
        school.Students.Add(studentPeter);
        school.Students.Add(studentGeorge);
    }
}
```

# 结语

如果你正在阅读这段结语，并且已经仔细阅读了整本书，那么请**接受我们实至名归的祝贺！** 我们相信你已经在编程原理方面获得了了宝贵的知识，这些知识将令你终身受益。岁月流逝，技术演进，文化远离现状，但如果你在信息技术领域工作，编程中数据结构的基础知识、算法思维以及解决编程问题的积累经验将始终为你服务。

## 你解决了所有问题吗？

如果你**解决了所有章节中的所有问题**，并且还仔细阅读了整本书，那么你就可以自豪地**宣布自己是一名程序员了**。你现在学习的任何技术都将小一碟。现在既然你已经掌握了编程的基础和基本原理，你就能轻松地学会使用数据库和 SQL，开发 Web 应用和服务器端软件（例如使用 ASP.NET 和 WCF）、HTML5 应用、移动设备应用以及任何你想要的内容。相比于大多数程序员，你拥有**巨大的优势**，因为他们不知道什么是哈希表、树搜索是如何工作的，以及什么是算法复杂度。如果你付出了巨大的努力来解决书中的所有问题，那么你绝对已经达到了对编程概念的**基础性理解水平以及程序员的思维方式**，这将让你受益多年。

## 你在练习中遇到困难了吗？

如果你还没有解决练习题，或者至少没有解决大部分题目，**请回去解决它们！** 是的，这确实需要大量时间，但这就是学习编程的方式——通过大量的工作和努力。不加实践，你就学不会！

如果你遇到了困难，请**使用编程基础课程的讨论论坛**或 [Software Academy](http://forums.academy.telerik.com)。参考此书：http://forums.academy.telerik.com。有数百人参加了这些课程，其中大多数人都解决了所有问题并分享了他们的。因此，请查看它们，尝试解决问题，然后在不看任何指南的情况下再次尝试。

# 使用 C# 的计算机编程基础

Telerik 在本书网站（http://www.introprogramming.info）上上传了许多讲座和视频教程。我们为书的每一章提供了英语和保加利亚语的免费 幻灯片和视频。这些对你会有帮助，特别是如果你是第一次接触编程的话。如果你决定教授 C#、编程或数据结构与算法，幻灯片和练习题将帮助你专注于培训并节省准备内容的时间。这值得一试。

此外，请查看 Telerik Software Academy (http://academy.telerik.com) 提供的免费课程。他们所有的学习材料和视频录制已在每个课程相应的网站上免费下载。这些课程是你作为软件工程师和软件开发专业人员进步的极佳后续。本书网站和 Telerik Academy 网站上的所有材料（演讲幻灯片、练习、演示）以及部分视频录制均提供英文。

## 读完书后你如何继续？

你可能在想如何继续你作为软件工程师的开发。你已经通过这本书奠定了坚实的基础，所以这并不困难。我们可以给你以下建议：

- 1. 选择一种语言和一种编程平台，例如 C# + .NET Framework、Java + Java EE、Ruby + Rails 或 PHP + CakePHP。使用 C# 没有任何问题。专注于你所在平台支持的技术；你将很快学会相应的语言。例如，如果你选择了 Objective-C 和 iPhone / iPad / iOS，你从书中学到的算法思维将帮助你取得进步。
- 2. 阅读一本关于数据库的书，学习如何使用表格和它们之间的关系为你的应用程序建模。学习如何编写 SQL 查询来选择和更新数据。学习如何与 Oracle、SQL Server 或 MySQL 等数据库服务器协作。自然的行动路线是获取 ORM 技术框架 Hibernate 和 JPA。你也可以尝试公有云中提供的 NoSQL 数据库系统。
- 3. 获取构建动态 Web 网站的技术。从 HTML、CSS、JavaScript 和 jQuery 的书籍开始，配合我们关于 HTML5、CSS3 和 JavaScript 的免费课程 (http://html5course.telerik.com)。然后探索平台支持的 Web 开发工具，例如使用 .Net Framework 和 C# 的 ASP.NET Web Forms / .NET MVC，使用 Java 语言的 Servlets / JSF，使用 PHP 的 CakePHP / Symfony / Django Framework，Ruby on Rails 或 Python 的 Django。学习如何创建具有动态内容的简单 网站。使用移动 UI 工具包为移动设备创建 Web 应用。
- 4. 学习编写移动应用程序。例如从 HTML5 和 Cordova 开始，将你的应用部署到 Google、Apple、Microsoft 和 Amazon 管理的大型市场。学习原生移动开发（例如 Java 和 Android 开发以及 Objective C 和 iOS 开发）。创建一个移动应用（例如某个游戏）并将其部署在某个主要市场。这样你将经历整个设计/开发/发布周期，这将带给你真实的移动开发经验。
- 5. 开始从事一个更严肃的项目，如 Web 市场或仓库管理程序或会计软件。这将给你机会遇到实际软件开发中的实际问题。你将获得更有价值的实践经验，并发现编写高级软件比编写代码要困难得多。
- 6. 找一份工作。如果你付出了巨大的努力来解决书中的所有问题，那么你绝对已经达到了对编程概念的基础性理解水平以及程序员的思维方式，这将让你受益多年。

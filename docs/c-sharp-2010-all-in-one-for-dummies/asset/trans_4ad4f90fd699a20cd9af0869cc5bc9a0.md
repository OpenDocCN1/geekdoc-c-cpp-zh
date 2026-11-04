
The no-PIA feature allows you to continue to use PIAs at design time without having them around at runtime. Instead, the C# 4.0 compiler bakes the small part of the PIA that a program actually uses directly into its assembly. The PIA doesn't have to be loaded at runtime.
无 PIA 功能允许你在设计时继续使用 PIA，而在运行时无需它们存在。相反，C# 4.0 编译器会将程序实际使用的 PIA 的小部分直接烘焙到其程序集中。PIA 在运行时不必加载。

To see how this works, try these steps in both Visual Studio 2010 and Visual Studio 2008 (if you have it):
要了解其工作原理，请在 Visual Studio 2010 和 Visual Studio 2008（如果有）中尝试以下步骤：

- 1. Create a new console application by choosing File→New→Project and picking C#→Console application. Name your project PIAs.
- 1. 通过选择 File→New→Project 创建新的控制台应用程序，并选择 C#→Console application。将你的项目命名为 PIAs。
- 2. After the project loads, right-click on References.
- 2. 项目加载后，右键单击 References。
- 3. Click Add Reference.
- 3. 单击 Add Reference。
- 4. Select Microsoft.Office.Interop.Excel, version 12, if you have it. Otherwise, use the latest version you have loaded.
- 4. 选择 Microsoft.Office.Interop.Excel，版本 12，如果你有的话。否则，使用你已加载的最新版本。
- 5. Click OK.
- 5. 单击 OK。
- 6. Add using Microsoft.Office.Interop.Excel; to the header.
- 6. 在头部添加 using Microsoft.Office.Interop.Excel;。
- 7. Change the Main procedure to the following (just enough to get Excel rolling):
- 7. 将 Main 过程更改为以下内容（足以启动 Excel）：
- 8. Right-click on the Solution and select Add Project.
- 8. 右键单击 Solution 并选择 Add Project。
- 9. Add a new Setup project.
- 9. 添加新的 Setup 项目。
- 10. Right-click on the Setup project and choose Add→Project Output.
- 10. 右键单击 Setup 项目并选择 Add→Project Output。
- 11. Select Primary Output.
- 11. 选择 Primary Output。
- 12. Click OK.
- 12. 单击 OK。

```csharp
static void Main(string[] args)
{
    Microsoft.Office.Interop.Excel.Application
    xl = new Application();
    xl.Quit();
}
```

The setup project will automatically determine what to deploy with the application. In Visual Studio 2008, with C# 3.0, it will deploy the primary Interop assemblies, as shown in Figure 3-1.
设置项目将自动确定随应用程序一起部署的内容。在 Visual Studio 2008 中，使用 C# 3.0，它将部署主 Interop 程序集，如图 3-1 所示。

In Visual Studio 2010, the setup doesn't deploy the PIAs. The specific parts being used are compiled right into the EXE for the application. This is demonstrated in Figure 3-2.
在 Visual Studio 2010 中，设置不会部署 PIA。正在使用的特定部分会被直接编译到应用程序的 EXE 中。这在图 3-2 中有所演示。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_818_0.png)

Figure 3-1:
Deploying the PIAs in C# 3.0
Figure 3-1:
在 C# 3.0 中部署 PIA

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_818_1.png)

Figure 3-2:
Deploying without PIAs in C# 4.0
Figure 3-2:
在 C# 4.0 中不使用 PIA 部署

## Skipping the Ref Statement
## 跳过 Ref 语句

Because of a different programming model, many COM APIs contain a lot of reference parameters. Contrary to refs in C#, these are typically not meant to mutate a passed-in argument for the subsequent benefit of the caller but are simply another way of passing value parameters.
由于不同的编程模型，许多 COM API 包含大量引用参数。与 C# 中的 ref 相反，这些参数通常并非旨在为了调用者的后续利益而修改传入的参数，而只是传递值参数的另一种方式。

It therefore seems unreasonable that a C# programmer should have to create temporary variables for all such ref parameters and pass these by reference. So let's delete them.
因此，要求 C# 程序员为所有此类 ref 参数创建临时变量并按引用传递似乎不合理。所以让我们删除它们。

Instead, specifically for COM methods, the C# compiler allows you to pass arguments by values to such a method and automatically generates temporary variables to hold the passed-in values, subsequently discarding these when the call returns. In this way, the caller sees value semantics and doesn't experience any side effects, but the called method still gets a reference.
相反，专门针对 COM 方法，C# 编译器允许你按值传递参数给此类方法，并自动生成临时变量来保存传入的值，在调用返回时随后丢弃这些变量。这样，调用者看到的是值语义并且不会经历任何副作用，但被调用的方法仍然获得引用。

You can see this in action in the canonical optional parameter example from Chapter 2. In the usual SaveAs from Microsoft Word, everything is a reference parameter.
你可以在第 2 章的典型可选参数示例中看到这一点。在 Microsoft Word 中通常的 SaveAs 中，一切都是引用参数。

```csharp
object filename = "test.docx";
object missing = System.Reflection.Missing.Value;

doc.SaveAs(ref filename,
    ref missing, ref missing, ref missing,
    ref missing, ref missing, ref missing,
    ref missing, ref missing, ref missing,
    ref missing, ref missing, ref missing);
```

In C# 4.0, you can skip both the "missing" optional parameters and the ref statement.
在 C# 4.0 中，你可以跳过 "missing" 可选参数和 ref 语句。

```csharp
object filename = "test.docx";
doc.SaveAs(filename);
```

## Chapter 4: Revising Generics
## 第 4 章：修订泛型

### In This Chapter
### 本章内容

- Understanding variance
- 理解协变
- Working with contravariance
- 使用逆变
- Using covariance
- 使用协变

Generics are covered in length in Books I and II, as they relate to creating collections of objects or business concepts, and how they impact object-oriented programming. They also play a large role in dynamic design and programming, which Chapter 1 of this book covers.
泛型在第一册和第二册中进行了详细介绍，因为它们与创建对象或业务概念的集合以及它们如何影响面向对象编程有关。它们在动态设计和编程中也发挥着重要作用，本书第 1 章对此进行了介绍。

The generics model implemented in C# 2.0 was incomplete. Although parameters in C# all allow for variance in several directions, generics do not.
C# 2.0 中实现的泛型模型是不完整的。虽然 C# 中的参数在多个方向上都允许变体，但泛型不允许。

Variance has to do with types of parameters and return values. Covariance means that an instance of a subclass can be used when an instance of a parent class is expected, while Contravariance means that an instance of a superclass can be used when an instance of a subclass is expected. When neither is possible, it is called Invariance.
变体与参数类型和返回值有关。协变意味着当期望父类实例时，可以使用子类实例，而逆变意味着当期望子类实例时，可以使用超类实例。当两者都不可能时，称为不变。

All fourth-generation languages support some kind of variance. In C# 3.0 and earlier versions, parameters are covariant and return types are contravariant. So, this works because string and integer parameters are covariant to object parameters:
所有第四代语言都支持某种变体。在 C# 3.0 及更早版本中，参数是协变的，返回类型是逆变的。因此，这可行是因为 string 和 integer 参数对 object 参数是协变的：

```csharp
public static void MessageToYou(object theMessage)
{
    if (theMessage != null)
        Console.WriteLine(theMessage);
}
//then:
MessageToYou("It's a message, yay!");
MessageToYou(4+6.6);
```

And this works because object return types are contravariant to string and integer return types (for example):
这可行是因为 object 返回类型对 string 和 integer 返回类型是逆变的（例如）：

```csharp
object theMessage = MethodThatGetsTheMessage();
```

Generics are nonvariant in C# 2.0 and 3.0. This means that if Basket<apple> is of type Basket<fruit>, those Baskets are not interchangeable like strings and objects are in the preceding example.
在 C# 2.0 和 3.0 中，泛型是不变的。这意味着如果 Basket<apple> 是 Basket<fruit> 的类型，那么这些 Basket 就像前面的示例中字符串和对象一样不可互换。

## Variance
## 变体

If we look at a method like the preceding one:
如果我们查看前面那样的方法：

```csharp
public static void WriteMessages()
{
    List<string> someMessages = new List<string>();
    someMessages.Add("The first message");
    someMessages.Add("The second message");
    MessagesToYou(someMessages);
}
```

and then we try to call that method like we did earlier with a string type:
然后我们尝试像之前对 string 类型那样调用该方法：

```csharp
//This doesn't work in C#3!!
public static void MessagesToYou(IEnumerable<object> theMessages)
{
    foreach (var item in theMessages)
        Console.WriteLine(item);
}
```

this fails in Visual Studio 2008. Generics are invariant in C# 3.0. But, in Visual Studio 2010 this complies because IEnumerable<T> is covariant — you can use a more derived type as a substitute for a higher-order type. Let's look at a real example.
这在 Visual Studio 2008 中失败。泛型在 C# 3.0 中是不变的。但是，在 Visual Studio 2010 中这是合规的，因为 IEnumerable<T> 是协变的——你可以使用更派生的类型作为更高阶类型的替代。让我们看一个实际例子。

## Contravariance
## 逆变

In my scheduling application, I have Events, which have a date, and then a set of subclasses, one of which is Course. A Course is an Event. Courses know their own number of students.
在我的调度应用程序中，我有 Events，它们有一个日期，然后是一组子类，其中之一是 Course。Course 是一个 Event。Courses 知道自己的学生人数。

Anyway, back at the ranch, I have a method called MakeCalendar.
无论如何，回到正题，我有一个名为 MakeCalendar 的方法。

```csharp
public void MakeCalendar(IEnumerable<Event> theEvents)
{
    foreach (Event item in theEvents)
    {
        Console.WriteLine(item.WhenItIs.ToString());
    }
}
```

Pretend it makes a calendar; for now, all it does is print the date to the console. MakeCalendar is systemwide, so it expects some enumerable list of events.
假装它制作日历；目前，它所做的只是将日期打印到控制台。MakeCalendar 是系统范围的，因此它期望一些可枚举的事件列表。

I also have a Sort algorithm at the main system, called EventSorter. This is used to pass into the Sort method of collections. It expects to be called from a list of Events. Here is the EventSorter class:
我在主系统上还有一个名为 EventSorter 的排序算法。这用于传递到集合的 Sort 方法中。它期望从 Events 列表中调用。以下是 EventSorter 类：

```csharp
class EventSorter : IComparer<Event>
{
    public int Compare(Event x, Event y)
    {
        return x.WhenItIs.CompareTo(y.WhenItIs);
    }
}
```

I am writing the Instructor Led Training section of the event manager, and I need to make a list of courses, sort them, and then make a calendar. So I make my list of courses in ScheduleCourses, then I call sort and pass in the EventSorter:
我正在编写事件管理器的 Instructor Led Training 部分，我需要制作课程列表，对其进行排序，然后制作日历。所以我在 ScheduleCourses 中制作课程列表，然后调用 sort 并传入 EventSorter：

```csharp
public void ScheduleCourses()
{
    List<Course> courses = new List<Course>()
    {
        new Course(){NumberOfStudents=20, WhenItIs = new
        DateTime(2009,2,1)},
        new Course(){NumberOfStudents=14, WhenItIs = new
        DateTime(2009,3,1)},
        new Course(){NumberOfStudents=24, WhenItIs = new
        DateTime(2009,4,1)},
    };
    //Now I am passing an IComparer<Event> class to my
    //List<Course> collection.
    //It should be an IComparer<Course> but I can use
    //IComparer<Event> because of contravariance
    courses.Sort(new EventSorter());

    //I am passing a List of courses, where a List of Events
    //was expected.
    //We can do this because generic parameters are covariant
    MakeCalendar(courses);
}
```

But wait, this is a list of courses I am calling Sort from, right, not a list of events. Doesn't matter — IComparer<Event> is a contravariant generic for T (its return type) as compared to IComparer<Course> so I can still use the algorithm.
但是等等，我调用 Sort 的是一个课程列表，对吧，而不是事件列表。没关系——与 IComparer<Course> 相比，IComparer<Event> 对于 T（其返回类型）是逆变泛型，因此我仍然可以使用该算法。

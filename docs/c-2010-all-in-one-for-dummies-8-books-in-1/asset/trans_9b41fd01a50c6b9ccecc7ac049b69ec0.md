

# 796 变型

泛型在 C# 2.0 和 3.0 中是不变变的（nonvariant）。这意味着如果 `Basket<apple>` 的类型是 `Basket<fruit>`，那么在前一个示例中，这些 `Basket` 字符串和对象是不可交换的。

# 变型

如果我们看上一个方法：

```csharp
public static void WriteMessages()
{
    List<string> someMessages = new List<string>();
    someMessages.Add("The first message");
    someMessages.Add("The second message");
    MessagesToYou(someMessages);
}
```

然后我们尝试像之前对字符串类型那样调用方法：

```csharp
// 这在 C# 3 中不起作用的！！
public static void MessagesToYou(IEnumerable<object> messages)
{
    foreach (var item in messages)
        Console.WriteLine(item);
}
```

这在 Visual Studio 2008 中会失败。泛型在 C# 3.0 中是等变的（invariant）。但在 Visual Studio 2010 中，它可以编译通过，因为 `IEnumerable<T>` 是协变的（covariant）——你可以使用更派生的类型来替代高阶类型。让我们来看一个真实的示例。

# 逆变型

在我的调度应用程序中，我有 `Events`（事件），它们有一个日期，然后是一组子类，其中一个是 `Course`（课程）。`Course` 是一个 `Event`。`Course` 知道自己的学生人数。

无论如何，回到仓库，我有一个名为 `MakeCalendar` 的方法。

```csharp
public void MakeCalendar(IEnumerable<Event> theEvents)
{
    foreach (Event item in theEvents)
    {
        Console.WriteLine(item.WhenItIs.ToString());
    }
}
```

# 逆变型 797

假设它创建一个日历；目前，它只是将日期打印到控制台。`MakeCalendar` 是系统级的，所以它期望某个可枚举的事件列表。

我在主系统中还有一个名为 `EventSorter` 的排序算法。它用于传递集合的 `Sort` 方法。它期望从一个 `Events` 列表调用。这里是 `EventSorter` 类：

```csharp
class EventSorter : IComparer<Event>
{
    public int Compare(Event x, Event y)
    {
        return x.WhenItIs.CompareTo(y.WhenItIs);
    }
}
```

我正在为事件管理器编写讲师培训章节，我需要创建一个课程列表，对它们进行排序，然后创建一个日历。所以我在 `ScheduleCourses` 中创建了课程列表，然后调用 `sort` 并传入 `EventSorter`。

```csharp
public void ScheduleCourses()
{
    List<Course> courses = new List<Course>()
    {
        new Course(NumberOfStudents=20, WhenItIs = new DateTime(2009,2,1)),
        new Course(NumberOfStudents=14, WhenItIs = new DateTime(2009,3,1)),
        new Course(NumberOfStudents=24, WhenItIs = new DateTime(2009,4,1));
    }
    // 我现在将一个 IComparer<Event> 类传递给我的
    // List<Course> 集合。
    // 它应该是 IComparer<Course>，但由于逆变型，
    // 我可以使用 IComparer<Event>
    courses.Sort(new EventSorter());
}
```

```csharp
// 我正在传递一个课程列表，而原本期望的是 Events 列表。
// 我们可以这样做，是因为泛型参数是协变的
MakeCalendar(courses);
```

但等一下，这是我调用 `Sort` 的一个课程列表，而不是事件列表。没关系——与 `IComparer<Course>` 相比，`IComparer<Event>` 是 `T`（其返回类型）的逆变型泛型（contravariant），所以我仍然可以使用该算法。

第八卷
第 4 章
修订泛型

现在我必须将我的列表传递到 `MakeSchedule` 方法中，但该方法期望一个可枚举的 `Events` 集合。因为现在泛型参数是协变的，我可以传递一个 `Courses` 列表，因为 `Course` 对 `Event` 是协变的。理解为什么吗？

逆变型的另一个例子是它使用的是参数而不是返回值。如果我有一个返回泛型 `Courses` 列表的方法，我可以以期望 `Events` 列表的方式来调用该方法，因为 `Event` 是 `Course` 的父类。

你知道你可以如何拥有一个返回 `String` 的方法并将返回值赋值给你声明为 `object` 的变量吗？现在你对泛型集合也可以这样做。。通常情况下，C# 编译器会对泛型版本做出假设。只要你在参数链中向上移动，或者在返回类型链中向下移动，C# 就会推断出类型。

# 协变型

现在我必须将我的列表传递到 `MakeSchedule` 方法中，但该方法期望一个可枚举的 `Events` 集合。因为现在泛型参数是协变的，我可以传递一个 `Courses` 列表，因为 `Course` 对 `Event` 是协变的。这是参数的协变。

# 索引 特殊字符

- + (一元)运算符, 74
- ! (非)运算符, 79
- != (不等于)运算符, 77
- % (取模)运算符, 74, 140
- & (与)运算符, 79
- && (与)运算符, 79, 102
- * (乘法)运算符, 73-81
- / (除法)运算符, 74
- : (冒号), 定义, 286
- \ (反斜杠字符), 35
- \0 (空字符), 35
- \n (换行符), 35, 220
- \r (回车符字符), 35
- \t (制表符), 35
- | (或)运算符, 79
- _ (下划线), 257
- | (或)运算符, 79
- || (或)运算符, 79, 102
- ~ (波号), 305
- + (加法)运算符, 74
- < (小于)运算符, 77
- <= (小于或等于)运算符, 77
- = (等号), 77
- == (相同值)运算符, 77
- > (大于)运算符, 77
- >= (大于或等于)运算符, 77
- ?: (三元)运算符, 90

- 抽象概念
- 方法的重要性, 234
- 面向对象编程
- 概述, 207–208
- 准备, 209
- 过程编程, 208
- 学术版本, Visual Studio, 485
- 访问控制
- 类
- 访问方法, 266
- 示例, 266–269
- 概述, 265
- 面向对象编程, 212
- 概述, 213
- 访问成员
- 类
- 访问级别, 264
- 示例, 264
- 内部, 387
- 保护, 390
- 保护内部, 392
- 重命名空间, 395
- 访问方法, 270
- 访问命名空间, 2 212
- 访问集合, 145–149
- 访问当前对象
- 定义的, 254
- 显式, 255
- 概述, 257
- 泛,, 259
- 泛到框架, 417–418
- 过程, 418
- System.Data 命名空间
- 连接数据源, 420–425
- 实体框架, 431–433
- 概述, 416–417
- 示例架构, 419
- 视觉工具, 425–428
- 编写数据, 428–431
- 抽象类
- 账户示例, 327–328
- 定义的, 328–330
- 使用, 353–354
- 因子化, 322–327
- 对象和,330
- 抽象关键字, 接口, 335
- 抽象化, 208
- 继承示例, 330

# 800 C# 2010 入门指南

- 访问互联网
- 这种类如何进入框架, 457–458
- System.Net 命名空间
- 检查网络状态, 459–460
- 从文件下载, 460–462
- 发送状态报告, 462–465
- 记录网络活动, 465–468
- 概述, 468

- 属性快捷方式
- 属性访问级别, 273
- 编译器创建的数据成员, 272–273 构造函数, 270
- AccountNumber 属性, 270–271
- AccumulateInterest() 方法, 295–296
- 活动设计器项目, 493
- 活动库项目, 493
- 适配器, 420
- 数据库特定的, 416
- 加 (+)运算符, 74
- 添加按钮, 代码片段管理器工具, 525
- 连接框, Visual Studio, 422–423
- 添加客户命令, 621–623
- 将项添加到 List<T> 类, 125 集合, 155
- DictionaryExample 程序, 127
- 添加新数据源链接, Visual Studio, 421
- 添加新项框, 530
- AddCustom, 623
- 管理工具, Visual Studio, 514
- AddRange() 方法, 184–189
- Add-as() 方法, 252–253
- 高级面板, Visual Studio, 520
- 受影响用户属性, DREAD 模型, 404
- 对齐输出程序, 61–62
- 全在一个文件夹, 383
- 更改发送的内容, 689–690
- 与 (&)运算符, 79
- AND (&&)运算符, 102
- 匿名方法, 368–374
- ANSI 文本, 438


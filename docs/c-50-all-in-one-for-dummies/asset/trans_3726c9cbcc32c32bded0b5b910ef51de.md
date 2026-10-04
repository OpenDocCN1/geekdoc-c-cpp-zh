

# WriteLine() 方法

你可能已经注意到，我在书中前面的程序示例使用的 `WriteLine()` 结构无非是一个由 `Console` 类调用的方法调用：

```
Console.WriteLine("this is a method call");
```

`WriteLine()` 是 .NET Framework 库提供的许多预定义方法之一。`Console` 预定义类指的是应用程序控制台（也称为命令提示符或命令窗口）。

到目前为止我使用的 `WriteLine()` 方法的参数是一个单一字符串。`+` 运算符允许程序员在将总和传递给 `WriteLine()` 之前将字符串组合在一起，或者将字符串与内置变量组合在一起：

```csharp
string s = "Sarah";
Console.WriteLine("My name is " + s + " and my age is " + 3);
```

在这种情况下，`WriteLine()` 看到的只有“My name is Sarah and my age is 3.”

`WriteLine()` 的第二种形式提供了更灵活的参数集：

```csharp
Console.WriteLine("My name is {0} and my age is {1}.", "Sarah", 3);
```

第一个参数是格式化字符串。字符串 "Sarah" 会插入在符号 {0} 出现的地方——0 指向格式化字符串之后的第一个参数。整数 3 被插入到由 {1} 标记的位置。这种形式比上一个示例更高效，因为字符串拼接并不像听起来那么简单。

# 第 4 章：关于这个我想说这些

在本章中
- 了解如何将对象传递给方法
- 比较类方法和实例方法
- 理解 `this` 是什么
- 知道当类没有某个方法时该怎么办
- 当类需要拥有某个方法时采取行动

本章强调了类的非静态方法。静态方法属于整个类，而非静态方法属于每个实例。静态和非静态成员之间存在重要的区别。

# 将对象传递给方法

你传递对象引用的方法与传递值类型变量的方法相同，唯一的区别是：你始终通过引用传递对象。下面的小程序演示了如何将对象传递给方法：

![](img/6dfbb88e9302e98442acc219bd7fc_268_0.png)

```csharp
// PassObject -- Demo如何将对象传递给方法。
using System;
namespace PassObject
{
    public class Student
    {
        public string name;
    }
    public class Program
    {
        public static void Main(string[] args)
        {
            Student student = new Student();
            // 直接访问设置名称。
            Console.WriteLine("The first time:");
            student.name = "Madeleine";
            OutputName(student);

            // 使用方法更改名称。
            Console.WriteLine("After modified:");
            SetName(student, "Willa");
            OutputName(student);

            // 等待用户确认。
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }

        // OutputName -- 输出学生的名字。
        public static void OutputName(Student student)
        {
            // 输出当前学生的名字。
            Console.WriteLine("Student's name is {0}", student.name);
        }

        // SetName -- 修改学生对象的名字。
        public static void SetName(Student student, string name)
        {
            student.name = name;
        }
    }
}
```

该程序创建了一个仅包含名称的学生对象。程序首先直接设置了学生的名称，并将学生对象传递给方法 `OutputName()`。`OutputName()` 显示它收到的任何 `Student` 对象的名字。

然后随后通过调用 `SetName()` 更新学生的名称。因为 C# 中的所有引用类型对象都是通过引用传递的，所以对 `student` 的更改被保留了。当 `Main()` 再次输出学生对象时，名称已经更改，代码所示：

```
The first time:
Student's name is Madeleine
After modified:
Student's name is Willa
Press Enter to terminate...
```

`SetName()` 方法可以更改 `Student` 对象中的名称并使其生效。

![](img/6dfbb88e9302e98442acc219bd7fc_269_0.png)

传递引用类型对象时不需要 `ref` 关键字。但效果是通过引用修改对象的内容。然而，如果 `SetName()` 尝试向其参数分配一个全新的 `Student` 对象，它不会影响方法外部的原始对象，正如这段代码所示：

```csharp
Student student = new Student();
SetName(student, "Pam");
Console.WriteLine(student.name);  // 仍然是 "Pam"

// 修改后的 SetName():
public static void SetName(Student student, string name)
{
    student = new Student(); // 不替换 SetName 外部的 student。
    student.name = name;
}
```

# 定义方法

类应该收集描述真实世界对象或概念的元素。例如，`Vehicle` 类可能包含最大速度、重量和负载能力的数据元素。然而，`Vehicle` 也具有活跃属性——行为——例如启动和停止等能力。这些活跃属性由与车辆数据相关的方法描述。这些方法与数据元素一样，都是 `Vehicle` 类的一部分。

# 定义静态方法

例如，你可以用稍微更好的方式重写上一节的程序：

![](img/6dfbb88e9302e98442acc219bd7fc_270_0.png)

```csharp
// StudentClassWithMethods -- Demo将对
// 类数据的操作方法放在类内部。类
// 负责它自己的数据以及对其的任何操作。
using System;
namespace StudentClassWithMethods
{
    // 现在 OutputName 和 SetName 方法是 
    // Student 的成员，而不是 Program 类。
    public class Student
    {
        public string name;
        // OutputName -- 输出学生的名字。
        public static void OutputName(Student student)
        {
            // 输出当前学生的名字。
            Console.WriteLine("Student's name is {0}", student.name);
        }
        // SetName -- 修改学生对象的名字。
        public static void SetName(Student student, string name)
        {
            student.name = name;
        }
    }
    public class Program
    {
        public static void Main(string[] args)
        {
            Student student = new Student();
            // 直接访问设置名称。
            Console.WriteLine("The first time:");
            student.name = "Madeleine";
            OutputName(student);

            // 使用方法更改名称。
            Console.WriteLine("After modified:");
            SetName(student, "Willa");
            OutputName(student);

            // 等待用户确认。
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
```

第二卷
第四章

关于这个我想说这些

除了名称之外，这个程序与 `PassObject` 程序相比只有一个一个重大变化：我将 `OutputName()` 和 `SetName()` 方法放在了 `Student` 类中。

许多程序员并不说在类“内部”（in），而是说类“上”（on）的成员。

由于这个变化，在调用 `SetName()` 和 `OutputName()` 时，`Main()` 必须引用 `Student` 类。这些方法现在是 `Student` 的成员，而不是 `Main()` 所在的 `Program` 类。

这一步很小，但意义重大。将 `OutputName()` 放在类内部可以实现更高层次的重用：需要显示对象的外部方法可以直接作为类的一部分在这里找到 `Outputname()`。它不需要由每个使用 `Student` 类的程序单独编写。

这种解决方案在哲学层也更好。`Program` 类不需要担心如何初始化 `Student` 对象的名称，也不需要担心如何输出信息。`Student` 类应该包含这些信息。对象应该负责自己。

事实上，`Main()` 就不应该将名称初始化为 `Madeleine`。它应该调用 `SetName()`。

在 `Student` 内部，一个成员方法可以调用另一个方法而无需明确应用类名。`SetName()` 可以调用 `OutputName()` 而不需要引用类名。如果你省略了类名，C# 会假设要访问的方法位于同一个类中或该类上。

# 定义实例方法

尽管 `OutputName()` 和 `SetName` 是静态方法，但它们同样可以是非静态（即实例）方法。

类的所有静态成员都是类成员，所有非静态成员都是实例成员。这包括方法。

对象（类的实例）的非静态数据成员是通过对象而不是类来访问的。因此，你可以说

```csharp
Student student = new Student(); // 创建 Student 的实例。
student.name = "Madeleine";      // 通过实例访问成员。
```


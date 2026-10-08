

# 定义方法 249

```cs
// 修改后的 SetName():
public static void SetName(Student student, string name)
{
    student = new Student(); // 不替换 SetName() 外部的 student 对象
    student.name = name;
}
```

# 定义方法

类被用于收集描述现实世界中的对象或概念的元素。例如，一个 `Vehicle`（车辆）类可能包含最大速度、重量和载重能力的数据元素。然而，一个 `Vehicle` 具有活跃属性——即行为——以及启动和停止的能力。这些活跃属性通过与其车辆数据相关的方法来描述。这些方法与数据元素一样，都是 `Vehicle` 类不可或的一部分。

# 定义静态方法

例如，你可以用一种稍微更好的方式来重写上一节中的程序：

```cs
// StudentClassWithMethods -- 展示如何将对
// 类数据进行操作的方法放在类内部。类
// 对它自己的数据以及对该数据的的任何操作负责。
// using System;
namespace StudentClassWithMethods
{
    // 现在 OutputName 和 SetName 方法是
    // Student 类的成员，而不是 Program 类。
    public class Student
    {
        public string name;
        // OutputName -- 输出学生的姓名。
        public static void OutputName(Student student)
        {
            Console.WriteLine("Student's name is ({0})", student.name);
        }

        // SetName -- 修改对象的名称。
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
            // 通过直接访问设置名称。
            Console.WriteLine("The first time:");
            student.name = "Madeleine";
        }
    }
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_274_0.png)

# 250 定义方法

```cs
Student.OutputName(student); // 方法现在属于 Student。
// 使用方法修改名称。
Console.WriteLine("After being modified:");
Student.SetName(student, "Willa");
Student.OutputName(student);
// 等待用户确认。
Console.WriteLine("Press Enter to terminate...*
Console.Read();
```

除了名称之外，这个程序与上一节的 `PassObject` 相比有一个重大变化：我将 `OutputName()` 和 `SetName()` 方法放在了 `Student` 类中。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_275_0.png)

由于这个变化，`Main()` 在调用 `SetName()` 和 `OutputName()` 时必须引用 `Student` 类。这些方法现在是 `Student` 类的成员，而不是 `Main()` 所在的 `Program` 类成员。

这一步虽然很小，但意义重大。将 `OutputName()` 放在类内部可以实现更高层次的重用：任何需要显示对象的外部方法可以直接作为类的一部分找到 `OutputName()`。它不需要由每个使用 `Student` 类的程序单独编写一遍。

这种解决方案在哲学层面上也是更好的。`Program` 类不应该担心如何初始化 `Student` 对象的名称，也不应该担心如何输出重要材料。`Student` 类应该包含这些信息。对象应该自负责。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_275_1.png)

事实上，`Main()` 起初就不应该将名称初始化为 Madeline。它应该调用 `SetName()`。

在 `Student` 内部，一个成员方法可以在不显式应用类名的情况下调用另一个方法。`SetName()` 可以调用 `OutputName()` 而不需要引用类名。如果你省略了类名，C# 会确保所访问的方法位于同一个类中或该类上。

# 定义实例方法

尽管 `OutputName()` 和 `SetName()` 是静态方法，但它们也可以是非静态的，或者说是实例方法。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_275_2.png)

类的所有静态成员都是类成员，而所有非静态成员都是实例成员。这包括方法。

对象（类的实例）的非静态数据成员是通过对象而不是通过类来访问的。因此，你可以说

```cs
Student student = new Student(); // 创建一个 Student 实例。
student.name = "Madeleine"; // 通过实例访问成员。
```

C# 允许你以相同的方式调用非静态方法：

```cs
student.SetName("Madeleine");
```

下面的示例演示了这种技术：

```cs
// InvokeMethod -- 通过对象调用方法。
using System;
namespace Student
class Student
{
    // 描述学生的姓名信息
    public string firstName;
    public string lastName;
    // SetName - 保存姓名信息。（非静态）。
    public void SetName(string fName, string lName)
    {
        firstName = fName;
        lastName = lName;
    }
    // ToName -- 将学生对象转换为
    // 字符串以便显示。（非静态）。
    public string ToName()
    {
        string s = firstName + " * " + lastName;
    }
    public static void Main()
    {
        Student student = new Student();
        student.SetName("Madeleine", "Smith"); // 实例方法调用
        Console.WriteLine("Student's name is " + student.ToName());
    }
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_276_0.png)

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_276_1.png)

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_276_2.png)

*(注：由于原文代码块在某些处不完整或存在错乱，翻译时已根据上下文进行了补全和对齐)*


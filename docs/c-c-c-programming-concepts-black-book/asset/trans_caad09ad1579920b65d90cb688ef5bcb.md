
## 命名参数

当一个方法包含相当多的参数时，命名参数会很有用。在这种情况下，当我们尝试调用这个方法时，可能会忘记参数出现的顺序。因此，使用命名参数有助于记住方法中参数出现的顺序。清单 17.56 展示了一个命名参数的简单示例：

### 清单 17.56：展示命名参数示例

```csharp
using System;
class Program
{
    public static void Main()
    {
        //calculating Area normally
        Console.WriteLine(CalculateArea(100, 20));
        //calculating area using named arguments
        Console.WriteLine(CalculateArea(length:100, width:20));
        //shuffling the position of the named arguments
        Console.WriteLine(CalculateArea(width:20, length:100));
        //combining both positional and named arguments
        Console.WriteLine(CalculateArea(100, width:20));
    }
    public static int CalculateArea(int length, int width)
    {
        return (length * width);
    }
}
```

在上述程序中，我们声明了一个名为 CalculateArea 的方法，它使用对象的长度和宽度来计算面积。在 Main() 方法中，我们首先通过在准确的位置提供 length 和 width 的值来调用这个方法，这些参数被称为位置参数。然后，我们指定了参数的名称及其值，这实现了命名参数。接下来，我们再次调用同一个方法，只是打乱命名参数的位置；最后，我们通过同时提供位置参数和命名参数来调用该方法。在这四种情况下，输出将相同。

## 可选参数

当一个方法包含一些将在程序中少数位置选择性使用的参数时，就会使用可选参数。这些可选参数可以持有常量值或默认值类型，以便在未指定值时，使用默认值或常量值执行。清单 17.57 展示了一个可选参数的示例：

### 清单 17.57：展示可选参数示例

```csharp
using System;
class Employee
{
    public static void Main()
    {
        //Providing positional arguments
        Print(100, "Mr. A Roy", "Manager");
        //Using optional arguments
        Print(200, "Mr. J Sen");
    }
    public static void Print(int id, string name, string designation = "Member", long salary=10000)
    {
        Console.WriteLine("The Employee details are as follows...");
        Console.WriteLine("ID: {0}, Name: {1}, Designation:{2}", id, name, designation);
    }
}
```

在上述程序中，定义了一个名为 Print 的静态方法，它包含一个可选参数 designation，该参数被设置为默认值 Member。在 Main() 方法中，我们两次调用了该方法，一次为可选参数提供了值，一次没有提供其值。程序的输出如下：

```text
The Employee details are as follows...
ID: 100, Name: Mr. A Roy, Designation: Manager
The Employee details are as follows...
ID: 200, Name: Mr. J Sen, Designation: Member
```

现在，让我们了解 C# 中的命名空间。

## 命名空间

在某些情况下，我们需要在类中声明一个方法，而该方法的名称与 C# 框架类方法匹配，当我们在代码中引用该方法时，代码会变得有歧义。此时，编译器不知道应该调用哪个方法。为了避免这个问题，C# 程序中会使用命名空间。命名空间以这样的方式组织程序，使我们能够简单地避免命名冲突。namespace 关键字用于在 C# 程序中声明命名空间。在每个 C# 程序中使用命名空间是一种良好的做法。命名空间的另一个用途是，我们可以借助 using 关键字引用命名空间，从而将命名空间内编写的任何方法引用到另一个代码文件。

声明命名空间有三种不同的方式。第一种方式是声明命名空间的常见方式，如清单 17.58 所示：

### 清单 17.58：展示声明命名空间的常见方式

```csharp
using System;
namespace Organization
{
    class Program
    {
        public static void Main()
        {
            //Statement
        }
    }
}
```

这种声明在 namespace 关键字之后包含命名空间的名称，并且命名空间定义嵌入在类体中。

还有另一种选择，我们可以定义嵌套命名空间。这种层次结构使我们能够更高效地管理代码。在这种情况下，我们可以将更通用的名称放在层次结构的顶部，将更具体的名称放在底部。这可以最大限度地减少命名冲突的可能性。清单 17.59 展示了一个嵌套命名空间的示例：

### 清单 17.59：展示嵌套命名空间示例

```csharp
using System;
namespace Corporate
{
    namespace Organization
    {
        class Program
```

```csharp
    public Employee(int emp_ID, string emp_name)
    {
        empID = emp_ID;
        empName = emp_name;
    }
    public static void Print()
    {
        Console.WriteLine("The employee information is as follows:");
        Console.WriteLine("Employee ID: {0}", empID);
        Console.WriteLine("Employee Name: {0}", empName);
    }
    }
```

在上述程序中，我们将清单 17.49 所示代码的结构复制到了 Organization 命名空间的体中。此外，我们定义了两个类：Program 和 Employee。Employee 类包含静态成员和一个静态成员方法，该方法打印该类的静态成员。Program 类包含 Main() 方法，它借助完全限定命名空间名称调用 Employee 类的静态成员方法。在这个限定命名空间名称中，父命名空间的名称在前，并通过点运算符与子命名空间的名称分隔开。使用这种层次结构，可以引用任何类及其方法。程序的输出如下：

```text
The employee information is as follows:
Employee ID: 100
Employee Name: C. Thomas
```

如果我们不想在每次从某个命名空间引用任何类时都写出该命名空间的完全限定名称，那么可以通过 using 指令来实现这一点。我们在引用 System 命名空间时已经使用了 using 指令，System 是 C# 语言的基础类库。使用 using 指令，我们可以写出完全限定命名空间名称，并引用该命名空间中的任何类或方法。清单 17.62 实现了 using 指令来调用命名空间名称：

### 清单 17.62：使用 using 指令调用命名空间

```csharp
using System;
using Corporate.Organization;
class Program
{
    public static void Main()
    {
        Employee e = new Employee(100, "C. Thomas");
        //calling the Print() method of the Employee class using namespace
        Employee.Print();
    }
}
namespace Corporate
{
    namespace Organization
    {
        class Employee
        {
            static int empID;
            static string empName;
            public Employee(int emp_ID, string emp_name)
            {
                empID = emp_ID;
                empName = emp_name;
            }
            public static void Print()
            {
                Console.WriteLine("The employee information is as follows:");
                Console.WriteLine("Employee ID: {0}", empID);
                Console.WriteLine("Employee Name: {0}", empName);
            }
        }
    }
}
```

在上述程序中，我们将命名空间名称声明为“using Corporate.Organization”。在 Main() 方法中，我们直接调用了 Print() 方法。该程序的输出将与上一个程序相同。

有时，命名空间名称可能太长，我们希望将其缩短，这既能提高可读性，也能避免命名冲突。这可以通过使用别名来实现。清单 17.63 展示了使用别名的示例：

### 清单 17.63：使用别名指令调用命名空间

```csharp
using System;
//Defining alias namespace
using EmpNamespace = Corporate.Organization.Employee;
class Program
{
    public static void Main()
    {
        //Calling the Print() method of the Employee class using namespace
        EmpNamespace.Print();
    }
}
namespace Corporate
{
    namespace Organization
    {
        class Employee
        {
            public static void Print()
            {
                Console.WriteLine("The employee information is as follows:");
                Console.WriteLine("Employee ID: {0}", 100);
                Console.WriteLine("Employee Name: {0}", "C. Thomas");
            }
        }
    }
}
```

在上述程序中，我们首先将命名空间声明为“using EmpNamespace = Corporate.Organization.Employee”；因此，通过使用名称 EmpNamespace，我们可以直接调用 Organization.Employee 命名空间中 Employee 类内的所有静态方法。在 Program 类的 Main() 方法中，我们可以通过使用别名来调用静态方法 Print()。对于这个程序，输出与清单 17.62 相同。

现在，如果我们修改上述程序，使 Main() 方法包含两个 Print() 方法，那么带有 EmpNamespace 命名空间引用的那个方法将向控制台打印所需文本，而不带任何引用的另一个 Print() 方法将实际执行打印。清单 17.64 展示了这种有歧义操作的示例：




```
namespace DemoApplication
{
    class Program
    {
        static void Main(string[] args)
        {
            double num=30.33;
            Console.Write(num);
            Console.ReadKey();
        }
    }
}
```

- **代码解释：** double 数据类型用于声明一个名为 num 的 double 类型变量。随后，该变量被赋值为 30.33。

至于控制台，你需要包含用于在控制台上显示该数字的函数。

## 布尔类型

布尔数据类型主要用于处理 true 和 false 这类布尔值。该数据类型由 Boolean 关键字标识。让我们通过以下示例看看如何使用这种数据类型：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace DemoApplication
{
    class Program
{
    static void Main(string[] args)
    {
        Boolean status=true;
        Console.Write(status);
        Console.ReadKey();
    }
}
}
```

- **代码解释：** Boolean 数据类型专门定义了一个名为“status”的布尔变量。然后给该变量赋值为 true/false。最后，不要忘记控制台输出。

## 字符串类型

String 数据类型用于管理字符串值。该数据类型由关键字“String”标识。为了演示这种数据类型，我们将使用一个名为“message”的 String 变量：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace DemoApplication
{
    class program
    {
        static void Main(string[] args)
        {
            String message="Hello";
Console.Write(message);
Console.ReadKey();
}
}
}
```

- **代码解释：** String 数据类型用于声明一个名为 message 的字符串变量。该变量随后被赋值为“Hello”。

## 变量

变量是内存位置的名称，对变量执行的所有操作都会影响该内存位置。在 C# 中，所有变量必须在使用前声明。变量被视为程序中的基本存储单元。变量中提供的值可以在程序执行期间修改。

变量类型：

- 局部变量。
- 实例变量或非静态变量。
- 静态变量或类变量。
- 常量变量。
- 只读变量。

### 局部变量

在块、方法或构造函数内部声明的变量称为局部变量。

这些变量在进入块时创建，在退出块或函数调用返回时销毁。

这些变量的作用域仅限声明该变量的块内。这意味着只能在该块内访问这些变量。

```
// C# program to demonstrate
// the local variables
using System;
class StudentDetails
{
            // Method
    public void StudentAge()
    {
                // local variable age
        int age = 0;
        age = age + 10;
        Console.WriteLine("Student age is
: " + age);
    }
    // Main Method
    public static void Main(String[] args)
    {
            // Creating object
        StudentDetails obj = new
StudentDetails();

            // calling the function
        obj.StudentAge();
    }
}
```

- **输出：** Student age is: 10.

从上述程序可以看出，变量“age”是一个属于 `StudentAge()` 函数的局部变量。如果你尝试在 `StudentAge()` 函数之外使用变量 age，编译器将会报错：

```
// C# program to demonstrate the error
// due to using the local variable
// outside its scope
using System;
class StudentDetails {
    // Method
    public void StudentAge()
    {
        // local variable age
        int age = 0;
        age = age + 10;
    }
    // Main Method
    public static void Main(String[] args)
    {
        // using local variable age outside
        it's scope
        Console.WriteLine("Student age is
: " + age);
    }
}
```

- **错误：** 当前上下文中不存在名称“age”。

### 实例变量或非静态变量

实例变量或非静态变量是在类中声明但位于任何方法、构造函数或块之外的变量。由于实例变量在类中声明，因此这些变量在创建类的对象时创建，并在对象被销毁时移除。此外，你可以对这些变量使用访问修饰符。为了举例说明：

```
// C# program to illustrate the
// Instance variables
using System;
class Marks {
    // These variables are instance
variables.
    // These variables are in a class and
    // are not inside any function
    int engMarks;
    int mathsMarks;
    int phyMarks;
    // Main Method
    public static void Main(String[]
args)
    {

        // first object
        Marks obj1 = new Marks();
        obj1.engMarks = 90;
        obj1.mathsMarks = 80;
        obj1.phyMarks = 93;

        // second object
        Marks obj2 = new Marks();
        obj2.engMarks = 95;
        obj2.mathsMarks = 70;
        obj2.phyMarks = 90;

// displaying marks for first
object
    Console.WriteLine("Marks for first object:");
    Console.WriteLine(obj1.engMarks);
    Console.WriteLine(obj1.mathsMarks);
    Console.WriteLine(obj1.phyMarks);

    // displaying marks for second
object
    Console.WriteLine("Marks for second object:");
    Console.WriteLine(obj2.engMarks);
    Console.WriteLine(obj2.mathsMarks);
    Console.WriteLine(obj2.phyMarks);
}
}
```

- **输出：** 第一个对象的分值：
  - 90
  - 80
  - 93

第二个对象的分值：
  - 95
  - 70
  - 90

在上述程序中，变量 engMarks、mathsMarks 和 phyMarks 是基本的实例变量。如上面的示例所示，当有多个对象时，每个对象都应该拥有自己的实例变量副本。从上面的输出可以明显看出，每个对象都有自己的一份实例变量副本。

### 静态变量或类变量

静态变量或类变量是使用 static 修饰符声明的变量。这些变量的声明方式与实例变量相同，唯一的区别是静态变量在类中、任何方法构造函数或块之外使用 static 关键字。

与实例变量不同，无论创建多少对象，每个类只能有一份静态变量副本。此外，静态变量在程序执行开始时创建，并在执行结束时自动销毁。

要访问静态变量，无需创建该类的对象，直接按如下方式访问变量即可：

```
class_name.variable_name;
```

```
// C# program to illustrate
// the static variables
using System;
class Emp {
    // static variable salary
    static double salary;
    static String name = "Aks";

    // Main Method
    public static void Main(String[] args)
    {
        // accessing static variable
        // without object
Emp.salary = 100000;
Console.WriteLine(Emp.name + "'s
average salary:"
            + Emp.salary);
}
}
```

- **输出：** Aks 的平均薪资：100000

非静态变量的初始化与实例创建和构造函数调用相关，因此非静态变量也可以通过构造函数来初始化。我们不会通过构造函数来初始化静态变量，因为每次构造函数调用时，它都会用新值覆盖现有值。

## 实例变量与静态变量的区别

每个对象都有自己的实例变量副本，而无论创建多少对象，每个类只能有一份静态变量副本。

使用一个对象对实例变量所做的更改不会反映到其他对象中，因为每个对象都有自己的一份实例变量副本。对于静态变量，更改会反映到其他对象中，因为静态变量对于类的所有对象是共享的。

我们可以通过对象引用来访问实例变量，而静态变量可以直接使用类名来访问。

我们可以通过对象引用来访问实例变量，而静态变量可以直接使用类名来访问。


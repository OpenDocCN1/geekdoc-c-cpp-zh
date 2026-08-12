# # 基础速查表






## C 简介
C 语言由微软为 .NET 框架开发。C 是一种基于 C 和 C++ 完全重写的语言。它是一种通用的、面向对象的、平台无关的语言，适用于 .NET 框架工作。

## Visual Studio (VS)
Visual Studio 2019 是微软提供的免费下载软件。要创建项目，转到“文件 > 新项目”。在左侧选择 C# 控制台应用模板。在右侧选择“控制台”窗口以配置项目的名称和位置。点击“确定”，VS 将为你创建你的项目。

## Hello World（世界）
使用 C#，你将用如下简单的一行代码启动程序：

```csharp
class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello world!");
        // 这行代码被 // 注释
        /* 多行注释
           由 /* 实现 */
    }
}
```

C# 将在非调试模式下运行。你之所以不想启动开始调试 (F5)，是因为控制窗口在程序结束时会自动关闭一次。有几种方法和属性可以控制这一点。你可以更改标题栏的颜色和标题。要实现这一点，可以使用项目属性。你还可以更改解决方案名称和项目位置。

## VS 中的一些小技巧

```csharp
Code Description
public class Constructor
{
    public int MyProperty { get; set; }
}
```

ReSharper 是 Visual Studio 的插件，添加了许多代码导航和编辑功能。它能发现编码错误、运行时错误和重构机会，并向你高亮它们，提供修复建议。

## 公用语言运行时 (CLR)
作为 .NET 框架的核心组件，CLR 运行在操作系统之上并管理你的执行。当你使用 .NET 工具、编译器、调试器和 ASP 时，它们都由 CLR 使用。对于 .NET 语言，编译器将其他代码转换为中间语言，并生成一个名为程序集（exe 或 DLL）的输出文件，原生机器代码可以将该程序集转换为中间语言（通用中间语言或 IL）。当程序运行时，CLR 将这些 IL 翻译成原生机器代码。CLR 确保安全性、内存安全，并通过对每个方法的即时编译 (JIT) 来管理应用程序的执行。当 CLR 编译时，它会进行管理，执行如释放对象、内存检查和处理异常等任务。

## 变量声明与赋值
在 C# 中，你必须在使用变量之前对其进行声明。要声明变量，指定变量类型后跟其名称。你还可以使用想要让包含的数据来初始化它，并在后跟变量名。使用赋值运算符 (=) 将值赋予变量。然后变量即被定义并初始化。

## 数据类型
C# 拥有内置的类型系统。这意味着你创建的每个变量都是特定类型。

| 原生类型 | 字节 | 范围 | 系统类型 |
| :--- | :--- | :--- | :--- |
| bool | 1 | 真或否 | Boolean |
| char | 2 | 0 到 65535 | Char |
| byte | 1 | 0 到 255 | Byte |
| short | 2 | -32,768 到 32,767 | Int16 |
| int | 4 | -2,147,483,648 到 2,147,483,647 | Int32 |
| long | 8 | -9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 | Int64 |
| float | 4 | ±1.5e-45 到 ±3.4e+38 | Float |
| double | 8 | ±5.0e-324 到 ±1.7e+308 | Double |
| decimal | 16 | ±1.0e-28 到 ±7.9e+28 | Decimal |

值字面量是数据类型的定义属性。例如，如果你需要一个整数，必须使用 int 类型。如果你需要一个小数，必须使用 double 类型。

- 有符号型 (short, int, long)
- 无符号型 (byte, ushort, uint, ulong)
- 实数型 (float, double)
- 小数型
- 字符串

字符串 是一种表示字符序列的内置类型。字符串字面量包含在双引号中。前缀为 # 的字符称为插值字符串，它可以在大括号内包含变量。这允许你将变量直接嵌入字符串字面量中。

Console.WriteLine() 方法用于向控制台打印文本。例如：

```csharp
string name = "John";
Console.WriteLine("Hello {name}!");
```

另一个示例：
```csharp
string city = "New York";
Console.WriteLine("I live in {city}!");
```

## 字符
char 类型 (System.Char) 表示一个 Unicode 字符，并占用两个字节。char 字面量包含在单引号中。

```csharp
char myChar = 'A';
Console.WriteLine(myChar);
foreach (char c in myChar.ToString()) { Console.Write(c); }
```


## 转义序列
转义序列适用于字符串和字符，以及由 @ 符号创建的逐字面字符串。

@（逐字字面量）允许你通过四位十六进制代码指定任何字符。

| 字符 | 值 | 重载 |
| --- | --- | --- |
| ' | 0x0027 | |
| \" | 0x0022 | |
| \\ | 0x005c | |
| \a | 0x0007 | |
| \b | 0x0008 | |
| \t | 0x0009 | |
| \f | 0x000c | |
| \n | 0x000a | |
| \r | 0x000d | |
| \t | 0x0009 | |
| \? | 0x003f | |

逐字字面量以前缀 @ @，不支持转义字符。






# 格式化

# 结构体 (Struct)

数字分为两类：整数和浮点数。

你可以使用 `struct` 关键字定义自定义类型。struct 是一个值类型。字段可以有初始化器，并在没有构造函数的情况下进行继承。第一个成员必须有一个初始化器。

# DateTime

DateTime 是一个结构体，因此是一个值类型。

```csharp
var now = new DateTime(2000);
```

| 格式 | 模式 | 数值 | 描述 |
| --- | --- | --- | --- |
| C c | (0;C21) | $2781.29 | 货币 |
| D s | (0;D57) | 1.798E+003 | 必须是整数或浮点数 |
| F | (F2;F29) | 2781.29 | 浮点数 |
| G | (0;G28) | 2781.29 | 插入零 |
| N | (0;N4) | - | 四舍五入到最近百分比 |
| R | (0,R85) | 2.89315 | 保留所有小数点 |
| X | (X,94) | - | 转换为十六进制 |

```csharp
struct Customer {
    public string FirstName;
    public string LastName;
    public Customer(string firstName, string lastName) {
        FirstName = firstName;
        LastName = lastName;
    }
    public string GetFullName() {
        return FirstName + " " + LastName;
    }
}
Customer c1 = new Customer("John", "Doe");
Console.WriteLine(c1.GetFullName()); // John Doe
```

# TimeSpan

- 创建一个 TimeSpan 表示一个时间间隔。

```csharp
var now = new DateTime(2020, 1, 1, 12, 0, 0);
var span = new TimeSpan(2, 45, 0); // 2 小时 45 分钟
var span2 = new TimeSpan(30); // 30 秒
var future = now.Add(span);
Console.WriteLine("Future: " + future);
Console.WriteLine("Future date/time: " + future.ToString("yyyy-mm-dd hh:mm:ss"));
var past = now.Subtract(span2);
Console.WriteLine("Past: " + past);
Console.WriteLine("Past date/time: " + past.ToString("yyyy-mm-dd hh:mm:ss"));
```

- 从 DateTime 中加上或减去 TimeSpan 会返回一个 DateTime。

# 枚举类型 (Enumerated Type)

它可以直接定义为命名空间、类或结构体。

```csharp
enum Day { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday }
Day d = Day.Tuesday;
Console.WriteLine(d); // Tuesday
Console.WriteLine((int)d); // 2
d = (Day)4;
Console.WriteLine(d); // Thursday
```

- 枚举是命名常量的列表。

例如你可以有一个星期几的列表：周一、周二等，且没有任何值。你可以使用 `typeof(Day)` 和 `typeof`。

# 转换 (Conversions)

C# 可以在兼容类型的实例之间进行转换。转换总是创建一个新值，而不是修改原始值。转换可以是隐式的或显式的；显式转换需要强制类型转换。一个实用的用例是你将值从 User 类转换为另一个类时。

```csharp
int x = 10;
long y = x; // 从 32 位到 64 位的隐式转换
double z = x; // 从 32 位到 64 位浮点数的隐式转换
float f = (float)z; // 从 64 位到 32 位的显式转换
int i = (int)z; // 从 64 位到 32 位的显式转换
```

整数类型的转换是隐式的。浮点数到整数类型的转换需要显式强制转换；不会进行四舍五入。

```csharp
string s = "123";
int i = int.Parse(s); // 字符串到整数
int.TryParse(s, out int result); // 字符串到整数
Console.WriteLine(result); // 123
```

- 这里是一些隐式和显式转换的示例。

```csharp
var a = 10;
var b = a; // 隐式转换
var c = (double)a; // 显式转换
```

枚举可以作为列表。例如在 .NET 中，每个对象的可用成员是相等的：

```csharp
float f = -2.7;
object obj = f; // 装箱 (boxing)
Int32 d = obj; // 装箱
Console.WriteLine(obj.GetType() + " " + obj);
```


# Lists

列表在下面详细介绍，但这里是使用它们的方法：

```csharp
var numbers = new List<int>(1, 2, 3);
numbers.Add(new int[] {5, 6});
foreach (var num in numbers) Console.WriteLine(num + " ");
```

# Regex 类

Regex 类位于 `System.Text.RegularExpressions`。将此添加到你的项目引用或命名空间。

| 描述 | 示例 |
| --- | --- |
| 匹配一个或多个 | `abc+` |
| 匹配零或多个 | `abc*` |
| 匹配零或一个 | `abc?` |
| 任意数字 | `[0-9]` |
| 任意三个数字 | `[0-9]{3}` |

# 文件 IO

使用 `using System.IO;` 将其添加到你的项目。

```csharp
class Program {
    static void Main(string[] args) {
        File.WriteAllText(@"D:\myfile.txt", "Hello world!");
        string[] lines = File.ReadAllLines(@"D:\myfile.txt");
        foreach (var line in lines) {
            Console.WriteLine(line);
        }
        File.AppendAllText(@"D:\myfile.txt", "\n line!");
        File.Delete(@"D:\myfile.txt");
    }
}
```

# 调试 (Debugging)

要调试代码，你可以点击行号并按 F5 设置断点。然后你可以使用 F10 单步执行。将鼠标悬停在变量上可以查看状态。如果一切正常，再次按 F5 继续执行。你也可以使用 Ctrl+Shift+F5 重新启动调试。完成后再次按 F5 停止执行。完成后你的断点将被移除。

- Windows
- 断点

# 比较运算符 (Comparison Operators)

比较运算符比较两个值并返回 true 或 false：

| 语法 | 示例 |
| --- | --- |
| == | `if (x == 10) // 等于` |
| != | `if (x != 10) // 不等于` |
| > | `if (x > 10) // 大于` |
| < | `if (x < 10) // 小于` |
| >= | `if (x >= 10) // 大于等于` |
| <= | `if (x <= 10) // 小于等于` |

# 条件语句

编写一个返回 true 或 false 的方法很好，然后调用它：

| 语法 | 示例 |
| --- | --- |
| if (condition) | `if (condition) { ... }` |
| else | `else { ... }` |
| else if (condition) | `else if (condition) { ... }` |
| switch | |

```csharp
if (x == 10) {
   x = 20;
} else {
   x = 30;
}
```

编写一个返回 true 或 false 的方法很好。例如，如果你想检查列表是否包含项，你可以写一个在包含项时返回 true 的方法。然而，这可能不是你所预期的。考虑边缘情况（Edge Cases）是非常重要的，它们是不常见的，是快乐路径（Happy Path）的相反面。

# NuGet 包管理器

NuGet 用于 .NET。NuGet 客户端管理器提供了对包仓库的访问以便消费这些包。NuGet 包使用 NuGet 包管理器或 Package Console 安装到你的 Visual Studio 项目中。一个有趣的功能是 NuGet 包管理器，它允许你打包自己的代码，但这里有一些...

# 你自己的库 (Your Own Library)

使用 Visual Studio 2017 创建类库，创建一个新项目 -> Class Library C# - Net Standard (.NET Standard) 并给它一个名称和位置。要使用它，转到 Build -> Build Solution 创建 DLL。DLL 名称将是你通过提供名称和位置让项目引用它时所需的。选择 Solution Explorer -> 右键点击 References -> Add Reference -> Browse 找到 DLL。现在你可以在程序顶部添加 using 语句。现在你应该可以访问你的库代码了：

# 循环 (Loop)

| 语法 | 示例 |
| --- | --- |
| while (condition) | `while (condition) { ... }` |
| for (condition) | `for (condition) { ... }` |
| foreach (item in collection) | `foreach (item in collection) { ... }` |

```csharp
int i = 0;
while (i < 4) {
   Console.WriteLine(i);
   i++;
}
for (int i = 0; i < 4; i++) {
   Console.WriteLine(i);
}
foreach (var item in numbers) {
   Console.WriteLine(item);
}
```

# 目录 (Directory)

| 语法 | 示例 |
| --- | --- |
| do { ... } | `do { ... } while (condition);` |
| while (condition) | `while (condition) { ... }` |

```csharp
int i = 0;
do {
   Console.WriteLine(i);
   i++;
} while (i < 4);
```






## 抽象类

### 面向对象编程 (OOP)
面向对象编程（OOP）是一种使用对象来封装代码的编程范式。类型的对象被称为类；类只是对象的模板。当我们说一个类被实例化时，意味着创建了一个对象。每个对象都包含数据和代码。在 C# 中，对象是类的实例。

抽象类不能被实例化。相反，只有子类可以被实例化。抽象类定义抽象方法，这些方法与虚成员相似，但它们不提供默认实现。实现必须由子类提供，除非该子类也是抽象类。

## 密封类

密封类不能作为任何其他类的基类。你使用 `sealed` 关键字来保护类不被继承。静态类是隐式密封的。

## DRY

DRY 代表“不要重复”（Don't Repeat Yourself）。在 OOP 中，封装被用于避免一个或两个相关的不同概念、系统到组合中：(1) 一种限制直接访问对象某些组件的语言机制；(2) 一种操作数据的语言机制（或其他函数）。在 OOP 中，开闭原则规定软件实体（类、函数等）对扩展开放，对修改关闭。

## 实例构造函数

对于类，如果你没有定义任何构造函数，编译器会自动生成一个无参数的构造函数。无参数构造函数不是自动生成的，因此你可能需要编写它。

当对象被销毁时，它的内存会被释放。内存由垃圾回收器释放。终结器通过 `new` 关键字调用。

## 类声明

```csharp
class Customer
{
    public protected int Id;
    public abstract string Name; // 继承自 object 的接口
}
```

类是一个包含数据并执行代码的数据结构。类的每个成员可以包含协调，或者可能变量的数量是局部的。在函数内部声明的局部变量是被隐藏的。在互联网上，服务是一个为客户端提供功能的程序。注意：当你有一个类（例如我们的 Customer），并且你有一个任何任意类型的对象列表时，你应该始终包含一个列表来映射每个项目。

```csharp
public class Customer
{
    public int Id;
    public string Name; // 在现实世界中这些是属性
    public Customer(int id, string name) // （与类名相同）
    {
        this.Id = id;
        this.Name = name;
    }
    public int GetCustomerId() => this.Id;
}
```

## 静态

静态方法旨在可以在不实例化它们的情况下使用。静态类可以用于组织程序可用的成员。静态方法可以访问静态成员，也可以访问类本身。静态类不能实例化。实例类不能继承自静态类。非静态类可以有静态成员，静态成员只能访问静态成员。静态成员由类的所有实例共享，且所有实例在访问静态方法时具有相同的内存位置。静态方法可以访问静态成员，但不能访问实例成员。静态成员还可以使用点运算符从类外部访问的选项，但前提是该类成员没有使用静态前缀。

## 方法

```csharp
class Program
{
    public void ShowDetails()
    {
        Console.WriteLine("Customer ID: " + Id);
        Console.WriteLine("Name: " + Name);
    }
}
```

方法是类成员的一个代码块。你可以从方法名称内部执行代码。这提供了对类成员的访问权限。

```csharp
class NotFound
{
    public void doSomething() {}
}
```

由大括号封装的一系列语句。它可能包含局部变量（用于局部计算）、控制流语句以及被称为局部函数的其他方法。

## 字段

字段属于一个类。它可以是任何类型。字段的初始化部分紧跟声明，由等号和一个求值的表达式组成。该值在编译时求值。如果没有初始化，则将其设置为默认值。

```text
[访问修饰符]
[static|virtual|new]
返回类型
方法名 (参数 ) { 体 }
```

C# 允许可选参数包含或省略 `new` 关键字。指定参数...

程序的输出第一个 Id 为 0，因为默认是 0：
Customer ID: 0
Name: 

## 属性

| 访问权限 | 描述 |
| :--- | :--- |
| public | 各处可访问 |
| private | 仅类内部可见 |
| internal | 在同一程序集可见 |
| protected | 在类及其派生类可见 |
| protected internal | 在程序集或派生类可见 |
| virtual | 可被子类重写 |
| override | 实现虚方法或抽象方法 |
| new | 隐藏基类实现 |
| abstract | 必须由子类实现 |

## 对象初始化

```csharp
Customer c = new Customer {
    Id = 1,
    Name = "John"
};
```

## 索引器

```csharp
class Words
{
    private string[] words;
    public string this[int index] {
        get { return words[index]; }
        set { words[index] = value; }
    }
}
```

索引参数可以是范围外的（任何类型）。你可以通过在字符串前使用问号来空引用地使用索引器。

```csharp
string[] words = null;
Console.WriteLine(words[0]); // NullReferenceException
```
编写索引器时，定义一个调用 `this` 的属性，使用参数名称。






## 组合 vs 继承

### 组合（又称包含）

设计类时需要小心。在使用继承时，使用继承可能会导致由于紧耦合而难以重构的层级结构。鱼和鲸都继承自 `Animal`，但它们非常不同。一种是鱼，另一种是哺乳动物。如果我们使用继承，就必须创建一个 `Fish` 类和一个 `Whale` 类。

组合是两个类之间的一种“拥有”（a-has）关系，它允许一个类包含另一个类。继承是另一种类型的关系。两者的方法都允许代码重用。然而，在组合中，对象调用被包含对象的方法而不是自己实现它们，这向被包含的对象发送了消息。

我们还可以创建一个 `WalkAndSwim` 类。使用“是”（a-is）在这里是不妥的，因为在会走路的鱼的语境下这并说得通，但我们确定所有的动物现在和将来都会走路。如果你有，也就是说你可能需要一个名为 `WalkAnimal` 的 `Animal` 子类，并重新开发你的代码。

通常，实例使用类中的字段来持有另一个类的实例，而组合取决于你的需求。需要记住两点：

```csharp
using System;
using System.Collections.Generic;

class Car {
    private readonly Engine engine;
    public Car(Engine engine) // 构造函数 {
        engine = engine;
    }
    public void Drive() {
        float speed = 0.0f;
        engine.Start("starting speed of km/h");
        speed = 50.0f;
    }
    engine.EngineStart("starting car");
    engine.Stop("car off");
}

class Truck {
    private readonly Engine engine;
    public Truck(Engine engine) // 构造函数 {
        engine = engine;
    }
    public void DriveTruck() {
        engine.Drive();
    }
}
class Vehicle // 车和卡车都有“一个引擎”
{
    public void updateStatus(string status) {
        Console.WriteLine("status: " + status);
    }
}
class Program {
    public static void main(string[] args) {
        var car = new Car(new Engine());
        var sedan = new Sedan();
        var pickup = new Truck(new Engine());
        pickup.DriveTruck();
    }
}
```

## 接口

接口类似于类，但它是成员的规范而非实现。它是一个“合约”。接口成员是抽象的。一个类可以实现多个接口，但只能继承一个类。类和结构体可以继承自自己实现了接口的对象。

在 System.Type.Value 中，接口将由实现接口的类和结构体实现。按照约定，接口名称以字母 "I" 开头。

## 方法重写与多态

方法重写允许继承方法的实现改变于基类中的方法。`virtual` 关键字用于基类的方法以及派生类中以重写它。什么是多态？多态允许我们使用具有不同类的示例作为基类。

```csharp
class BaseClass {
    public int Property { get; set; }
    public virtual void writeMessage() {}
}

class Child : BaseClass {
    public int Composition = 3;
    public override void writeMessage() {
        Console.WriteLine("Green " + Composition);
    }
}

class Display {
    public void writeAllMessages(List<BaseClass> baseclasses) {
        foreach (var item in baseclasses) {
            item.writeMessage();
        }
    }
}
```

当我们调用上面的 `writeAllMessages()` 时，我们拥有多态行为。在这里我们有一个不同对象的列表，但每个颜色都有对应的实现。红色重写了绿色的基类。注意的是基类 `BaseClass` 的列表。

```csharp
interface IInterface {
    string GetName();
}

class Person : IInterface {
    public string Name;
    public int Age;
    public string GetName() { return Name; }
    public string GetAge() { return Age.ToString(); }
}

class Student : Person {
    public string School;
    public override string GetName() { return Name + ". Student"; }
}

class Program {
    public static void main(string[] args) {
        var p = new Person { Name = "John Doe", Age = 35 };
        var s = new Student { Name = "Jane", Age = 24, School = "University" };
        // 对象会被自动
        // 转换为接口
        Console.WriteLine((IInterface)p.GetName());
        Console.WriteLine((IInterface)s.GetName());
        Console.WriteLine(p.GetType());
    }
}
```
输出：
John Doe
Jane. Student

```csharp
public static void main(string[] args) {
    var baseclasses = new List<BaseClass>();
    baseclasses.Add(new Child() { Composition = 3 });
    baseclasses.Add(new Child() { Composition = 3 });
    var display = new Display();
    display.writeAllMessages(baseclasses);
}
```
输出：
Green 3
Green 3

等待，之前的输出是：
John Doe Age: 35
Jane Smith Age: 24


### 接口与可扩展性

我们创建了一个构造函数和依赖，这意味着 `FileProcessor` 依赖于 `ConsoleLogger`。它并不关心。

```csharp
class FileProcessor {
    private readonly ILogger _logger;
    public FileProcessor(ILogger logger) {
        _logger = logger;
    }
    public void Process(string message) {
        _logger.Log(message);
    }
    public void Save(string message) {
        _logger.Log("Saving: " + message);
    }
}
```

### 接口与单元测试

为了单元测试 `JournalPost`，我们需要一个 `IEntryChecker` 接口。

```csharp
public interface IEntryChecker {
    bool Check(JournalEntry entry);
}
```

现在我们可以使用 Moq 来测试 `JournalPost`。

```csharp
[TestClass]
public class JournalPostTests {
    [TestMethod]
    public void Test_AlreadyPosted_ThrowsException() {
        var mock = new Mock<IEntryChecker>();
        var post = new JournalPost(mock.Object);
        var entry = new JournalEntry { Amount = -120.5m };
        mock.Setup(x => x.Check(It.IsAny<JournalEntry>())).Returns(true);
        Assert.ThrowsException<InvalidOperationException>(() => {
            post.Post(entry);
        });
    }

    [TestMethod]
    public void Test_NewEntry_UpdatesBalance() {
        var mock = new Mock<IEntryChecker>();
        var post = new JournalPost(mock.Object);
        var entry = new JournalEntry { Amount = 120.5m };
        mock.Setup(x => x.Check(It.IsAny<JournalEntry>())).Returns(false);
        post.Post(entry);
        mock.Verify(x => x.Check(entry), Times.Once);
    }
}
```






```csharp
// 仅用于演示，将字段与属性混合
public int x;
public string Name = "";
public Status Status { get; set; }
```

# 泛型

C# 有两种机制可以编写跨类型的可重用代码：继承和泛型。继承通过基类表示可重用性，而泛型通过一个包含“占位符”的模板表示可重用性。

我们的代码在类中有三个方法。它们是 Add()、Add() 和 AppendString()。

```csharp
using System.Collections.Generic;
public class List<T> {
```

```csharp
  public int Id { get; set; }
  public string Name { get; set; }
```

```csharp
// 使用对象初始化语法
var customer = new Customer { Name = "Alice", Status = Status.Active };
```

```csharp
public static void Main(string[] args) {
```

```csharp
  List<Customer> customers = new List<Customer>();
  customers.Add(new Customer { Name = "Alice", Status = Status.Active });
  customers.Add(new Customer { Name = "Bob", Status = Status.Inactive });
  foreach (var customer in customers) {
    Console.WriteLine(customer.Name + " : " + customer.Status);
  }
}
```

# 委托 (Delegates)

委托是一种“持有”其他方法的类型。委托是对匹配特定签的函数或方法列表的引用。当你执行委托时，它将执行用户定义的引用类型。你可以创建自己的委托类型，或者使用泛型：Func<T> 和 Action<T>。在这里我们将创建一个委托。

```csharp
public delegate void MyDelegate(string message);
```

```csharp
static void MyMethod(string message) {
  Console.WriteLine(message);
}
```

```csharp
MyDelegate del = MyMethod;
del.Invoke("Hello!");
```

# 列表 (Lists)

列表在本清单的基础部分已经创建过，但当时的示例仅是整数列表。现在我们有了一个基于自定义类结构的对象列表。

# 类 Customer

```csharp
public class Customer {
  public int Id { get; set; }
  public string Name { get; set; }
  public Status Status { get; set; }
}
```

# 类 Repository

```csharp
public class Repository {
  private List<Customer> _customers = new List<Customer>();
  public void AddCustomer(Customer customer) {
    _customers.Add(customer);
  }
  public List<Customer> GetCustomers() {
    return _customers;
  }
  public int GetCount() {
    return _customers.Count;
  }
}
```

```csharp
public static void Main(string[] args) {
  Repository repo = new Repository();
  repo.AddCustomer(new Customer { Id = 1, Name = "Alice", Status = Status.Active });
  repo.AddCustomer(new Customer { Id = 2, Name = "Bob", Status = Status.Inactive });
  Console.WriteLine("Total customers: " + repo.GetCount());
}
```

这是另一个对象列表示例，没有使用 Repository。

# 类 Program

```csharp
public class Program {
  public static void Main(string[] args) {
    List<Customer> customers = new List<Customer>();
    customers.Add(new Customer { Id = 1, Name = "Alice", Status = Status.Active });
    customers.Add(new Customer { Id = 2, Name = "Bob", Status = Status.Inactive });
    foreach (var customer in customers) {
      Console.WriteLine(customer.Name + " : " + customer.Status);
    }
    Console.WriteLine("Total customers: " + customers.Count);
  }
}
```

这是一个委托的真实示例。在这里我们创建一个多路委托委托。我们使用的在 main 方法中。我们有一个需要“处理”多个方法的对象，并且我们能够从列表中添加或删除方法。

# 类 Processor

```csharp
public class Processor {
  public event Action<string> MessageReceived;
  public void Process(string message) {
    MessageReceived?.Invoke(message);
  }
}
```

```csharp
public static void Main(string[] args) {
  Processor processor = new Processor();
  processor.MessageReceived += Method1;
  processor.MessageReceived += Method2;
  processor.Process("First message!");
  processor.MessageReceived -= Method1;
  processor.Process("Second message!");
}

static void Method1(string message) {
  Console.WriteLine("Method 1: " + message);
}
static void Method2(string message) {
  Console.WriteLine("Method 2: " + message);
}
```

# Func 和 Action

在 .NET 中，我们有 Action 和 Func 委托。它们是非泛型的。构建它们允许我们使用 Action 并引入一个新的处理器，它可以调用 MyDelegateProcessor() 并在那里移除我们的自定义委托。在 main() 程序中我们想要修改该行和代码的第一行。


beginning.com

## Function 和 Action... 续...

```csharp
public class Myclass
{
    public int My { get; set; }
    // public delegate void MyMethodHandler(Myclass subclass)
    public delegate void MyEventHandler(Myclass sender);
    public void MethodHandler(Myclass subclass)
    {
        var myclass = new Myclass("In Process method");
        myclass.My = 1;
        Invoke(myclass); // 我们想要在这里执行的方法
    }
}
```

## 匿名类型

使用对象初始化语法允许你在先定义类之前创建对象。

```csharp
var person = new { Name = "Alice", Age = 30 };
```






beginningnow.com

```csharp
public IEnumerable<Product> GetProducts() {
    return new List<Product>();
}
```

## 扩展方法

扩展方法允许你在不更改原始类型定义的情况下，为现有类型扩展新方法。扩展方法是静态类中的静态方法，该方法被添加了修饰符。第一个参数类型定义了类型。在扩展方法中，例如：

```csharp
public class Product {
  public static string ToString(this string str, string[] args) {
    if (str == null) throw new ArgumentNullException("str cannot be null");
    return string.Join(", ", new Product(Name = "One", Price = 5),
    new Product(Name = "Two", Price = 9.99),
    new Product(Name = "Three", Price = 3));
  }
}
```

关于空和空合并运算符又是什么？

```csharp
DateTime date = DateTime.Parse("2018,1,1");
DateTime result = date.GetValueOrDefault(); // 无法转换
Console.WriteLine(date);
DateTime result = date;
```

```csharp
class Program {
  static void Main(string args) {
    var products = new ProductRepository().GetProducts();
    foreach (var product in products) {
      if (product.Price > 10) {
        Console.WriteLine(product.Name);
      }
    }
  }
}
```

```csharp
// 空合并运算符：
DateTime? date = null;
if (date != null) {
  使用 ?? 运算符
} else {
  date = DateTime.GetValueOrDefault();
}
Console.WriteLine(date);
DateTime date = DateTime.Now;
date = date ?? DateTime.Now; // 如果在块
```

处理可空类型时，`DateTime.GetValueOrDefault()` 是执行此操作的首选方法。

当你折叠此委托时，你可以访问这些方法和扩展方法列表。扩展方法的一个例子是 `Where`。`Func<Product, bool>` 指向一个带有参数的方法。谓词接受一个产品。当我们将 `Func` 作为 Lambda 表达式的委托时，例如 `p => p.Price > 10`。这里是带有 LINQ 代码：

## 类

```csharp
static void Main(string args) {
  string sentence = "A very long sentence...";
  string[] words = sentence.Split(' ');
  int length = words.Length;
  var sortedSentence = string.Join(" ", words.OrderBy(w => w.Length));
  var s3 = int.Parse("53");
  Console.WriteLine(s3 + " + " + s3);
}

## LINQ

LINQ 代表语言集成查询（Language Integrated Query），并被称为 "LINQ"。它是 .NET Framework 的扩展，允许你使用 SQL 查询以更大型的方式收集数据。通过 LINQ，你可以从（对象）、对象集合、XML 文档（LINQ to XML）和数据源使用 LINQ 集合查询数据。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Data;

class Program {
  static void Main(string args) {
    int[] data = {6, 4, 15, 23, 33, 68}; // 数据源
    var numbers = data.OrderBy(n => n); // 定义排序
    foreach (var x in numbers) // 执行查询
      Console.WriteLine(x); // 输出: 4, 6, 15, 23, 33, 68
  }
}
```

现在让我们看一个更具体的例子。我们将向你展示当我们有一个名为 `Product` 的类以及 `ProductRepository` 时，不使用 LINQ 该如何做。

```csharp
public class Product {
  public string Name { get; set; }
  public float Price { get; set; }
}

class ProductRepository {
  public IEnumerable<Product> GetProducts() {
    return new List<Product> {
      // 在此处添加 products
    };
  }
}
```

LINQ 方法可以做到。。选择列表，如果只需要一个，使用 `Single()` 或 `FirstOrDefault()`。如果未找到，`Single()` 将抛出 `InvalidOperationException`。`FirstOrDefault()` 返回第一个项，这样更好。

```csharp
var products = new ProductRepository().GetProducts();
var product = products.FirstOrDefault(p => p.Price > 10); // 返回匹配
Console.WriteLine(product == null); // 返回 false
Console.WriteLine(product.Name); // 返回 "Product Name"
```

有许多过滤数据的方法。在哪里找到它们？如果只需要一个使用 `Single()`... 如果未找到，`Single()` 将抛出 `InvalidOperationException`。`FirstOrDefault()` 返回第一个。

## 可空类型

可空类型表示引用类型。值类型不能为 null，所以为了表示空，必须使用用 `?` 标记的可空类型。当你有一个值时使用可空类型很重要。

## 动态

编程语言是解释性的，而 C# 变量是在运行时而不是编译时解析的。CLR（虚拟机）编译代码 (IL)，中间中间语言 (IL) 包含了所有对象的元数据。你可以通过反射获取对象的属性，并将值转换为动态（`dynamic`）。

```csharp
string name = "John";
dynamic name = "John"; // 因为 name 是动态
Console.WriteLine(name); // 返回 20
dynamic a = 1, b = 2, c = a + b; // 变为动态
dynamic d = 9;
int i = 1;
Console.WriteLine(i); // 返回 1
```

# C# 高级速习表 (4/4)

## 异步

在同步模型中，你逐行执行，但在异步模型中（例如网络请求），你不是。.NET 4.5 (2012) 引入了新的异步模型以取代多线程和回调。使用 `async` 和 `await` 关键字。在我们的示例中，我们有一个阻塞操作（下载）的 WPF 程序。使用 `async` 和 `await` 关键字使 UI 保持响应性。`Async` 方法只有在输入是 `async` 时才会对 UI 产生影响。

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;
using System.Windows;

namespace Asynchronous {
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        private async void Button_Click(object sender, RoutedEventArgs e)
        {
            await DownloadTaskAsync("http://beginnow.com/");
            await Task.Delay(2000); // 在方法结束处等待
}
        public async Task DownloadTaskAsync(string url)
{{
             使用 Task Task. 将 将卸载到后台线程
            await Task.Run(async () =>
            {
                using (HttpClient client = new HttpClient())
                {
                    string result = await client.GetStringAsync(url);
                    MessageBox.Show(result);
                }
            });
        }
    }
}
```

我们现在修改模型。消息框立即执行。我们在这里执行其他代码。另一个消息框在阻塞操作后执行。

异常处理块可以在程序崩溃时避免意外异常。我们使用 `try catch` 块。异常处理的四个关键字是：`try`、`catch`、`finally` 和 `throw`。第一个代码示例有一个意外异常。在第二个示例中，我们处理了异常。

```csharp
public int Divide(int numerator, int denominator)
{
    try
    {
        return numerator / denominator;
    }
    catch (DivideByException ex)
    {
        MessageBox.Show("Cannot divide by zero. " + ex.Message);
    }
    catch (Exception ex)
    {
        MessageBox.Show("Unexpected error! " + ex.Message);
    }
}
```

递归是一个调用它自己的函数。你必须写一个检查条件是否满足的条件。否则，函数将无限调用自身并导致无限循环。

```csharp
public static int Factorial(int n)
{
    if (n <= 1)
    {
        return 1;
    }
    else
    {
        return n * Factorial(n - 1);
    }
}
```

```csharp
public static int CountDivisors(double number, double divisor)
{
    int count = 0;
    for (int i = 1; i <= number; i++)
    {
        if (number % divisor == 0)
        {
            count++;
        }
    }
    return count;
}
```

```csharp
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public int Subtract(int a, int b)
    {
        return a - b;
    }

    public int Multiply(int a, int b)
    {
        return a * b;
    }

    public int Divide(int a, int b)
    {
        if (b == 0)
        {
            throw new DivideByZeroException();
        }
        return a / b;
    }
}
```

多个 `catch` 块示例下：

```csharp
try
{
    var calculator = new Calculator();
    var result = calculator.Divide(10, 0);
}
catch (DivideByException ex)
{
    MessageBox.Show("Cannot divide by zero!");
}
catch (Exception ex)
{
    MessageBox.Show("Unexpected error!");
}
```


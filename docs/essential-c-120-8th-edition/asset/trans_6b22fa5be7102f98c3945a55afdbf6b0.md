

# 使用文件存储和加载

`DataStorage` 中 `Store()` 方法的实际实现涉及 `System.IO` 命名空间中的类，如列表 6.13 所示。在 `Store()` 内部，你首先实例化 `FileStream` 对象并将其与员工全名对应的文件关联。`FileMode.Create` 参数表示，如果不存在名为 `<firstname><lastname>` 的文件，则将创建一个新文件；如果文件存在，则将覆盖它。接下来，你创建一个 `StreamWriter` 类，它负责向 `FileStream` 写入内容。你使用 `WriteLine()` 方法写入数据，就像写入控制台一样。

列表 6.13：数据持久化到文件

```csharp
public class DataStorage
{
    // 将员工对象保存到文件
    // 以员工名称命名
    // 未显示错误处理
    public static void Store(Employee employee)
{
        // 使用 FirstNameLastName.dat 实例化 FileStream
        // 作为文件名。FileMode.Create 将强制
        // 创建新文件或覆盖
        // 现有的文件
        // 注意：此代码可以使用 using
        // 语句进行改进 - 这是一个我们避免使用的
        // 结构，因为它还没有引入。
        FileStream stream = new(
            employee.FirstName + employee.LastName + ".dat",
            FileMode.Create);

        // 创建 StreamWriter 对象将文本
        // 写入 FileStream
        StreamWriter writer = new(stream);

        // 写入与员工关联的所有数据
        writer.WriteLine(employee.FirstName);
        writer.WriteLine(employee.LastName);
        writer.WriteLine(employee.Salary);

        // 释放 StreamWriter 及其流
        writer.Dispose(); // 关闭流
    }
}
```

```csharp
 // ...
}
```

一旦完成写入操作，都需要关闭 `FileStream` 和 `StreamWriter`，以免它们无限期地等待垃圾回收器的运行。列表 6.13 未包含任何错误处理，因此如果抛出异常，任何 `Close()` 方法都不会被调用。
加载过程也类似（请参见列表 6.14 及其输出 6.4）。

# 列表 6.14：从文件检索数据

```csharp
using System;
// IO 命名空间
using System.IO;

public class Employee
{
    // ...
}

public class DataStorage
{
    // ...
    public static Employee Load(string firstName, string lastName)
    {
        Employee employee = new();

        // 使用 FirstNameLastName.dat 实例化 FileStream
        // 作为文件名。FileMode.Open 将打开
        // 现有文件，否则报告错误
        FileStream stream = new(firstName + lastName + ".dat", FileMode.Open);

        // 创建 StreamReader 从文件中读取文本
        StreamReader reader = new(stream);

        // 从文件中读取每一行并将其放入
        // 关联的属性中。
        employee.FirstName = reader.ReadLine() ??
        throw new InvalidOperationException("FirstName cannot be null");
        employee.LastName = reader.ReadLine() ??
        throw new InvalidOperationException("LastName cannot be null");
```

# 使用关键字 313

```csharp
employee.Salary = reader.ReadLine();
```

```csharp
// 释放 StreamReader 及其 Stream
reader.Dispose(); // 关闭流
```

```csharp
return employee;
}
public class Program {
    public static void Main() {
        Employee employee1;
        Employee employee2 = new();
        employee2.SetName("Inigo", "Montoya");
        employee2.Save();
        // 在保存后修改 employee2
        IncreaseSalary(employee2);
        // 从 employee2 的保存版本加载 employee1
        employee1 = DataStorage.Load("Inigo", "Montoya");
        Console.WriteLine(
            "${employee1.GetName()}: {employee1.Salary}");
    }
// ...}
```

# 输出 6.4

Name 已更改为 'Inigo Montoya'
Inigo Montoya:

保存过程的反向出现在列表 6.14 中，它使用了 `StreamReader` 而不是 `StreamWriter`。同样，在读取数据后，需要在 `FileStream` 和 `StreamReader` 上都调用 `Close()`。

输出 6.4 在 Inigo Montoya: 之后没有显示薪水：因为在调用 `IncreaseSalary()` 到调用 `Save()` 之间，工资尚未设置为足够生存。

# 314 第 6 章：类

注意在 `Main()` 中，我们可以从员工实例调用 `Save()`，但要加载新员工，我们调用 `DataStorage.Load()`。要加载员工，我们通常已经没有可以加载进去的员工实例，因此在 `Employee` 上的实例方法是不理想的。在 `DataStorage` 上调用 `Load` 的替代方案是在 `Employee` 中添加一个静态 `Load()` 方法（参见本章稍后的“静态成员”部分），这样就可以调用 `Employee.Load()`（使用 `Employee` 类，而不是 `Employee` 的实例）。

# 访问修饰符

在章前面的部分声明字段时，你在字段声明前加上了 `public` 关键字。`public` 是一种访问修饰符，用于标识它所修饰成员的封装级别。共有七种访问修饰符：`public`、`private`、`protected`、`internal`、`protected internal`、`private protected` 和 `file`。本节考虑前两个。

> 初学者主题

# 封装部分2：信息隐藏

除了将数据和方法封装成单个单元之外，封装还涉及隐藏细节。面向对象编程实现了这一点，控制了成员的可见范围。

在面向对象编程中，封装是一个意味着分组数据和行为的术语，但也隐藏了类内部的细节。面向对象编程实现了这一点，控制了成员的可见范围。

上一节“访问修饰符”演示了你如何使用 `private` 关键字来封装密码，防止从类外部访问。这种封装并不十分严格，例如，有时你可能需要定义一些外部类只能读取但你可以在内部更改其值的字段。或者，也许你可能允许访问向类类写入某些数据，但你可能需要对数据所做的更改进行验证。在另一种场景中，也许你可能需要即时构建数据。传统上，语言通过将字段标记为 `private` 来启用这些示例中的功能。

但请考虑一个包含密码的 `Employee` 类。应该能够调用 `Employee` 对象并使用 `Logon()` 方法验证密码。相反，不应该能够在类外部访问 `Password` 字段。为了将 `Password` 字段定义为隐藏的且从类外部不可访问，你使用 `private` 关键字作为访问修饰符，代替 `public`（参见列表 6.15）。结果是 `Password` 字段只能从 `Employee` 类进行访问，例如。

# 列表 6.15：使用私有访问修饰符

```csharp
public class Employee
{
    public string FirstName;
    public string LastName;
    public string? Salary;
    // 仅限解密密码
    // 这是不建议的
    // 未初始化；等待构造函数的解释
    private string Password;
    private bool IsAuthenticated;

    public bool Logon(string password)
    {
        if(Password == password)
        {
            Authenticated = true;
        }
        return IsAuthenticated;
    }

    public bool GetAuthenticated()
    {
        return IsAuthenticated;
    }
}
```

```csharp
// ...
public class Program
{
    public static void Main()
    {
        Employee employee = new();

        employee.FirstName = "Inigo";
        employee.LastName = "Montoya";

        // ...

        // 错误：Password 是私有的，因此无法从
        // 类外部访问
        Console.WriteLine("Password = {0}", employee.Password);
    }
    // ...
}
```

尽管此选项在列表 6.15 中没有显示，但也可以使用 `private` 访问修饰符来修饰方法。
如果在类成员上没有放置访问修饰符，则默认为 `private`。换句话说，成员默认是私有的，程序员需要显式指定该成员是 `public` 的。

# 属性

上一节“访问修饰符”演示了你如何使用 `private` 关键字来封装密码，防止从类外部访问。这种封装并不十分严格，例如，有时你可能需要定义一些外部类只能读取但你可以在内部更改其值的字段。或者，也许你可能允许访问向类写入某些数据，但你可能需要对数据所做的更改进行验证。在另一种场景中，也许你可能需要即时构建数据。传统上，语言通过将字段标记为 `private` 来启用这些示例中的功能。


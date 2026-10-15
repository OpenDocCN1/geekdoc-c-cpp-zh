

case 2:
    FirstName = arguments[2];
    break;
case 3:
    LastName = arguments[3];
    break;
}
}
public string Action;
public string Id;
public string FirstName;
public string LastName;
}

static void Main(string[] args)
{
    Commandline commandline = new CommandLine(args);

    switch (commandLine.Action)
    {
        case "new":
            // Create a new employee
            // ...
            break;
        case "update":
            // Update an existing employee's data
            // ...
            break;
        case "delete":
            // Remove an existing employee's file.
            // ...
            break;
        default:
            Console.WriteLine(
                "Employee.exe " +
                "new|update|delete <id> [firstname] [lastname]");
            break;
    }
}

此示例中的嵌套类为 Program.CommandLine。与所有类成员一样，从包含类内部不需要包含类标识符，因此可以简单地将其引用为 CommandLine。

嵌套类的一个独特特性是可以将 `private` 指定为类本身的访问修饰符。因为此类用于解析命令行并将每个参数放入单独的字段中，所以 Program.CommandLine 仅与此应用程序中的 Program 类相关。使用 private 访问修饰符定义了类的预期可访问性，并防止从类外部访问。只有在类为嵌套时才能这样做。

嵌套类中的 `this` 成员指的是嵌套类的实例，而不是包含类。嵌套类访问包含类实例的一种方式是如果包含类实例被显式传递，例如通过构造函数或方法参数。

嵌套类的另一个有趣特性是它们可以访问包含类上的任何成员，包括私有成员。但是反之则不成立：包含类无法访问嵌套类的私有成员。

嵌套类很少见。如果它们很可能在包含类型之外被引用，就不应定义它们。此外，对公共嵌套类持怀疑态度；它们表明代码可能很差，很可能令人困惑且难以发现。

## 指南

避免公开暴露的嵌套类型。唯一的例外是如果此类类型的声明不太可能发生或与高级自定义场景相关。

## 语言对比：Java—内部类

Java 不仅包含嵌套类的概念，还包含内部类的概念。内部类对应于与包含类实例相关联的对象，而不仅仅是语法关系。在 C# 中，你可以通过在外部类中包含嵌套类型的实例字段来实现相同的结构。工厂方法或构造函数也可以确保在内部类实例中设置对外部类对应实例的引用。

## 部分类

C# 2.0 中添加的另一个语言特性是 **partial classes**。部分类是编译器可以组合以形成完整类的类的一部分。虽然你可以在同一个文件中定义两个或多个部分类，但部分类的一般用途是允许将类定义拆分到多个文件。主要用于生成或修改代码的工具。有了部分类，工具就可以在与开发人员手动编码的文件不同的文件中工作。

### 定义部分类

C# 2.0 及更高版本允许通过在 `class` 之前加上上下文关键字 `partial` 来声明部分类，如清单 5.46 所示。

```
**Listing 5.46: Defining a Partial Class**

```csharp
// File: Program1.cs
partial class Program
{
}

// File: Program2.cs
partial class Program
{
}
```
```

在这种情况下，`Program` 的每个部分都放在单独的文件中，如注释所标识。

除了与代码生成器一起使用外，部分类的另一个常见用途是将任何嵌套类放入自己的文件中。这符合将每个类定义放在其自己的文件中的编码约定。例如，清单 5.47 将 `Program.CommandLine` 类放入与核心 `Program` 成员分开的文件中。

```
**Listing 5.47: Defining a Nested Class in a Separate Partial Class**

```csharp
// File: Program.cs
partial class Program
{
    static void Main(string[] args)
    {
        CommandLine commandLine = new CommandLine(args);

        switch (commandLine.Action)
```
```
{ // ... } } } }
```

```
// File: Program+CommandLine.cs
partial class Program
{
    // Define a nested class for processing the command line.
    private class CommandLine
    {
        // ...
    }
}
```

部分类不允许扩展已编译的类或其它程序集中的类。它们只是将类实现在同一程序集内的多个文件之间拆分的一种手段。

## 部分方法

从 C# 3.0 开始，语言设计者增加了部分方法的概念，扩展了 C# 2.0 的部分类概念。部分方法仅允许在部分类中使用，与部分类一样，其主要目的是适应代码生成。

考虑一个代码生成工具，它根据数据库中的 Person 表为 Person 类生成 Person.Designer.cs 文件。该工具检查表并为表中的每一列创建属性。然而，问题是工具通常无法生成可能需要的任何验证逻辑，因为该逻辑基于业务规则，而这些规则并未嵌入到数据库表定义中。为了克服这一困难，Person 类的开发人员需要添加验证逻辑。直接修改 Person.Designer.cs 是不可取的，因为如果文件被重新生成，例如为了适应数据库中的额外列，更改将会丢失。相反，Person 的代码结构需要分离，以便生成的代码出现在一个文件中，而自定义代码 包含业务规则 放在重新生成不受影响的单独文件中。如前一节所述，部分类非常适合将类拆分到多个文件中的任务，但在许多情况下，我们还需要部分方法

部分方法允许在不要求实现的情况下声明方法。然而，当可选实现包含时，它可以位于其中一个兄弟部分类定义中，很可能在单独的文件中。清单 5.48 显示了 Person 类的部分方法声明和实现。

# LISTING 5.48: Defining a Nested Class in a Separate Partial Class

```
// File: Person.Designer.cs
public partial class Person
{
    #region Extensibility Method Definitions
    partial void OnLastNameChanging(string value);
    partial void OnFirstNameChanging(string value);
    #endregion

    // ...
    public System.Guid PersonId
    {
        // ...
    }
    private System.Guid _PersonId;

    // ...
    public string LastName
    {
        get
        {
            return _LastName;
        }
        set
        {
            if ((_LastName != value))
            {
                OnLastNameChanging(value);
                _LastName = value;
            }
        }
    }
    private string _LastName;

    // ...
    public string FirstName
    {
        get
        {
            return _FirstName;
        }
        set
        {
            if ((_FirstName != value))
```

```
```csharp
{
    OnFirstNameChanging(value);
    _FirstName = value;
}
}
}
private string _FirstName;
}
```
```

```
// File: Person.cs
partial class Person
{
    partial void OnLastNameChanging(string value)
    {
        if (value == null)
        {
            throw new ArgumentNullException("value");
        }
        if(value.Trim().Length == 0)
        {
            throw new ArgumentException(
                "LastName cannot be empty.",
                "value");
        }
    }
}
```

在 Person.Designer.cs 的清单中，声明了 OnLastNameChanging() 和 OnFirstNameChanging() 方法。此外，最后名和名字属性会调用其对应的 changing 方法。即使 changing 方法的声明不包含实现，此代码也能成功编译。关键在于方法声明前面加上了上下文关键字 partial，此外包含此类方法的类也是如此。

在清单 5.48 中，只有 OnLastNameChanging() 方法被实现。在这种情况下，实现会检查建议的新 LastName 值，如果无效则抛出异常。请注意，两个位置之间 OnLastNameChanging() 的签名是匹配的。

任何部分方法必须返回 void。如果方法不返回 void 且未提供实现，那么对未实现方法的调用的预期返回值是什么？为了避免对返回值的任何无效假设，C# 设计者决定禁止返回类型不是 void 的方法。同样，部分方法上不允许使用 out 参数。如果需要返回值，可以使用 ref 参数。

![](img/25683ccec0773ba5b8794b11f2b12877_325_0.png)


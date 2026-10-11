
不出所料，赋值可以在声明所在的同一语句中发生，也可以在一个单独的语句中发生。

与到目前为止你处理的原始类型不同，没有字面方式来指定一个 `Employee`。相反，`new` 操作符向运行时提供了一条指令，用于为 `Employee` 对象分配内存，实例化对象，并返回对实例的引用。

虽然存在显式用于分配内存的操作符，但没有用于解除分配内存的操作符。相反，运行时在对象变得不可访问后的某个时间自动回收内存。`垃圾回收器`负责自动解除分配。它确定哪些对象不再被其他活动对象引用，然后解除分配这些对象的内存。结果是，没有编译时确定的程序位置来回收内存并将其还原给系统。

在这个简单的示例中，没有与 `Employee` 相关的显式数据或方法，这使得对象基本上是无用的。下一节专注于向对象添加数据。

## 入门主题

## 封装第一部分：对象将数据与方法分组

如果你收到三叠索引卡片，分别写着员工的 `firstName`（名）、`lastName`（姓）和 `salary`（薪水），除非你知道这三叠卡片的顺序一致，否则这些卡片几乎没有价值。即便如此，由于需要翻阅两叠卡片才能确定一个人的全名，处理这些数据也会相当困难。更糟糕的是，如果你掉落了一叠卡片，就再也没有办法将名字、姓氏和薪水重新关联起来。相反，你需要一叠员工卡片，每张卡片上包含每位员工的所有数据。通过这种方法，名字、姓氏和薪水将被封装在一起。

在面向对象编程语境之外，`封装`一组项目是指将这些项目封闭在一个胶囊内。类似地，面向对象编程将方法和`数据`一起封装进对象。这为类的所有`成员`（类中的数据和方法）提供了分组，使它们不再需要单独处理。你不再需要将名字、姓氏和薪水作为三个独立的参数传递给方法，而是可以通过对象调用传递一个指向员工对象的引用。一旦被调用的方法接收到对象引用，它就可以向该对象发送消息（例如，调用像 `AdjustSalary()` 这样的方法）以执行特定操作。

## 语言对比：C++—delete 运算符

C# 程序员应将 `new` 运算符视为实例化对象的调用，而不是分配内存的调用。无论是堆上分配的对象还是栈上分配的对象都支持 `new` 运算符，这强调了 `new` 关注的不是内存分配应如何进行，也不是是否需要释放内存。

因此，C# 不需要 C++ 中的 `delete` 运算符。内存的分配和释放是运行时管理的细节，这让开发人员可以更专注于领域逻辑。然而，尽管内存由运行时管理，但运行时并不管理其他资源，例如数据库连接、网络端口等。与 C++ 不同，C# 不支持`隐式确定性资源清理`（在代码中编译时定义的位置发生隐式对象销毁）。幸运的是，C# 支持通过 `using` 语句进行`显式确定性资源清理`，以及使用 `finalizers`（终结器）进行`隐式非确定性资源清理`。

## 实例字段

面向对象设计的一个关键方面是将数据分组以提供结构。本节讨论如何向 `Employee` 类添加数据。类内部存储数据的变量在面向对象术语中称为成员变量。这个术语在 C# 中很常见，但更标准的术语——也是规范中使用的术语——是 `field`（字段），它与包含类型相关联的命名存储单元。实例字段是在类级别声明的变量，用于存储与对象关联的数据。因此，关联是指字段数据类型与包含字段之间的关系。

### 声明实例字段

在清单 6.4 中，`Employee` 类已被修改以包含三个字段：`FirstName`、`LastName` 和 `Salary`。

**清单 6.4：声明字段**

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;
}
```

添加这些字段后，可以存储与每个 `Employee` 实例相关的基本数据。在此情况下，我们在字段前加上了 `public` 访问修饰符。在字段上使用 `public` 表示字段中的数据可以被 `Employee` 之外的类访问（参见本章稍后关于“访问修饰符”的部分）。

与局部变量声明一样，字段声明包含字段所引用的数据类型。此外，还可以在声明时为字段赋初始值，如清单 6.5 中 `Salary` 字段所示。

**清单 6.5：在声明时设置字段的初始值**

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary = "Not enough";
}
```

我们将关于命名和编码字段的指南推迟到本章后面介绍 C# 属性之后。简而言之，清单 6.5 *没有* 遵循通用约定。

### 访问实例字段

你可以设置和获取字段内的数据。然而，字段不包含 `static` 修饰符这一事实表明它是一个实例字段。你只能从包含类的实例（即对象）访问实例字段。不能直接从类访问它（换句话说，即必须先创建一个实例）。

清单 6.6 展示了更新后的 `Program` 类及其对 `Employee` 类的利用方式，而输出 6.1 显示了结果。

**清单 6.6：访问字段**

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        Employee employee2;
        employee2 = new Employee();
        employee1.FirstName = "Inigo";
        employee1.LastName = "Montoya";
        employee1.Salary = "Too Little";
        IncreaseSalary(employee1);
        Console.WriteLine(
            "{0} {1}: {2}",
            employee1.FirstName,
            employee1.LastName,
            employee1.Salary);
        // ...
    }
    static void IncreaseSalary(Employee employee)
    {
        employee.Salary = "Enough to survive on";
    }
}
```

**输出 6.1**

```text
Inigo Montoya: Enough to survive on
```

清单 6.6 实例化了两个 `Employee` 对象，如前所述。然后，它设置每个字段，调用 `IncreaseSalary()` 来更改薪水，并显示与 `employee1` 引用的对象关联的每个字段。

请注意，你必须首先指定你正在处理哪个 `Employee` 实例。因此，在分配和访问字段时，`employee1` 变量作为前缀出现在字段名称之前。

## 实例方法

在 `Main()` 方法中的 `WriteLine()` 方法调用中格式化姓名的一种替代方案是在 `Employee` 类中提供处理格式化的方法。将功能更改为在 `Employee` 类中而不是 `Program` 的成员中，这与类的封装是一致的。为什么不将与员工全名相关的方法与包含形成该名字的数据的类分组在一起呢？

清单 6.7 演示了如何创建这样的方法。

**清单 6.7：从包含类内部访问字段**

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;
    public string GetName()
    {
        return $"{ FirstName } { LastName }";
    }
}
```

除了现在 `GetName()` 方法访问的是对象上的字段而不仅仅是局部变量外，这个方法与你在第 4 章中学到的内容没有什么特别之处。此外，方法声明未标记为 `static`。正如你将在本章稍后看到的那样，`static` 方法不能直接访问类内部的实例字段。相反，必须获取类的实例才能调用任何实例成员，无论是方法还是字段。

鉴于增加了 `GetName()` 方法，你可以更新 `Program.Main()` 以使用该方法，如清单 6.8 和输出 6.2 所示。

**清单 6.8：从包含类外部访问字段**

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        Employee employee2;
        employee2 = new Employee();
        employee1.FirstName = "Inigo";
        employee1.LastName = "Montoya";
        employee1.Salary = "Too Little";
        IncreaseSalary(employee1);
        Console.WriteLine(
            $"{ employee1.GetName() }:{ employee1.Salary }");
        // ...
    }
    // ...
}
```

**输出 6.2**

```text
Inigo Montoya: Enough to survive on
```

## 使用 this 关键字

你可以通过属于该类的实例成员，从类内部获取类的引用。在 C# 中，为了明确表示访问的字段或方法是包含类的实例成员，使用 `this` 关键字。当调用任何实例成员时，对 `this` 的使用是隐式的，它返回对象本身的实例。

例如，考虑清单 6.9 中显示的 `SetName()` 方法。（注：原文此处描述提到 `SetName`，但代码块显示的是 `GetName`，此处保留原文意译，但代码块按原文展示）

**清单 6.9：使用 this 明确标识字段的所有者**

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;
    public string GetName()
    {
        return $"{ FirstName } { LastName }";
    }
}
```

```csharp
public void SetName(
    string newFirstName, string newLastName)
{
    this.FirstName = newFirstName;
    this.LastName = newLastName;
}
```

此示例使用关键字 `this` 来表明字段 `FirstName` 和 `LastName` 是类的实例成员。

尽管 `this` 关键字可以加在任何对本地类成员的引用之前，但一般准则是，当没有额外价值时，不要使代码杂乱。因此，除非必要，否则应避免使用 `this` 关键字。本章后面的列表 6.12 是存在这种必要性的少数情况之一。然而，列表 6.9 和 6.10 并不是好的例子。在列表 6.9 中，可以完全去掉 `this` 而不改变代码的含义。而在列表 6.10（下面介绍）中，通过更改字段的命名约定，我们可以避免局部变量和字段之间的任何歧义。

## 初学者话题

### 依靠编码风格来避免歧义

在 `SetName()` 方法中，你不需要使用 `this` 关键字，因为 `FirstName` 显然与 `newFirstName` 不同。但假设，你并不将参数称为“newFirstName”，而是将其称为“FirstName”（使用 PascalCase），如列表 6.10 所示。

**列表 6.10：使用 this 来避免歧义**

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;
    public string GetName()
    {
        return $"{ FirstName } { LastName }";
    }
    // 注意：参数名称使用 PascalCase
    public void SetName(string FirstName, string LastName)
    {
        this.FirstName = FirstName;
        this.LastName = LastName;
    }
}
```

在此示例中，如果不明确指示 `Employee` 对象拥有该变量，就不可能引用 `FirstName` 字段。`this` 的作用就像 `Program.Main()` 方法中使用的 `employee1` 变量前缀（参见列表 6.8）；它将该引用标识为调用 `SetName()` 的那个引用。

列表 6.10 并不遵循 C# 命名约定，该约定要求参数像局部变量一样声明，使用 `camelCase`。这可能导致微妙的 bug，因为将 `FirstName`（意图指代字段）赋给 `FirstName`（参数）会导致代码仍然可以编译甚至运行。为了避免这个问题，为参数和局部变量使用与字段不同的命名约定是一种良好的实践。我们稍后在本章中演示了其中一种约定。

### 语言对比：Visual Basic——使用 Me 访问类实例

C# 关键字 `this` 等同于 Visual Basic 关键字 `Me`。

在列表 6.9 和 6.10 中，`GetName()` 方法中没有使用 `this` 关键字——它是可选的。但是，如果存在与字段同名的局部变量或参数（参见列表 6.10 中的 `SetName()` 方法），省略 `this` 将导致访问局部变量/参数，而意图是访问字段；在这种场景下，必须使用 `this`。

你还可以使用关键字 `this` 来显式访问类的方法。例如，在 `SetName()` 方法内，`this.GetName()` 是允许的，这允许你打印出新分配的名称（参见列表 6.11 和输出 6.3）。

### 列表 6.11：使用 this 与方法

```csharp
class Employee
{
    // ...
    public string GetName()
    {
        return $"{ FirstName } { LastName }";
    }
    public void SetName(string newFirstName, string newLastName)
    {
        this.FirstName = newFirstName;
        this.LastName = newLastName;
        Console.WriteLine(
            $"Name changed to '{ this.GetName() }'");
    }
}
class Program
{
    static void Main()
    {
        Employee employee = new Employee();
        employee.SetName("Inigo", "Montoya");
        // ...
    }
    // ...
}
```

**输出 6.3**

> Name changed to 'Inigo Montoya'

有时可能需要使用 `this` 来传递对当前执行对象的引用。考虑列表 6.12 中的 `Save()` 方法。

### 列表 6.12：在方法调用中传递 this

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;
    public void Save()
    {
        DataStorage.Store(this);
    }
}
class DataStorage
{
    // 将 employee 对象保存到以 Employee 名称命名的文件
    public static void Store(Employee employee)
    { // ...
    }
}
```

列表 6.12 中的 `Save()` 方法调用 `DataStorage` 类中的一个方法，称为 `Store()`。然而，需要向 `Store()` 方法传递需要持久化的 `Employee` 对象。这是通过关键字 `this` 完成的，它传递了调用 `Save()` 的 `Employee` 对象实例。

## 使用文件进行存储和加载

`DataStorage` 内部 `Store()` 方法的实际实现涉及 `System.IO` 命名空间中的类，如列表 6.13 所示。在 `Store()` 中，你首先实例化一个 `FileStream` 对象，并将其与对应于员工全名的文件相关联。`FileMode.Create` 参数表示你希望创建新文件，如果不存在名为 `<firstname><lastname>.dat` 的文件；如果文件已存在，它将被覆盖。接下来，你创建一个 `StreamWriter` 类。`StreamWriter` 类负责将文本写入 `FileStream`。你使用 `WriteLine()` 方法写入数据，就像写入控制台一样。

**列表 6.13：将数据持久化到文件**

```csharp
```

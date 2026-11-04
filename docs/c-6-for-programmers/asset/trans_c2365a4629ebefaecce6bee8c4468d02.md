
使用对象创建表达式

```csharp
new Account()
```

用于创建 Account 对象，然后将其分配给变量 myAccount。变量的类型是 Account——我们在图 4.2 中定义的类。关键字 new 创建指定类的新对象——在此例中为 Account。Account 右侧的括号是必需的（我们将在第 4.8 节讨论这些）。

### 4.2.2 调用类 Account 的 GetName 方法

Account 类的 GetName 方法返回存储在特定 Account 对象中的账户名称。图 4.1 的第 13 行

```csharp
Console.WriteLine($"Initial name is: {myAccount.GetName()}");
```

通过调用对象的 GetName 方法并使用表达式 myAccount.GetName() 来显示 myAccount 的初始名称。要为特定对象调用此方法，需要指定
- 对象的名称（myAccount）后跟
- 成员访问运算符（.），以及
- 方法名（GetName）以及
- 一组括号。

空括号表示 GetName 执行其任务不需要任何额外信息。不久后，你将看到 SetName 方法，它在执行任务时确实需要额外信息。

当 Main 调用 GetName 方法时：
- 1. 应用程序将执行从表达式 myAccount.GetName()（Main 中的第 13 行）转移到方法 GetName 的声明（我们将在第 4.3 节研究）。由于 GetName 是通过对象 myAccount 访问的，因此 GetName 知道要操作哪个对象的数据。
- 2. 接下来，方法 GetName 执行其任务——即，它将 myAccount 对象的名称返回到调用该方法的第 13 行。
- 3. Console.WriteLine 显示 GetName 返回的字符串——名称被插入到插值字符串中，替换对 GetName 的调用——然后程序继续在 Main 中第 16 行执行。

因为我们尚未在 myAccount 对象中存储名称，所以第 13 行不会显示名称。

### 4.2.3 从用户输入名称

接下来，第 16–17 行提示并输入名称。第 17 行

```csharp
string theName = Console.ReadLine(); // read a line of text
```

用户输入直到按下 *Enter* 时输入的换行符——换行符将被丢弃。按下 *Enter* 还会将输出光标定位到控制台窗口下一行的开头，因此程序的下一个输出将从用户输入的下一行开始。

### 4.2.4 调用类 Account 的 SetName 方法

Account 类的 SetName 方法将（*sets*）账户名称存储在特定 Account 对象中。第 18 行

```csharp
myAccount.SetName(theName); // put theName in the myAccount object
```

调用 myAccount 的 SetName 方法，将 theName 的值作为 SetName 的参数传递。该方法将此值存储在对象 myAccount 中——我们将在下一节看到它具体存储在哪里。

当 Main 调用 SetName 方法时：
- 1. 应用程序将程序执行从 Main 中的第 18 行转移到方法 SetName 的声明。由于方法 SetName 是通过 myAccount 对象访问的，因此 SetName “知道”要操作哪个对象。
- 2. 接下来，方法 SetName 将参数的值存储在 myAccount 对象中（我们将在第 4.3 节看到具体位置）。
- 3. 当 SetName 执行完成时，程序控制返回到调用方法 SetName 的位置（Main 中的第 18 行），然后执行继续在第 21 行。

### 显示用户输入的名称

为了证明 myAccount 现在包含用户输入的名称，第 21 行

```csharp
Console.WriteLine($"MyAccount's name is: {myAccount.GetName()}");
```

再次调用 myAccount 的 GetName 方法。正如你在程序输出的最后一行所看到的，第 17 行用户输入的名称被显示出来。当前一条语句执行完成后，达到 Main 的末尾，因此应用程序终止。

## 4.3 具有实例变量和 Set 与 Get 方法的 Account 类

图 4.1 中我们可以在不知道其实现细节的情况下创建和操作 Account 对象这一事实称为 *abstraction*。这是面向对象编程最强大的软件工程优势之一。现在我们已经看到了类 Account 的实际应用（图 4.1），在接下来的几个小节中我们将详细解释其实现。然后，我们将展示一个 UML 图，它以简洁的图形表示总结了类 Account 的 *attributes* 和 *operations*。

### 4.3.1 Account 类声明

类 Account（图 4.2）包含一个 *name* 实例变量（第 7 行），用于存储账户持有人的姓名——每个 Account 对象都有自己的一份 *name* 实例变量副本。在第 4.9 节，我们将添加一个 *balance* 实例变量来跟踪每个 Account 的当前余额。类 Account 还包含方法 SetName，程序可以调用它将名称存储在 Account 对象中，以及方法 GetName，程序可以调用它从 Account 对象获取名称。

```csharp
// Fig. 4.2: Account.cs
// A simple Account class that contains a private instance
// variable name and public methods to Set and Get name's value.

class Account
{
    private string name; // instance variable

    // method that sets the account name in the object
    public void SetName(string accountName)
    {
        name = accountName; // store the account name
    }

    // method that retrieves the account name from the object
    public string GetName()
    {
        return name; // returns name's value to this method's caller
    }
}
```

Fig. 4.2 | 一个简单的 Account 类，包含私有实例变量 name 以及用于设置和获取 name 值的公共方法。

### 4.3.2 关键字 class 和类体

类声明从第 5 行开始

```csharp
class Account
```

正如我们在第 3 章提到的，每个类声明都包含关键字 class，紧跟其后的是类的名称——在此例中为 Account。此外，每个类声明通常存储在与类同名且以 .cs 文件扩展名结尾的文件中，因此我们将类 Account 放在文件 Account.cs 中。类的主体被一对大括号括起来（图 4.2 的第 6 行和第 20 行）。

**标识符和驼峰式命名**

类、属性、方法 和 变量名 都是标识符，并且按照惯例都使用我们在第 3 章讨论的命名方案：
- 类、属性 和 方法名 以大写字母开头（即 Pascal 命名法）
- 变量名 以小写字母开头（即 camel 命名法）。

### 4.3.3 类型为 string 的实例变量 name

回顾第 1.2 节，类具有属性，由实例变量实现。类的对象在其生命周期内携带这些实例变量。每个对象都有类实例变量的自己的副本。通常，类还包含方法和属性。它们操作属于类特定对象的实例变量。

实例变量在类声明 *内部* 声明，但 *在* 类的方法和属性的主体 *之外*。第 7 行

```csharp
private string name; // instance variable
```

在方法 SetName 和 GetName 的主体 *之外* 声明了类型为 string 的实例变量 name。如果有多个 Account 对象，每个对象都有自己的 name。因为 name 是实例变量，所以它可以被类的每个方法和属性操作。类 Account 的客户端——即调用该类方法的任何其他代码（如图 4.1 中类 AccountTest 的 Main 方法）——无法访问 name 实例变量，因为它被声明为 private。然而，客户端可以访问 Account 的公共方法 SetName 和 GetName。这些方法可以访问私有实例变量 name。我们将在第 4.3.6 节讨论 private 和 public，然后在第 4.5 节更详细地讨论私有实例变量和公共 *access methods* 这种架构为何强大。

> **Good Programming Practice 4.1**
>
> 我们更喜欢先在类的主体中列出类的实例变量，这样你可以在它们在类的方法和属性中使用之前看到变量的名称和类型。你可以在类的方法（和属性）声明之外类的任何位置列出类的实例变量，但分散实例变量可能导致代码难以阅读。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_108_0.png)

**null——string 变量的默认值**

每个实例变量都有一个 *default initial value*——如果不指定实例变量的初始值，则由 C# 提供的值。因此，在程序中使用实例变量之前不需要显式初始化——除非它们必须初始化为默认值以外的其他值。类型为 string 的实例变量（像本例中的 name）的默认值是 **null**，我们将在第 7 章进一步讨论它，当我们考虑所谓的 *reference types* 时。当你使用 `Console.Write` 或 `Console.WriteLine` 显示包含值 null 的字符串变量时，屏幕上不会显示任何文本——这就是为什么在 Main（图 4.1）第 13 行第一次调用 myAccount 的 GetName 方法时没有显示名称的原因。

### 4.3.4 SetName 方法

让我们逐步查看方法 SetName 声明的代码（图 4.2，第 10–13 行）：

```csharp
public void SetName(string accountName)
{
    name = accountName; // store the account name
}
```

每个方法声明的第一行（第 10 行）是 *method header*。方法的 *return type*（出现在方法名称左侧）指定方法在执行任务后返回给其 *caller* 的数据的类型。返回类型 `void`（第 10 行）表示当方法 SetName 完成其任务时，它不会向其 *calling method* 返回（即交还）任何信息——在此例中为 Main 方法（图 4.1）的第 18 行。正如你很快会看到的，Account 方法 GetName 确实会返回一个值。

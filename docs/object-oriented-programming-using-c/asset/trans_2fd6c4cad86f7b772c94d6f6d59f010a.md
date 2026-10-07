

# 使用 C# 的面向对象编程

为了让账户真正唯一，我们可以修改 `Account` 的定义，使其包含一个账户号码，并确保该号码是唯一的，我们可以继续使用集合（set）来存储这些数据。然而，由于我们经常通过账户号码来检索账户，对于此应用程序来说，字典（dictionary）是一个更高效的集合。

字典类似于集合，但其中存储的每个项目都由一个键/值对（key/value pair）组成。

在这种情况下，键将唯一的账户号码，而值是相关的银行账户对象。

![](img/e143b38d00f95425fa4f3efca0527189_154_0.png)

在上一个示例中，我们在集合中存储了一组 `Accounts`（账户），如果我们想将它们存储在字典中，则不需要对 `Account` 类进行任何更改。

我们可以从 `Account` 类中移除重写的 `Equals()` 和 `GetHashCode()` 方法，因为字典可以包含重复的值。或者，如果我们愿意，也可以保留这些方法。

在字典中，只有键是唯一的。

# 使用 C# 的面向对象编程

`Bank` 类发生了一些重大变化，这些变化围绕创建的是字典（Dictionary）而不是集合（set）。`Bank` 类的代码所示：

```sharp
class Bank
{
    private Dictionary<int, Account> accounts;
    public Dictionary<int, Account> Accounts
    {
        get { return accounts; }
    }

    public Bank()
    {
        accounts = new Dictionary<int, Account>();
    }

    public void AddAccount(int number, Account account)
    {
        try
        {
            accounts.Add(number, account);
        }
        catch (Exception)
        {
        }
    }

    public Account GetAccount(int number)
    {
        Account a;
        accounts.TryGetValue(number, out a);
        return a;
    }
}
```

在上面的代码中，创建字典时可以看到指定了两个数据类型：首先指定了字典键的类型——在我们的案例中，我们使用简单的 `int` 作为账户号码。其次指定了值的数据类型——在我们的案例中，值是一个完整的账户对象。下面的代码段：

```sharp
private Dictionary<int, Account> accounts;
```

字典类为我们定义了两个非常有用的方法：`Add()` 和 `TryGetValue()`。

`Add()` 方法需要两个参数，“Key”（键）和“Value”（值）。因此，我们必须同时提供账户号码和要添加到字典的账户对象：

```sharp
accounts.Add(number, account);
```

# 使用 C# 的面向对象编程

# 通用集合以及如何将其序列化

请注意，如果“键”不唯一，此方法将生成异常，这种错误应该被捕获并处理……尽管在这个简单的案例中，我们决定在发生这种情况时不采取任何行动。

`TryGetValue()` 方法需要一个输入参数，即它正在查找的键，并将第二个参数的值设置为与键关联的值。在我们的示例中，它将第二个参数设置为与账户号码相关的账户。注意，如果账户号码不存在，该值将为 `null`。见下面的代码：

```sharp
accounts.TryGetValue(number, out a);
```

![](img/e143b38d00f95425fa4f3efca0527189_156_0.png)

# 使用 C# 的面向对象编程

用于测试此字典的 `Main` 方法如下：

```sharp
static void Main(string[] args)
{
    Bank b = new Bank();
    Account a;
    int an; // account number;

    a = new Account("Bert", "06/12/1963");
    b.AddAccount(1,a);

    // 创建并添加一个重复账户-这不应该起作用
    a = new Account("Bert", "06/12/1963");
    b.AddAccount(1,a);

    a = new Account("Alice", "14/08/1990");
    b.AddAccount(2,a);
    a = new Account("Claire", "1/1/2000");
    b.AddAccount(3,a);

    // 显示账户
    foreach (KeyValuePair<int, Account> kvp in b.Accounts)
    {
        an = kvp.Key;
        a = kvp.Value;
        Console.WriteLine("Account number: " + an + "\nAccount details: " + a.ToString());
    }

    Console.ReadLine();
}
```

`Main` 方法在功能上与测试集合的 `Main` 方法几乎相同。上面的代码执行了以下操作：

- 创建了几个账户，包括尝试创建一个重复。
- 显示了集合，包括账户号码。
- 检索了一个账户并进行了修改，然后再次显示了集合。

为了保持示例简短，没有防止账户无法找到的情况。

# 使用 C# 的面向对象编程

# 通用集合以及如何将其序列化

显示集合内容的以下代码值得进一步解释：

```sharp
foreach (KeyValuePair<int, Account> kvp in b.Accounts)
{
    an = kvp.Key;
    a = kvp.Value;
    Console.WriteLine("Account number: " + an + "\nAccount details: " + a.ToString());
}
```

集合中的每个对象都由键/值对组成。当我们遍历集合时，每个项目返回一个键/值对。

在上面我们了一个由键/值对组成的变量，其中键是 `int`（即账户号码），值是 `Account` 对象。我们将此对拆分为部分并存储在相应的变量（`an` 和 `a`）中。然后我们显示账户号码并对账户调用 `ToString()` 方法，使用结果显示账户详情。

![](img/e143b38d00f95425fa4f3efca0527189_158_0.png)

正如预期的，系统不允许我们创建重复的账户。

# 使用 C# 的面向对象编程

# 通用集合以及如何将其序列化

如果你查看 .NET 框架中 `System.Collections.Generic` 命名空间下的 `Dictionary` 类，你会看到许多其他用于管理字典的方法。这些包括 `Clear()`、`ContainsKey()`、`ContainsValue()` 和 `Remove()`。

# 7.11 集合的序列化与反序列化

集合、列表、集合和字典是存储对象的强大灵活的机制。它们会自动调整大小，并在添加成员、搜索成员、排序集合等方面节省了大量的编程工作。

与 .NET 框架提供的序列化/反序列化功能相结合时，它们变得更加强大。

使用传统的文件处理程序，可以将文本数据存储并从文件中检索。

序列化允许使用单个命令（一旦打开了适当的文件）存储对象。

然而，C# 对象经常包含其他对象的引用，它们创建了被称为“图”（graph）的连接网络。序列化机制遵循这些引用，并序列化被引用的对象，以及这些对象引用的对象，以此此类推。

![](img/e143b38d00f95425fa4f3efca0527189_159_0.png)

在 bookboom.com 免费免费电子书

# 使用 C# 的面向对象编程

# 通用集合以及如何将其序列化

对象所示：

![](img/e143b38d00f95425fa4f3efca0527189_160_0.png)


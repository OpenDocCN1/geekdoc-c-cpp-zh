
```c
public string Name { get; set; } // 自动实现属性
private decimal balance; // 实例变量

// 接收两个参数的 Account 构造函数
public Account(string accountName, decimal initialBalance)
{
    Name = accountName;
    Balance = initialBalance; // Balance 的 set 访问器会验证
}

// 带有验证的 Balance 属性
public decimal Balance
{
    get
    { return balance; }
    private set // 可以在类内部使用
    {
        // 验证余额是否大于 0.0；如果不是，
        // 实例变量将保留其先的值
        if (value > 0.0m) // m 表示 0.0 是 decimal 类型字面量
            balance = value;
    }
}

// 仅向余额存款（增加）有效金额的方法
public void Deposit(decimal depositAmount)
{
    if (depositAmount > 0.0m) // 如果 depositAmount 有效
        Balance = Balance + depositAmount; // 将其加到余额中
}
```

![](img/57baed2319be0bb1b5f98674846f2711_167_0.png)

## Account 类双参数构造函数

在开户时立即存款是常见操作，因此构造函数（第 10–14 行）现在接收第二个参数——类型为 `decimal` 的 `initialBalance`，它代表初始余额。第 13 行将 `initialBalance` 赋值给属性，调用 `Balance` 的 `set` 访问器，以确保在给实例余额赋值之前，参数 `initialBalance` 参数是有效的。

## Account 属性 Balance

类型为 `decimal` 的属性 `Balance`（第 17–32 行）提供了一个 `get` 访问器，允许账户的客户端获取特定 `Account` 对象的余额。该属性还提供了一个 `set` 访问器。

## 第 4 章 类、对象、方法和字符串简介

在图 4.6 中，类 `Account` 定义了一个 `Name` 属性，其 setter 简单地将隐式参数中的值赋值给类 `Account` 的实例变量。`Name` 属性并没有确保名称仅包含有效数据。

`Balance` 属性的 setter 执行了验证（也称为有效性检查）。第 27 行 (F.11) 显示 setter 的隐式值参数大于 0.0——字母 `m` 或 `M` 表示 0.0 是 `decimal` 类型字面量。如果 `value` 大于 0.0，则存储在 `value` 中的金额被赋值给实例变量（第 29 行）。否则，`balance` 保持不变——将在书中介绍更多关于错误处理的内容。

虽然在这个示例中验证了余额，但没有对名称进行验证。名称通常是“自由格式”的——有许多可以接受的名称格式。当你填写表单时，会被要求将名称限制在特定的字符数量。在第 16 章“字符串和字符：深度观察”中，你将学习如何创建字符串长度，以便通过检查字符串是否过长来验证字符串。

## 使用不同访问修饰符的 set 和 get 访问

默认情况下，属性的 `get` 和 `setter` 具有与属性相同的访问权限——例如 `public Name public`。可以使用不同的访问修饰符声明 `get` 和 `setter`。在这种情况下，其中一个访问器必须意味着比属性更严格的修饰符。我们将 `Balance` 属性的 `setter` 声明为 `private`——这表示它只能在 `Account` 类内部使用，不能由类的外部使用。这使我们能够确保任何 `Account` 对象存在，，余额只能通过 `Deposit` 方法（在练习中也通过 `Withdraw` 方法）进行修改。

![](img/57baed2319be0bb1b5f98674846f2711_168_0.png)

> 错误预防提示 4.3
>
> 数据完整性的好处并不是仅仅因为实例变量被设置为私有就自动获得的——你必须提供有效性检查并报告错误。

![](img/57baed2319be0bb1b5f98674846f2711_168_1.png)

> 错误预防提示 4.4
>
> 用于私有数据的值的 `set` 访问器应该验证预期的新值是否正确；如果不正确，setter 应该保持实例变量不变并指示错误。我们将在第 10 章演示如何抛抛异常来指示错误。

## Account Deposit 方法

公共方法 `deposit`（第 35–41 行）允许客户端代码向 `Account` 存款，增加其余额。第 35 行表示其调用者（由返回类型 `void` 指定）和：
- 方法不向调用者返回任何信息
- 接收一个参数 `depositAmount`——一个 `decimal` 值。

只有当参数值有效时（即如第 37 行所示大于 0.0），`depositAmount` 才会加到余额中。
- 需要 `m` 来表示 `decimal` 字面量。C# 默认将带有小数点的数字字面量视为 `double`，且 `double` 和 `decimal` 无法混合使用。我们将在第 5 章引入 `double` 类型。

## 4.9 带有余额的 Account 类：处理货币金额

`depositAmount` 形成一个临时和，然后被赋值给 `Balance` 属性。属性的 `setter` 随后替换实例变量之前的值（回想加法的优先级高于赋值运算符）。第 39 行在赋值的右侧使用 `Balance` 属性的 `getter`，在左侧使用 `setter` 访问器。理解赋值右侧的计算很重要，第 39 行的计算并没有修改实例——这就是为什么需要赋值。

## 软件工程观察 4.5

在实现方法时，虽然方法可以直接访问类的实例变量，但请始终使用类的属性。在第 10 章中，我们将深入探讨这一点。

## 4.9 使用带有余额的 Account 类

`AccountTest`（图 4.12）创建了两个 `Account` 对象（第 9–10 行），分别为它们初始化了 50.00 的有效余额和 -7.53 的无效余额——我们假设余额大于或等于零。`Console.WriteLine` 在第 13–16 行输出每个 `Account` 的余额。

```csharp
// 图 4.12: AccountTest.cs
// 读取和写入货币金额
using System;

class Account
{
    public string Name { get; set; } // 自动实现属性
    private decimal balance; // 实例变量

    // 接收两个参数的 Account 构造函数
    public Account(string accountName, decimal initialBalance)
    {
        Name = accountName;
        Balance = initialBalance; // Balance 的 set 访问器会验证
    }

    // 带有验证的 Balance 属性
    public decimal Balance
    {
        get
        { return balance; }
        private set // 可以在类内部使用
        {
            // 验证余额是否大于 0.0；如果不是，
            // 实例变量将保留其先的值
            if (value > 0.0m) // m 表示 0.0 是 decimal 类型字面量
                balance = value;
        }
    }

    // 仅向余额存款（增加）有效金额的方法
    public void Deposit(decimal depositAmount)
    {
        if (depositAmount > 0.0m) // 如果 depositAmount 有效
            Balance = Balance + depositAmount; // 将其加到余额中
    }
}

class AccountTest
{
    static void Main()
    {
        Account account1 = new Account("Jane Green", 50.00m);
        Account account2 = new Account("John Blue", -7.53m);

        Console.WriteLine(account1.Name + ": " + account1.Balance);
        Console.WriteLine(account2.Name + ": " + account2.Balance);

        Console.Write("enter deposit amount for account1: ");
        decimal depositAmount = decimal.Parse(Console.ReadLine());
        account1.Deposit(depositAmount);
        Console.WriteLine(account1.Name + ": " + account1.Balance);

        Console.Write("enter deposit amount for account2: ");
        decimal depositAmount = decimal.Parse(Console.ReadLine());
        account2.Deposit(depositAmount);
        Console.WriteLine(account2.Name + ": " + account2.Balance);
    }
}
```

> 图 4.12 带有 Account 对象的读取和写入货币金额。（部分 1/2）

```csharp
// 提示并输入
Console.Write("enter deposit amount for account2: ");
decimal depositAmount = decimal.Parse(Console.ReadLine());
Console.WriteLine($"{depositAmount:C} to account2");
account2.Deposit(depositAmount); // 加到余额
```

Jane Green's balance: $50.00

John Blue's balance: $0.00

enter deposit amount for account1: 25.53

Jane Green's balance: $75.53

enter deposit amount for account2: 123.45

John Blue's balance: $123.45

> 图 4.12 带有 Account 对象的读取和写入货币金额。（部分 2/2）

## 4.9 带有余额的 Account 类：处理货币金额

- 50 在美国（U.S.）显示为 $50.00，在德国显示为 50,00 e（欧元），在日本显示为 ¥50。
- 4382.51 在美国显示为 $4,382.51，在德国显示为 4,382,51 e，在日本显示为 ¥4,382。
- 1254827.40 在美国显示为 $1,254,827.40，在德国显示为 1.254,827,40 e，在日本显示为 ¥1,254,827。

图 4.13 列出了额外的格式说明符。

| 说明符 | 描述 |
| :--- | :--- |
| C c | 将字符串格式化为货币。包含带有适当货币符号（美国用 $）的数字。使用适当的分隔符分隔数字（千位、百万位等每三位一个），并默认将小数设置为两位。 |
| D d | 将字符串格式化为整数（仅限整数类型）。 |
| \N n | 使用千分位分隔符格式化字符串，默认两位小数。 |
| E e | 使用科学计数法格式化数字，默认六位小数。 |
| F f | 使用固定位数的小数格式化字符串（默认两位）。 |
| G g | 根据上下文使用带小数的小数或科学计数法正常格式化数字。如果格式项不包含格式说明符，则隐式假设格式 G。 |
| X x | 将字符串格式化为十六进制（16进制数字；我们将在在线的数字系统附录中讨论这些）。 |

**图 4.13 | 字符串格式说明符。**

## 从用户处读取小数值

第 19 行（图 4.12）提示用户为 `account1` 输入存款金额。第 20 行声明了局部变量 `depositAmount` 用于存储用户输入的每个金额。与实例变量（如 `Account` 类中的 `name` 和 `balance`）不同，局部变量（如 `Main` 中的 `depositAmount`）默认不会初始化，它们通常必须显式初始化。正如你稍后将学到的，`variableAmount` 的初始值将由用户的输入决定。

> > 常见编程错误 43
>
> 如果你尝试使用未初始局部变量的值，C 编译器将发出编译错误“Use of unassigned local variable variableName”——在错误消息中，`variableName` 将是实际变量名。这有助于避免执行时的逻辑错误。在程序中发现错误总比在执行时要好。

第 20 行通过调用 `Read` 方法获取用户输入，将用户输入的字符串传递给 `decimal` 的 `Parse` 方法，该方法返回此字符串中的小数值。第 21–22 行以货币格式显示存款金额。

## 第 4 章 类、对象、方法和字符串简介

### 存款

第 23 行调用 `account1` 的 `Deposit` 方法并提供 `depositAmount` 作为方法的参数。然后该方法将参数值加到 `Balance` 属性上（图 4.11 的第 39 行）。接着，图 4.12 中的第 26–29 行输出两个账户的余额，以显示只有 `account1` 的余额实例发生了变化。

### 读取小数并存入账户

第 32 行提示用户为 `account2` 输入一个小数。第 33 行通过调用 `Console.ReadLine` 获取用户输入并将返回值传递给 `decimal1` 的 `Parse` 方法。第 34–35 行显示存款金额。第 36 行调用 `account2` 的 `deposit` 方法并提供 `depositAmount` 作为方法的参数。然后，该方法将该值加到 `account2` 的 `Balance` 属性上。最后，第 39–42 行输出两个账户的余额，以显示只有 `account2` 的余额实例发生了变化。

### Main 中的重复代码

第 13–14、15–16、27–28、39–40 和 41–42 行的语句几乎相同——它们都输出 `Account` 的名称和余额。它们唯一的区别在于 `Account` 对象——`account1` 或 `account2`。这种重复代码在需要更新时可能会产生维护问题——如果你有六处相同的代码需要纠正错误或修改六次且不出错。练习 4.13 要求你修改图 4.12，包含一个 `Display` 方法，该方法接受 `Account` 对象作为参数并输出对象的名称和余额，且仅包含一份代码。你将用调用 `DisplayAccount` 替换 `Main` 中的重复语句。

![](img/57baed2319be0bb1b5f98674846f2711_172_0.png)

> > 软件工程观察 4.6
>
> 用包含一份代码的方法调用替换重复代码，可以减小程序的大小并提高其可维护性。

## Account 类的 UML 类图

图 4.14 中的图简洁地模拟了图 4.11 中的 `Account` 类。该图的第二个部分显示了 `string` 类型的公共属性和 `decimal` 类型的 `Balance`。`Account` 的构造函数在第三部分中建模，带有 `string` 类型的参数和 `decimal` 类型的 `initialBalance`。该类的公共 `deposit` 操作也在第三部分中建模——`Deposit` 有一个 `decimal` 类型的 `depositAmount`。方法 `Deposit` 不返回值（因为在 C# 中它返回 `void`），UML 类图没有为此操作指定类型。

| Account |
| :--- |
| +property: string |
| +property: Balance: decimal |
| <constructor>Account(name: string, initialBalance: decimal) |
| +Deposit(depositAmount: decimal) |

图 4.14 | 图 4.11 Account 类的 UML 类图。

## 4.10 总结

在本章中，你学习了面向对象编程的基本概念：类、对象、实例变量、属性和构造函数——这些将用于你创建的大多数实质性 C# 程序。学习了类的类的声明实例变量以维护该类的每个对象的数据，以及用于操作这些数据的 `Set/Get` 方法。我们演示了如何调用方法执行其任务，以及如何将信息作为参数传递给方法。现在我们展示了 C# 更优雅的属性语法，用于设置和获取访问器。我们讨论了方法的局部变量与类的实例变量之间的区别，以及实例变量是如何初始化的。

## 总结

### 4.1 引言

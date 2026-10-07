
![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_1331_0.png)

## 步骤 2：
点击 Visual Studio 栏上的 `Project`（项目），然后选择 `Add Class...`（添加类...）。将 `Add New Item` 窗口。确保项类型选择为 `Class`。将默认文件名更改为 `BankAccount.cs`，然后点击 `Add` 按钮。这将向项目添加一个名为 `BankAccount.cs` 的源代码文件。

## 步骤 3：
现在代码编辑器中应该会显示 `BankAccount.cs` 文件。通过在 `Program 10-5` 中输入第 11-36 行代码，完成 `BankAccount` 类的代码。让我们仔细查看代码：

**第 12 行：** 该语句声明了一个私有的 `_balance`。`_balance` 字段是 `Balance` 属性的备份字段（backing field）。

**第 15–18 行：** 这些行是带参数的类构造函数。当创建类的实例时，会将指定账户初始余额的参数传递给 `startingBalance` 参数。在第 17 行中，`startingBalance` 参数被赋值给 `_balance` 字段。

**第 21-24 行：** 这是 `Balance` 属性的代码。注意该属性没有 `set` 访问器，因此它是只读的。

**第 27-30 行：** 这是 `Deposit` 方法，它接受一个 `decimal` 参数并将该参数加到 `_balance` 字段。

**第 33-36 行：** 这是 `Withdraw` 方法，它接受一个 `decimal` 参数并从 `_balance` 字段中减去该参数。

## 步骤 4：
在代码编辑器中打开 `Form1.cs` 文件。在 [`Program 10-6`](http://example.com) 的第 15 和 16 行输入注释和声明。第 16 行的语句执行了以下操作：

- 它创建了一个 `BankAccount` 类的对象，并将 1000 作为参数传递给构造函数。
- 它将对象的引用赋值给名为 `account` 的字段。

由于 `account` 变量被声明为字段，因此 `Form1` 类中的所有方法都可以访问它。

## 步骤 5：
接下来为表单创建一个 Load 事件处理器。该事件处理器显示 `balanceLabel` 控件。在 `Designer` 中切换到 `Form1` 表单，双击表单上不包含控件的任何部分。这将打开代码编辑器，你将看到一个名为 `Form1_Load` 的事件处理器。通过输入 [`Program 10-6`](http://example.com) 中第 25 和 26 行所示的代码来完成事件处理器。注意第 26 行使用 `ToString` 方法将 `account` 对象的 `Balance` 属性格式化为货币，并将结果赋值给 `balanceLabel` 控件的 `Text` 属性。

## 步骤 6：
现在你为 Button 控件创建 Click 事件处理器。在 `Designer` 中切换回 `Form1` 表单并双击 `depositButton` 控件。这将打开代码编辑器，你将看到一个名为 `depositButton_Click` 的空事件处理器。通过输入 [`Program 10-6`](#) 中第 31–49 行所示的代码来完成事件处理器。

让我们来看代码：

**第 31 行：** 该语句声明了一个名为 `amount` 的本地 `decimal` 变量。它保存用户用于存款的金额。

**第 34–49 行：** 第 34 行的 `if` 语句调用 `decimal.TryParse` 将 `TextBox` 的 `Text` 属性转换为 `decimal`，并将结果存储在 `amount` 变量中。如果转换成功，将发生以下操作：

- 第 37 行调用账户的 `Deposit` 方法，并将 `amount` 作为参数传递。
- 第 40 行显示账户余额，格式化为货币。
- 第 43 行清空 `depositTextBox` 控件。

如果转换失败，第 48 行将显示错误消息。

## 步骤 7：
在 `Designer` 中切换回 `Form1` 表单并双击 `withdrawButton` 控件。这将打开代码编辑器，你将看到一个名为 `withdrawButton_Click` 的空事件处理器。通过输入 [`Program 10-6`](#) 中第 54–72 行所示的代码来完成事件处理器。让我们来看代码：

第 54 行：该语句声明了一个本地 `decimal` 变量 `amount`。它保存用户想要取取的金额。

第 57-72 行：第 57 行的 `if` 语句调用 `decimal.TryParse` 方法将 `withdrawTextBox` 控件的 `Text` 属性转换为 `decimal`，并将结果存储在 `amount` 变量中。如果转换成功，将发生以下操作：

- 第 60 行调用账户对象的 `Withdraw` 方法，并将 `amount` 作为参数传递。
- 第 63 行显示账户余额，格式化为货币。
- 第 66 行清空 `withdrawTextBox` 控件。如果转换失败，第 71 行显示错误消息。

## 步骤 8：
在 `Designer` 中切换回 `Form1` 表单并双击 `exitButton` 控件。在代码编辑器中，你将看到一个名为 `exitButton_Click` 的空事件处理器。通过输入 `Program 10-6` 中第 77-78 行的代码来完成事件处理器。

## 步骤 9：
保存项目。然后，按键盘上的 `F5` 或点击工具栏上的 `Start` 按钮来编译并运行应用程序。应用程序运行时，尝试进行存款和取款。完成后点击 `Exit`。

```csharp
using System;

namespace Account_Simulator
{
    public class BankAccount
    {
        private decimal _balance;
        public BankAccount(decimal startingBalance)
        {
            _balance = startingBalance;
        }
        public decimal Balance
        {
            return _balance;
        }
        public void Deposit(decimal amount)
        {
            _balance += amount;
        }
        public void Withdraw(decimal amount)
        {
            _balance -= amount;
        }
    }
}
```

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;
namespace Account_Simulator
{
    public partial class Form1 : Form
    {
        private BankAccount account = new BankAccount(1000);
        public Form1()
        {
            InitializeComponent();
        }
        private void Form1_Load(object sender, EventArgs e)
        {
            balanceLabel.Text = account.Balance.ToString("c");
        }
        private void depositButton_Click(object sender, EventArgs e)
        {
            decimal amount; // To hold the amount of deposit
            if (decimal.TryParse(depositTextBox.Text, out amount))
            {
                // Deposit the amount into the account.
                account.Deposit(amount);
                // Display the new balance
                balanceLabel.Text = account.Balance.ToString("c");
                // Clear the text box
                depositTextBox.Clear();
            }
            else
            {
                // Display an error message
                MessageBox.Show("Invalid amount");
            }
        }
        private void withdrawButton_Click(object sender, EventArgs e)
        {
            decimal amount; // To hold the amount of withdrawal
            if (decimal.TryParse(withdrawTextBox.Text, out amount))
            {
                // Withdraw the amount from the account.
                account.Withdraw(amount);
                // Display the new balance
                balanceLabel.Text = account.Balance.ToString("c");
                // Clear the text box
                withdrawTextBox.Clear();
            }
            else
            {
                // Display an error message
                MessageBox.Show("Invalid amount");
            }
        }
        private void exitButton_Click(object sender, EventArgs e)
        {
            // Close the form.
            this.Close();
        }
    }
}
```

有时，你需要不同的方式来执行操作。例如，你在教程 10-3 中编写的 `BankAccount` 类有一个接受 `decimal` 参数的 `Deposit` 方法。假设你正在一个应用程序中使用该类，该程序需要向方法传递一个 `double` 变量而不是 `decimal` 变量。在这个程序中，调用 `Deposit` 方法时，必须将 `double` 变量转换为 `decimal` 才能传递给该方法。如果 `Deposit` 方法既能接受 `decimal` 参数也能接受 `double` 参数就太好了。这样在传递 `double` 变量之前就不需要进行转换。这可以通过重载（overloading）来实现。

当一个方法被重载时，意味着同一个类中的多个方法具有相同的名称，但使用不同类型的参数。以下是我们在 `BankAccount` 类内部重载 `Deposit` 方法的示例：

```
// Deposit method
public void Deposit(decimal amount)
{
    _balance += amount;
}

// Deposit method
public void Deposit(double amount)
{
   _balance += (decimal)amount;
}
```

`Deposit` 方法（第 2–5 行）接受一个 `decimal` 参数，该参数被加到第 4 行的 `_balance` 字段。第二个 `Deposit` 方法（第 8–11 行）接受一个 `double` 参数。第 10 行使用转换运算符将其值转换为 `decimal`，并将结果赋值给 `_balance` 字段。

当你编写对 `Deposit` 方法的调用时，编译器必须确定你打算调用重载方法中的哪一个。将调用与正确方法匹配的过程被称为 `binding`（绑定）。当调用重载方法时，编译器使用方法的名称和参数列表来确定将调用绑定到哪种方法上。如果我们调用 `Deposit` 方法并传递一个 `decimal` 参数，则会调用带有 `decimal` 参数的方法版本。同样，如果我们调用 `Deposit` 方法并传递一个 `double` 参数，则会调用带有 `double` 参数的方法版本。

编译器使用方法的签名（`signature`）将其与同名的其他方法区分开来。方法的 `signature` 由方法名称以及方法参数的数据类型和参数种类（按值传递、`ref` 或 `out`）组成，从左到右排列。例如，这里是我们之前展示的 `Deposit` 方法的签名：

```
Deposit(decimal)
Deposit(double)
```

请注意，方法的返回类型**不是**签名的一部分。由于这个原因，你不能通过赋予它们不同的返回类型来重载方法。

# 重载构造函数

构造函数也可以被重载，这意味着一个类可以有多个构造函数。重载构造函数的规则与重载其他方法的规则相同：每个版本的构造函数必须具有不同的参数列表。只要每个构造函数都有唯一的签名，编译器就能区分它们。

以下是我们如何重载 `BankAccount` 类构造函数的示例：

```
// Constructor
public BankAccount()
{
    _balance = 0;
}

// Constructor
public BankAccount(decimal startingBalance)
{
   _balance = startingBalance;
}
```

第一个构造函数（第 2–5 行）是无参数构造函数，意味着它不接受参数。以下语句在创建 `BankAccount` 对象时调用了无参数构造函数：

```
BankAccount account = new BankAccount();
```

第二个构造函数（第 8–11 行）接受一个 `decimal` 参数。以下语句在创建 `BankAccount` 对象时调用了该构造函数：

```
BankAccount account = new BankAccount(500m);
```

以下语句也调用了第二个构造函数（第 8–11 行），因为整数值可以隐式转换为 `decimal`：

```
BankAccount account = new BankAccount(500);
```

然而，以下代码会导致错误，因为没有接受 `double` 参数的构造函数：

```
// Error
BankAccount account = new BankAccount(500.0);
```

# 默认构造函数

编写一个没有任何构造函数的类是完全允许。如果你写了一个完全没有构造函数的类，编译器会提供一个默认构造函数。默认构造函数是一个无参数构造函数（不接受参数），并用值 0 初始化对象的字段。（如果任何字段是引用类型变量，它们将被初始化为特殊值 `null`。）

# 对象初始化器语法

如果你在创建对象时就已经想要存储在对象属性中的值，可以使用对象初始化器语法（object initializer syntax）来初始化对象的属性。例如，假设我们有如下 `Circle` 类：

```
class Circle
{
    public int CenterX { get; set; }
    public int CenterY { get; set; }
}
```

我们可以使用对象初始化器语法这样初始化该类的实例：

```
Circle ring = new Circle { CenterX = 100, CenterY = 50 };
```

该语句在内存中创建了 `Circle` 类的实例。对象的名称是 `ring`。对象的 `CenterX` 属性将被初始化为值 100，`CenterY` 属性将被初始化为值 50。

让我们来看另一个例子。假设我们有如下 `Person` 类：

```
class Person
{
    public string Name { get; set; }
    public string Email { get; set; }
}
```

我们可以使用对象初始化器语法这样初始化该类的实例：

```
Person person = new Person { Name = "Janet Smith", Email = "janet@example.com" };
```

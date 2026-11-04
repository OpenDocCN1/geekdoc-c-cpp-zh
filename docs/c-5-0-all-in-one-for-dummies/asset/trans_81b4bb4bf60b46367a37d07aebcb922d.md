
## 访问器方法

如果你更仔细地查看 BankAccount 类，你会看到一些其他方法。其中一个 GetString()，返回适合向任何 Console.WriteLine() 展示的账户字符串版本。然而，如果其内容无法访问，显示 BankAccount 对象的內容可能会很困难。类应该有权决定如何显示自己。

另外，你会看到两个“getter”方法 GetBalance() 和 GetAccountNumber()，以及一个“setter”方法 SetAccountNumber()。你可能会想，为什么我要费心将像 _balance 这样的数据成员声明为 private，却提供一个公共的 GetBalance() 方法来返回其值。我有 *两个* 原因：

- ◆ GetBalance() **不提供修改 `_balance` 的方式——它仅返回其值。** 余额是只读的。用真实银行作类比，你可以随时查看余额；但你不能不使用银行的取款机制就从账户中取钱。
- ◆ GetBalance() **将类的内部格式隐藏在外部方法之外。** GetBalance() 可能通过读取收据、添加账户费用并核算银行可能想从余额中扣除的任何其他金额来进行大量计算。外部方法不知道也不关心。当然，你关心收取了哪些费用——除非换银行，否则你对此无能为力。

最后，GetBalance() 提供了一种在无需更改 BankAccount 使用者的情况下对类进行内部更改的机制。如果联邦存款保险公司（FDIC）要求你的银行以不同的方式存储存款，该要求不应改变你访问账户的方式。

## 访问控制的救援——一个示例

下面的 DoubleBankAccount 程序演示了 BankAccount 程序中的一个潜在缺陷。整个程序在我的网站上；然而，下面的列表仅显示 Main()——这是与之前的 BankAccount 程序不同的唯一部分：

![](img/80ff26f06fc9ab951e1cd4257b867366_287_0.png)

```csharp
// DoubleBankAccount -- Create a bank account using a double variable
//     to store the account balance (keep the balance in a private
//     variable to hide its implementation from the outside world).
using System;
namespace DoubleBankAccount
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Open a bank account.
            Console.WriteLine("Create a bank account object");
            BankAccount ba = new BankAccount();
            ba.InitBankAccount();
            // Make a deposit.
            double deposit = 123.454;
            Console.WriteLine("Depositing {0:C}", deposit);
            ba.Deposit(deposit);
            // Account balance.
            Console.WriteLine("Account = {0}", ba.GetString());
            // Here's the problem.
            double fractionalAddition = 0.002;
            Console.WriteLine("Adding {0:C}", fractionalAddition);
            ba.Deposit(fractionalAddition);
            // Resulting balance.
            Console.WriteLine("Resulting account = {0}", ba.GetString());
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
```

`Main()` 方法创建一个银行账户，然后存入 $123.454，这是一个包含小数分钱的金额。`Main()` 然后向余额存入一分钱的很小一部分并显示 resulting balance。

程序的输出如下所示：

```
Create a bank account object
Depositing $123.45
Account = #1001 = $123.45
Adding $0.00
Resulting account = #1001 = $123.46
Press Enter to terminate...
```

用户开始抱怨：“我就是无法将我的支票簿与银行对账单核对。” 就我个人而言，如果能凑到最近的 $100 我就很满意了，但有些人坚持他们的账户必须精确到分。显然，程序存在一个 bug。

问题当然是 $123.454 显示为 $123.45。为了避免这个问题，银行决定将存款和取款四舍五入到最近的分。存入 $123.454，银行就拿走那额外的 0.4 分。在另一边，银行放弃足够多的 0.4 金额，使得从长远来看一切都能平衡。好吧，理论上是这样。

解决舍入问题的最简单方法是將银行账户转换为 decimal 并使用 `Decimal.Round()` 方法，如此 `DecimalBankAccount` 程序所示：

![](img/80ff26f06fc9ab951e1cd4257b867366_289_0.png)

```csharp
// DecimalBankAccount -- Create a bank account using a decimal
//     variable to store the account balance.
using System;
namespace DecimalBankAccount
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Open a bank account.
            Console.WriteLine("Create a bank account object");
            BankAccount ba = new BankAccount();
            ba.InitBankAccount();
            // Make a deposit.
            double deposit = 123.454;
            Console.WriteLine("Depositing {0:C}", deposit);
            ba.Deposit(deposit);
            // Account balance.
            Console.WriteLine("Account = {0}", ba.GetString());
            // Now add in a very small amount.
            double fractionalAddition = 0.002;
            Console.WriteLine("Adding {0:C}", fractionalAddition);
            ba.Deposit(fractionalAddition);
            // Resulting balance.
            Console.WriteLine("Resulting account = {0}", ba.GetString());
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
    // BankAccount -- Define a class that represents a simple account.
    public class BankAccount
    {
        private static int _nextAccountNumber = 1000;
        private int _accountNumber;
        // Maintain the balance as a single decimal variable.
        private decimal _balance;
        // Init -- Initialize a bank account with the next
        //     account id and a balance of 0.
        public void InitBankAccount()
        {
            _accountNumber = ++_nextAccountNumber;
            _balance = 0;
        }
        // GetBalance -- Return the current balance.
        public double GetBalance()
        {
            return (double)_balance;
        }
        // AccountNumber
        public int GetAccountNumber()
        {
            return _accountNumber;
        }
        public void SetAccountNumber(int accountNumber)
        {
            this._accountNumber = accountNumber;
        }
        // Deposit -- Any positive deposit is allowed.
        public void Deposit(double amount)
        {
            if (amount > 0.0)
```

在这种情况下，唯一可能受影响的调用方法就是 Main()，但影响可能扩展到数十个访问银行账户的方法，而这些方法可能分布在数百个程序集中。 这些方法都不需要更改，因为修复在 BankAccount 类的范围内，其公共接口（其公共方法）在表面上没有改变。如果类的内部成员暴露给外部方法，就不可能实现这种解决方案。

![](img/80ff26f06fc9ab951e1cd4257b867366_291_0.png)

对类的内部更改仍然需要对其他代码进行一些重新测试，即使你不需要修改该代码。

## 定义类属性

在上一节 BankAccount 程序中演示的 GetX() 和 SetX() 方法是访问方法，或简称为访问器。虽然在理论上它们代表良好的编程习惯，但在实践中访问方法可能会变得笨拙。例如，以下代码行是必要的来将 _accountNumber 增加 1：

```
SetAccountNumber(GetAccountNumber() + 1);
```

C# 定义了一种称为属性的构造，它使得使用访问方法比将其作为方法使用更容易。下面的代码片段定义了一个读写属性 AccountNumber（它既是 getter 也是 setter）：

```csharp
public int AccountNumber          // No parentheses here.
{
    get { return _accountNumber; }  // The "read" part. Curly braces and semicolon.
    set { _accountNumber = value; } // The "write" part. 'value' is a keyword.
}
```

get 部分在属性被读取时调用，而 set 部分在写入时被调用。下面的 Balance 属性是只读的，因为只有 get 部分被定义（使用较不紧凑的记法）：

```csharp
public double Balance
{
    get
    {
        return (double)_balance;
    }
}
```

使用时，这些属性如下所示：

```csharp
BankAccount ba = new BankAccount();
// Set the account number property.
ba.AccountNumber = 1001;
// Get both properties.
Console.WriteLine("#{0} = {1:C}", ba.AccountNumber, ba.Balance);
```

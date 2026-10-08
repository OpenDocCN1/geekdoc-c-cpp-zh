

# 重载继承自的方法

正如本迷你书第 3 节所述（请在索引中查找“重载”），两个或多个方法可以具有相同的名称，只要参数的数量或类型不同（或者只要两者都不同）即可。

> ### **这是一个简单的方法重载案例**
> 给两个方法赋予相同的名称就是重载，就像“把它们搞清楚让我的我的大脑过载了”一样。

方法的参数是其扩展名称的一部分，如下例所示：

```csharp
public class MyClass {
    public static void aMethod() {
        // Do something.
    }
    public static void aMethod(int i) {
        // Do something else.
    }
    public static void aMethod(double d) {
        // Do something even different.
    }
    public static void Main(string[] args) {
        aMethod();
        aMethod(1);
        aMethod(2.0);
    }
}
```

C# 可以根据参数来区分这些方法。Main() 中的每次调用都访问了不同的方法。

返回类型不是扩展名称的一部分。你不能拥有两个仅在返回类型上不同的方法。

## 不同类，不同方法

意乎其然，方法所属的类也是其扩展名称的一部分。考虑这段代码段：

```csharp
public class MyClass {
    public static void aMethod1();
    public void aMethod2();
}
public class UrClass {
    public static void AMethod1();
    public void AMethod2();
}

public class Program {
    public static void Main(string[] args) {
        UrClass.AMethod1(); // 调用静态方法。
        // 调用 MyClass.AMethod2() 实例方法：
        MyClass mcObject = new MyClass();
        mcObject.AMethod2();
    }
}
```

类的名称是方法扩展名称的一部分。方法 MyClass.AMethod1() 与 UrClass.AMethod1() 的关系，就像 YourCar.StartOnAColdMonitoring() 和 MyCar.StartOnAColdMonitoring() 的关系一样——至少运行起来没问题。

## 躲猫猫 — 隐藏基类方法

因此，在一个类中的方法可以通过不同的参数来重载其自身类中的另一个方法。事实证明，方法也可以重载其自身基类中的方法：隐藏基类方法被称为“隐藏方法”。

假设你的银行部门让储蓄账户与其他类型的取款有所不同。为了辩论，假设从储蓄账户取款的费用 1.50 美元。

采用过程方法，你可以通过在类中设置一个标记（变量）来实现此策略，以指示该对象是储蓄账户还是简单的银行账户。然后，取款时必须检查该标记以决定是否在此收费：

```csharp
public class BankAccount {
    private decimal _balance;
    private bool _isSavingsAccount; // 标记
    // 初始化初始余额以及你正在创建的账户是否为储蓄账户。
    public BankAccount(decimal initialBalance, bool isSavingsAccount) {
        _balance = initialBalance;
        _isSavingsAccount = isSavingsAccount;
    }

    public decimal Withdraw(decimal amountToWithdraw) {
        // 如果是储蓄账户……
        if (_isSavingsAccount) {
            // ……那么扣除 1.50 美元。
            _balance -= 1.50M;
        }
        // 继续执行常规的取款代码：
        if (amountToWithdraw > _balance)
        {
            amountToWithdraw = _balance;
            _balance -= amountToWithdraw;
            return amountToWithdraw;
        }
    }
}

class MyClass {
    public void someMethod() {
        // 我想创建一个储蓄账户：
        BankAccount ba = new BankAccount(0, true);
    }
}
```

你的方法必须在构造函数中通过传递标记告诉 BankAccount 它是否是储蓄账户。构造函数保存该标记，并在 Withdraw() 方法中使用它来决定是否收取 1.50 美元。

更面向对象的方法通过在 SavingsAccount 类中使用一个具有相同名称、签名和“发色”的新方法，隐藏了基类 BankAccount 中的 Withdraw() 方法：

```csharp
// HidingWithdrawal -- 使用同名的子类
// 隐藏基类中的取款方法。
using System;
namespace HidingWithdrawal
{
    // Withdraw -- 一个非常基础的银行账户
    public class BankAccount
    {
        protected decimal _balance;
        public BankAccount(decimal initialBalance)
        {
            _balance = initialBalance;
        }
        public decimal _balance
        {
            get { return _balance; }
        }
        public decimal Withdraw(decimal amount)
        {
            // 良好的做法避免修改输入参数。
            // 修改副本
            decimal amountToWithdraw = amount;
            if (amountToWithdraw > _balance)
            {
                amountToWithdraw = _balance;
            }
            _balance -= amountToWithdraw;
            return amountToWithdraw;
        }
    }
    // SavingsAccount -- 产生利利的银行账户
    public class SavingsAccount : BankAccount
    {}
}
```

![](img/36596fb11aa4233cab0d6ddd1828_335.png)

## 重载继承自的方法

```csharp
// ...
public class SavingsAccount : BankAccount
{
    private decimal _interestRate;
    // SavingsAccount -- 产生利利的银行账户
    public SavingsAccount(decimal initialBalance, decimal interestRate) : base(initialBalance) {
        _interestRate = interestRate;
    }
    // AccumulateInterest -- 给余额增加利息
    public void AccumulateInterest() {
        _balance += _balance * _interestRate;
    }
    // Withdraw -- 调用基类方法收费
    public new decimal Withdraw(decimal amount) {
        decimal result = base.Withdraw(amount);
        result -= 1.50M;
        return result;
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        BankAccount ba = new BankAccount(100);
        SavingsAccount sa = new SavingsAccount(100, 0.05m);

        Console.WriteLine("BankAccount balance: {0}", ba._balance);
        Console.WriteLine("SavingsAccount balance: {0}", sa._balance);

        ba.Withdraw(20);
        Console.WriteLine("BankAccount balance after withdrawal: {0}", ba._balance);

        sa.Withdraw(20);
        Console.WriteLine("SavingsAccount balance after withdrawal: {0}", sa._balance);

        sa.AccumulateInterest();
        Console.WriteLine("SavingsAccount balance after interest: {0}", sa._balance);
    }
}
```

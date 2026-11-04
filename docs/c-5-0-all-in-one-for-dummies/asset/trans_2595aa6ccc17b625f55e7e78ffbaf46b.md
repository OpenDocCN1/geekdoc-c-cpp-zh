
`SavingsAccount` 类还提供两个构造函数。`SavingsAccount(interest rate)` 构造函数调用 `SavingsAccount(interest rate, initial balance)` 构造函数，并传入初始余额 0。这个最通用的构造函数使用 `base` 关键字将初始余额传递给 `BankAccount(initial balance)` 构造函数，如图 6-1 所示。

图 6-1：使用默认构造函数构造对象的路径。

![](img/80ff26f06fc9ab951e1cd4257b867366_327_0.png)

我修改了 `Main()`，去掉了那些讨厌的 `Init...()` 方法，改用构造函数取而代之。该程序的输出是一样的。

![](img/80ff26f06fc9ab951e1cd4257b867366_327_1.png)

注意 `BankAccount` 中的 `Balance` 属性，它有一个公共 getter，但有一个受保护的 setter。在这里使用 `protected` 可以防止从 `BankAccount` 外部使用，但允许在子类中使用受保护的 setter，这种情况出现在 `SavingsAccount.AccumulateInterest` 中，其中 `Balance` 位于赋值运算符的左侧。（属性和 protected 关键字见第 II 册第 5 章。你可以在本书的索引中查找它们。）

## 第 7 章：多什么态？

### 本章内容

- 决定是隐藏还是重写基类方法（选择真多！）
- 构建抽象类——你是认真的吗？
- 将方法和包含它的类声明为抽象
- 使用 `ToString`，类的名片
- 密封类，使其不能被子类化

在继承中，一个类“采用”另一个类的成员。因此，我可以创建一个 `SavingsAccount` 类，它从基类 `BankAccount` 继承数据成员（如 `account id`）和方法（如 `Deposit()`）。这很有用，但这个继承定义不足以模拟商业世界中的情况。

![](img/80ff26f06fc9ab951e1cd4257b867366_328_0.png)

如果你不太了解（或记不清）类继承，请参阅本小册子的第 6 章。

微波炉是一种烤箱，不是因为它看起来像烤箱，而是因为它执行与烤箱相同的功能。微波炉可以执行附加功能，但它至少执行基础烤箱功能——最重要的是，当我说“StartCooking”时加热我的玉米片。（我依靠 `Refrigerator` 类的对象来冷却啤酒。）我并不特别关心烤箱内部必须做什么才能实现这一点，就像我不关心它是什么类型的烤箱、是谁制造的，或者我妻子买它时是否在打折一样。（嘿，等等——我确实关心最后一点。）

从人类的角度来看，微波炉与传统烤箱之间的关系似乎没什么大不了的，但请从烤箱的角度考虑这个问题。传统烤箱内部执行的步骤与微波炉可能采取的步骤完全不同。

![](img/80ff26f06fc9ab951e1cd4257b867366_328_1.png)

继承的强大之处在于，子类不必完全按照基类方法的写法继承每一个方法。子类可以继承基类方法的本质，同时以不同方式实现细节。

### 重载继承的方法

如本小册子第 3 章所述（在索引中查找*重载*），两个或多个方法可以具有相同的名称，只要参数的数量或类型不同（或者只要两者都不同）。

![](img/80ff26f06fc9ab951e1cd4257b867366_329_0.png)

#### 这是一个方法重载的简单例子

给两个方法起相同的名称就是*重载*，正如“把它们区分清楚是在让我的大脑*超载*”一样。

方法的参数成为其扩展名称的一部分，如下例所示：

```csharp
public class MyClass
{
    public static void AMethod()
    {
        // Do something.
    }
    public static void AMethod(int i)
    {
        // Do something else.
    }
    public static void AMethod(double d)
    {
        // Do something even different.
    }
    public static void Main(string[] args)
    {
        AMethod();
        AMethod(1);
        AMethod(2.0);
    }
}
```

C# 可以通过参数区分这些方法。`Main()` 中的每个调用都访问不同的方法。

![](img/80ff26f06fc9ab951e1cd4257b867366_329_1.png)

返回类型不是扩展名称的一部分。不能有两个仅返回类型不同的方法。

#### 不同的类，不同的方法

毫不意外，方法所属的类也是其扩展名称的一部分。考虑以下代码段：

```csharp
public class MyClass
{
    public void AMethod() { }
}

public class UrClass
{
    public static void AMethod() { }
}

public class Program
{
    public static void Main(string[] args)
    {
        UrClass.AMethod();   // Call static method.
        // Invoke the MyClass.AMethod() instance method:
        MyClass myObject = new MyClass();
        myObject.AMethod();
    }
}
```

类的名称是方法扩展名称的一部分。`MyClass.AMethod()` 方法与 `UrClass.AMethod()` 的关系，大致就像 `YourClass.StartOnAColdMorning()` 与 `MyCar.StartOnAColdMorning()` 的关系——至少你的还能工作。

#### 躲猫猫——隐藏基类方法

因此，一个类中的方法可以通过具有不同的参数来重载其自身类中的另一个方法。事实证明，一个方法也可以重载其基类中的方法。重载基类方法称为*隐藏方法*。

假设你的银行采用一项政策，使储蓄账户取款不同于其他类型的取款。假设（仅为讨论起见）从储蓄账户取款需要花费 1.50 美元。

采用过程式方法，你可以在类中设置一个标志（变量）来指示对象是 `SavingsAccount` 还是普通的 `BankAccount`，从而实现该政策。然后，取款方法必须检查该标志，以决定是否需要收取 1.50 美元，如下所示：

```csharp
public class BankAccount
{
    private decimal _balance;
    private bool _isSavingsAccount;  // the flag
    // Indicate the initial balance and whether the account
    // you're creating is a savings account.
    public BankAccount(decimal initialBalance, bool isSavingsAccount)
    {
        _balance = initialBalance;
        _isSavingsAccount = isSavingsAccount;
    }
    public decimal Withdraw(decimal amountToWithdraw)
    {
        // If the account is a savings account . . .
        if (_isSavingsAccount)
        {
            // . . .then skim off $1.50.
            _balance -= 1.50M;
        }
        // Continue with the usual withdraw code:
        if (amountToWithdraw > _balance)
        {
            amountToWithdraw = _balance;
        }
        _balance -= amountToWithdraw;
        return amountToWithdraw;
    }
}

class MyClass
{
    public void SomeMethod()
    {
        // I want to create a savings account:
        BankAccount ba = new BankAccount(0, true);
    }
}
```

你的方法必须在构造函数中通过传递标志来告诉 `BankAccount` 它是否是 `SavingsAccount`。构造函数保存该标志，并在 `Withdraw()` 方法中使用它来决定是否收取额外的 1.50 美元。

更面向对象的方法是在 `SavingsAccount` 类中用同名、同身高、同发色的新方法隐藏基类 `BankAccount` 中的 `Withdraw()` 方法：

![](img/80ff26f06fc9ab951e1cd4257b867366_331_0.png)

```csharp
// HidingWithdrawal -- Hide the withdraw method in the base
// class with a method in the subclass of the same name.
// using System;
namespace HidingWithdrawal
{
    // BankAccount -- A very basic bank account
    public class BankAccount
    {
        protected decimal _balance;
        public BankAccount(decimal initialBalance)
        {
            _balance = initialBalance;
        }
        public decimal Balance
        {
            get { return _balance; }
        }
        public decimal Withdraw(decimal amount)
        {
            // Good practice means avoiding modifying an input parameter.
            // Modify a copy.
            decimal amountToWithdraw = amount;
            if (amountToWithdraw > Balance)
            {
                amountToWithdraw = Balance;
            }
            _balance -= amountToWithdraw;
            return amountToWithdraw;
        }
    }
    // SavingsAccount -- A bank account that draws interest
    public class SavingsAccount : BankAccount
    {
        public decimal _interestRate;



## 重载继承自的方法 313

在“将警告视为错误”（Treat As Errors）部分，选择“全选”。（如果某个警告让你感到困扰，可以将其列入“抑制警告”（Suppress Warnings）列表中，使其不再出现在你的视范围内。）当你将警告视为错误时，你被迫修复这些警告——就像你被迫修复真实的编译器错误一样。这种做法可以产生更好的代码。即使你没有开启“警告视为警告”（Treat Warnings）选项，也请将“警告级别”（Warning Level）保持在 4，并在每次之后选择“错误列表”（Error List）窗口。

后续示例代码中的描述符 `new` 告诉 C#，隐藏方法是有意图，而不是疏忽的结果（并且它让隐藏变得消失）：

```csharp
// 现在不支付 withdraw() 取款。
public decimal Withdraw(decimal withdrawal)
{
    // 内部没有变化...
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_338_0.png)

关键字 `new` 的这种用法与用于创建实例的同一个 `new` 无关。（C# 甚至重载了它自己！）

## 回基类

查看本章早些所示 `HidingWithal` 示例中的 `SavingsAccount.Withdraw()` 方法。该新方法对 `BankAccount.Withdraw()` 的调用包含了新关键字 `base`。

以下没有 `base` 关键字的方法版本不起作用：

```csharp
public decimal Withdraw(decimal withdrawal)
{
    decimal amountWithdrawn = Withdraw(withdrawal);
    amountWithdrawn += Withdraw(1.5);
    return amountWithdrawn;
}
```

这个调用与这个具有相同的问题：

```csharp
void fn()
{
    fn(); // 调用自己。
}
```

在 `fn` 内部调用 `fn()` 会导致不断地调用自己（递归）。同样地，在方法内部调用 `Withdraw()` 会在循环中调用自己，追逐自己的尾巴，直到程序最终崩溃。

有时，你需要指示 C# `SavingsAccount.Withdraw()` 内部的调用是为了调用基类 `BankAccount` 方法。一种方法是在调用之前将 `this` 引用强制转换为 `BankAccount` 类的对象：

## 314 多态

这种解决方案是有效的：调用 `ba.Withdraw()` 现在调用的是 `BankAccount` 方法，正如预期的那样。这种方法的问题是对 `BankAccount` 的显式引用。程序未来的更改可能会重新排列继承层次结构，使得 `SavingsAccount` 不再继承自 `BankAccount`。这种重排会以一种未来程序员可能无法轻易发现的方式破坏此方法（老实，我永远无法找到那种 bug）。

你需要一种方法来告诉 C# 调用层次结构中紧邻上面的 `Withdraw()` 方法，而无需指明它的名称。那应该是 `SavingsAccount` 扩展的类。C# 为此目的提供了关键字。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_339_0.png)

这个关键字 `base` 与构造函数向其基类构造函数传递参数时使用的的是同一个。

以下代码块中的 C# `base` 代码是这种形式，因为无论该类是什么，它都会自动被强制转换为基类：

```csharp
// Withdraw -- 你可以提取余额范围内的任何金额； // 返回提取的金额。
new public decimal Withdraw(decimal withdrawal)

// 扣除上面的 $1.50。
base.Withdraw(1.50);
// 现在你可以从剩余部分中提取。
return base.Withdraw(withdrawal);
}
```

调用 `base.Withdraw()` 现在调用 `BankAccount.Withdraw()` 方法，避免了递归的“调用自己”的问题。此外，这种解决方案在继承层次结构被更改时也不会破坏。

## 多态

你可以在基类中重载方法，但这种方法是基于基类在子类中的同名方法。正如 `所，，，是是预期的，BankAccount调用 `BankAccount` 。

                        ，取决于取决于你的期的输出：
   ```
   BankAccount  100.00
   Savings  100000
   



这种在运行时运行时调用的能力被称为：
   - 多态（Polymorphism）
   - 晚绑定（Late binding）

   这种 `idingidingal` 程序显示如下：
   ```csharp
   // 隐藏方法
   public class SavingsAccount

       
       // ...
               virtual decimal Withdraw(decimal withdrawal)
   
       public new decimal Withdraw(decimal withdrawal)
   {
           // ...
       }
   }
   ```

   这种 `Hidingal` 程序显示如下：
   ```csharp
   // 隐藏方法
   public class BankAccount
   
       // ...
       public virtual decimal Withdraw(decimal withdrawal)
   {
           // ...
       }
   }
   ```

   如果你使用 `override` 关键字，你将：
   ```csharp
   public override decimal Withdraw(decimal withdrawal)
   {
       // ...
   }
   ```

   如果你使用 `new` 关键字，你将：
   ```csharp
   public new decimal Withdraw(decimal withdrawal)
   {
       // ...
   }
   ```

   使用 `override` 关键字将允许你实现多态，而使用 `new` 关键字将隐藏基类方法。


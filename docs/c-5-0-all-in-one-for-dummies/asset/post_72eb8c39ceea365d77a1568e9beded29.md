
The `SavingsAccount` class also provides two constructors. The `SavingsAccount(interest rate)` constructor invokes the `SavingsAccount(interest rate, initial balance)` constructor, passing an initial balance of 0. This most general constructor passes the initial balance to the `BankAccount(initial balance)` constructor using the `base` keyword, as shown in Figure 6-1.

Figure 6-1: The path for constructing an object using the default constructor.

![](img/80ff26f06fc9ab951e1cd4257b867366_327_0.png)

I've modified `Main()` to get rid of those infernal `Init...()` methods and replace them with constructors instead. The output from this program is the same.

![](img/80ff26f06fc9ab951e1cd4257b867366_327_1.png)

Notice the `Balance` property in `BankAccount`, which has a public getter but a protected setter. Using `protected` here prevents use from outside of `BankAccount` but permits using the protected setter in subclasses, which occurs in `SavingsAccount.AccumulateInterest`, with `Balance` on the left side of the assignment operator. (Properties and the protected keyword are in Chapter 5 in Book II. You can look them up in this book's index.)

## Chapter 7: Poly-what-ism?

### In This Chapter

- Deciding whether to hide or override a base class method (so many choices!)
- Building abstract classes — are you for real?
- Declaring a method and the class that contains it to be abstract
- Using `ToString`, the class business card
- Sealing a class from being subclassed

In inheritance, one class “adopts” the members of another. Thus I can create a class `SavingsAccount` that inherits data members such as `account id` and methods such as `Deposit()` from a base class `BankAccount`. That’s useful, but this definition of inheritance isn’t sufficient to mimic what’s going on out there in the business world.

![](img/80ff26f06fc9ab951e1cd4257b867366_328_0.png)

See Chapter 6 of this minibook if you don’t know (or remember) much about class inheritance.

A microwave oven is a type of oven, not because it looks like an oven but, rather, because it performs the same functions as an oven. A microwave oven may perform additional functions, but it performs, at the least, the base oven functions — most importantly, heating up my nachos when I say, “StartCooking.” (I rely on my object of class `Refrigerator` to cool the beer.) I don’t particularly care what the oven must do internally to make that happen, any more than I care what type of oven it is, who made it, or whether it was on sale when my wife bought it. (Hey, wait — I do care about that last one.)

From a human vantage point, the relationship between a microwave oven and a conventional oven doesn’t seem like such a big deal, but consider the problem from the oven’s point of view. The steps that a conventional oven performs internally are completely different from those that a microwave oven may take.

![](img/80ff26f06fc9ab951e1cd4257b867366_328_1.png)

The power of inheritance lies in the fact that a subclass doesn’t have to inherit every single method from the base class just the way it’s written. A subclass can inherit the essence of the base class method while implementing the details differently.

### Overloading an Inherited Method

As described in Chapter 3 of this minibook (look up *overloading* in the index), two or more methods can have the same name as long as the number or type of arguments differs (or as long as both differ).

![](img/80ff26f06fc9ab951e1cd4257b867366_329_0.png)

#### It's a simple case of method overloading

Giving two methods the same name is *overloading*, as in "Keeping them straight is *overloading* my brain."

The arguments of a method become a part of its extended name, as this example demonstrates:

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

C# can differentiate the methods by their arguments. Each of the calls within `Main()` accesses a different method.

![](img/80ff26f06fc9ab951e1cd4257b867366_329_1.png)

The return type isn't part of the extended name. You can't have two methods that differ only in their return types.

#### Different class, different method

Not surprisingly, the class to which a method belongs is also a part of its extended name. Consider this code segment:

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

The name of the class is a part of the extended name of the method. The method `MyClass.AMethod()` has about as much to do with `UrClass.AMethod()` as `YourClass.StartOnAColdMorning()` with `MyCar.StartOnAColdMorning()` — at least yours works.

#### Peek-a-boo — hiding a base class method

So a method in one class can overload another method in its own class by having different arguments. As it turns out, a method can also overload a method in its own base class. Overloading a base class method is known as *hiding the method*.

Suppose that your bank adopts a policy that makes savings account withdrawals different from other types of withdrawals. Suppose, just for the sake of argument, that withdrawing from a savings account costs $1.50.

Taking the procedural approach, you could implement this policy by setting a flag (variable) in the class to indicate whether the object is a `SavingsAccount` or just a simple `BankAccount`. Then the withdrawal method would have to check the flag to decide whether it needs to charge $1.50, as shown here:

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

Your method must tell the `BankAccount` whether it's a `SavingsAccount` in the constructor by passing a flag. The constructor saves that flag and uses it in the `Withdraw()` method to decide whether to charge the extra $1.50.

The more object-oriented approach hides the method `Withdraw()` in the base class `BankAccount` with a new method of the same name, height, and hair color in the `SavingsAccount` class:

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
```



请注意，我们只定义了与储蓄账户直接相关的函数和数据，在本例中，是存入和取出资金的函数。我们不需要重新定义与银行账户相关的所有变量和函数——例如存储利率、美元、分，或定义 update( ) 函数——因为这些成员将从 BankAccount 类继承，并在我们构造 SavingsAccount 对象时自动创建。例如，如果我们创建一个 SavingsAccount 对象，我们可以调用以下函数：

```
SavingsAccount account(100, 50, 5.5);
account.deposit(10,25);
account.output(cout);
```

在派生类中调用函数，

在父类 BankAccount 中调用函数

在本例中，继承使我们能够在派生类的上下文中重用父类中定义的代码。此外，如果我们以后更改 BankAccount 的某个函数——例如 update( )——那么在程序重新编译和链接后，新的代码将自动从其派生类的上下文中使用。Display 10.9 给出了 SavingsAccount 类的实现以及一个用于测试 deposit 和 withdraw 函数的 main 函数。为了简单起见，我们在 deposit 和 withdraw 函数中省略了验证，例如检查负数金额，但你应该能够很容易地使用一些 if 语句添加它们。

一旦 SavingsAccount 类被定义，我们可以更进一步，从 SavingsAccount 派生出更专业的类。例如，要定义 CD 账户类，我们需要一个新的私有成员变量来存储到期天数，并定义函数来访问该变量：

```
class CDAccount : public SavingsAccount
{
public:
    CDAccount(int dollars, int cents, double rate,
              int daysToMaturity);
    <Other constructors would normally go here>
    int getDaysToMaturity();
    //Returns the number of days until the CD matures
    void decrementDaysToMaturity();
    //Subtracts one from the daysToMaturity variable
private:
    int daysToMaturity; //Days until the CD matures
};
```

同样，我们只定义了与 CD 账户直接相关的函数和数据，在本例中，是存储和操作到期天数的功能。我们不需要重新定义与银行账户或储蓄账户相关的所有变量和函数，因为这些成员将从父类继承。例如，一旦 CDAccount 类中的函数实现完成，给定一个 CDAccount 对象，我们就可以从 CDAccount、SavingsAccount 或 BankAccount 类调用以下函数：

## DISPLAY 10.9 A SavingsAccount Derived Class (part 1 of 2)

<Everything from Display 10.6 should be inserted here except for the main function.>

```
1  class SavingsAccount : public BankAccount
2  {
3  public:
4      SavingsAccount(int dollars, int cents, double rate);
5      //Other constructors would go here
6      void deposit(int dollars, int cents);
7      //Adds $dollars.cents to the account balance
8      void withdraw(int dollars, int cents);
9      //Subtracts $dollars.cents from the account balance
10 private:
11 };
12 int main()
13 {
14     SavingsAccount account(100, 50, 5.5);
15     account.output(cout);
16     cout << endl;
17     cout << "Depositing $10.25." << endl;
18     account.deposit(10,25);
19     account.output(cout);
20     cout << endl;
21     cout << "Withdrawing $11.80." << endl;
22     account.withdraw(11,80);
23     account.output(cout);
24     cout << endl;
25     return 0;
26 }
27 SavingsAccount::SavingsAccount(int dollars, int cents, double rate):
28     BankAccount(dollars, cents, rate)
29 {
30     //deliberately empty
31 }
32 void SavingsAccount::deposit(int dollars, int cents)
33 {
34     double balance = getBalance();
35     balance += dollars;
36     balance += (static_cast<double>(cents) / 100);
37     int newDollars = static_cast<int>(balance);
38     int newCents = static_cast<int>((balance - newDollars) * 100);
```

冒号表示类 SavingsAccount 是从类 BankAccount 派生而来

只需要定义新的成员函数或变量

SavingsAccount 构造函数调用 BankAccount 构造函数。注意前面的冒号。

deposit 函数将新金额添加到余额中，并通过 set 函数更改成员变量

## DISPLAY 10.9 A SavingsAccount Derived Class (part 2 of 2)

```
39     set(newDollars, newCents, getRate());
40   }
41   void SavingsAccount::withdraw(int dollars, int cents)
42   {
43     double balance = getBalance();
44     balance -= dollars;
45     balance -= (static_cast<double>(cents) / 100);
46     int newDollars = static_cast<int>(balance);
47     int newCents = static_cast<int>((balance - newDollars) * 100);
48     set(newDollars, newCents, getRate());
49   }
```

withdraw 函数从余额中减去金额，并通过 set 函数更改成员变量

# Screen Output

```
Account balance $100.50
Interest rate 5.50%
Depositing $10.25.
Account balance $110.75
Interest rate 5.50%
Withdrawing $11.80.
Account balance $98.95
Interest rate 5.50%
```

```
//Create a new CD with $1000, 6% interest, 180 days to maturity
CDAccount newCD(1000, 0, 6.0, 180);
newCD.deposit(100,50);
daysToMaturity = newCD.getDaysToMaturity();
//Returns 180
balance = newCD.getBalance();
//Returns 1100.50
```

在 SavingsAccount 中调用函数

在 CDAccount 中调用函数

在 BankAccount 中调用函数

这个简短的例子仅触及了使用继承所能实现的功能的表面。更多细节在第 15 章中描述。虽然学习如何有效地使用继承设计类需要一定的努力，但从长远来看，这种努力会得到回报。你将编写更少的代码，这些代码比不使用继承的代码更容易理解和维护。

## SELF-TEST EXERCISES

29. 继承如何支持代码重用并使代码更易于维护？

30. 派生类能否直接按名称访问父类的私有成员变量？

31. 假设类 SportsCar 是类 Automobile 的派生类。假设类 Automobile 具有名为 accelerate 和 addGas 的公共成员函数。类 SportsCar 的对象是否会有名为 accelerate 和 addGas 的成员函数？

## CHAPTER SUMMARY

+   - 结构可用于将不同类型的数据组合成一个单一的复合数据值。
+   - 类可用于将数据和函数组合成一个单一的复合对象。
+   - 类的成员变量或成员函数可以是 public 或 private。如果它是 public，则可以在类外使用。如果它是 private，则只能在类的另一个成员函数定义中使用。
+   - 函数可以具有类或结构类型的形式参数。函数可以返回类或结构类型的值。
+   - 类的成员函数可以像普通函数一样被重载。
+   - 构造函数是类的成员函数，在声明该类的对象时自动调用。构造函数必须与它所属的类同名。
+   - 数据类型由一组值以及定义在此类值上的基本操作集合组成。
+   - 如果使用该类型的程序员不需要知道该类型的值和操作的实现细节，则该数据类型称为抽象数据类型，缩写为 ADT。
+   - 在 C++ 中实现抽象数据类型的一种方法是定义一个类，所有成员变量均为 private，并且操作作为 public 成员函数实现。
+   - 继承是指类之间的父/子关系。子或派生类继承父类的成员。

## Answers to Self-Test Exercises

+   1. a. double
+      b. double
+      c. illegal–cannot use struct tag instead of a structure variable
+      d. illegal–savingsAccount undeclared
+      e. char
+      f. TermAccount

+   2. A $9.99
+      A $1.11

3. 许多编译器会给出不好的错误信息。令人惊讶的是，g++ 的错误信息相当有信息量。

```
g++ -fsyntax-only c10testq3.cpp
c10testq3.cc:8: semicolon missing after declaration of
'Stuff'
c10testq3.cc:8: extraneous 'int' ignored
c10testq3.cc:8: semicolon missing after declaration of
'struct Stuff'
```

4. A x = {1,2};

+   5. a. 初始化器太少，不是语法错误。初始化后，dueDate.month == 12，dueDate.day == 21，dueDate.year == 0。未提供初始值的成员变量将被初始化为适当类型的零。
+      b. 初始化后正确：12 == dueDate.month，21 == dueDate.day，2022 == dueDate.year。
+      c. 错误：初始化器太多。
+      d. 可能是一个设计错误，即意图上的错误。代码的作者仅为日期初始化器提供了两位数字。应使用四位数字表示年份，因为使用两位数字日期的程序在世纪之交时可能会以从有趣到灾难性的各种方式失败。

```
6. struct EmployeeRecord
{
    double wageRate;
    int vacation;
    char status;
};
```

```
7. void readShoeRecord(ShoeType& newShoe)
{
```


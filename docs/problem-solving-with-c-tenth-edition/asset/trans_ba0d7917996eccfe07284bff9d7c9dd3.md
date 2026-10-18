

```cpp
cout << "Enter shoe style (one letter): ";
cin >> newShoe.style;
cout << "Enter shoe price $";
cin >> newShoe.price;
}
```

8.
```cpp
ShoeType discount(ShoeType oldRecord)
{
    ShoeType temp;
    temp.style = oldRecord.style;
    temp.price = 0.90 * oldRecord.price;
    return temp;
}
```

9.
```cpp
struct StockRecord
{
    ShoeType shoeInfo;
    Date arrivalDate;
};
```

10.
```cpp
StockRecord aRecord;
aRecord.arrivalDate.year = 2006;
```

11.
```cpp
void DayOfYear::input()
{
    cout << "Enter month as a number: ";
    cin >> month;
    cout << "Enter the day of the month: ";
    cin >> day;
}
```

12.
```cpp
void Temperature::set(double newDegrees, char newScale)
{
    degrees = newDegrees;
    scale = newScale;
}
```

13. 既点运算符又作用域解析运算符都与成员名一起使用，以指定成员名所属的类或结构体。如果类 DayOfYear 如 Display 10.3 中定义，且 today 是 DayOfYear 类的对象，则成员 month 可通过点运算符访问：today.month。当我们给出成员函数的定义时，作用域解析运算符用于告诉编译器此函数是类名之前给出的类中声明的函数。

14.
```cpp
void DayOfYear::checkDate()
{
    if ((month < 1) || (month > 12)
        || (day < 1) || (day > 31))
    {
        cout << "Illegal date. Aborting program.\n";
        exit(1);
    }
    if (((month == 4) || (month == 6) || (month == 9)
            || (month == 11))
        && (day == 31))
    {
        cout << "Illegal date. Aborting program.\n";
        exit(1);
    }
    if ((month == 2) && (day > 29))
    {
        cout << "Illegal date. Aborting program.\n";
        exit(1);
    }
}
```

15.
```cpp
hyundai.price = 4999.99; //ILLEGAL. price is private.

jaguar.setPrice(30000.97); //LEGAL
double aPrice, aProfit; //LEGAL
aPrice = jaguar.getPrice(); //LEGAL
aProfit = jaguar.getProfit(); //ILLEGAL. getProfit is private.
aProfit = hyundai.getProfit(); //ILLEGAL. getProfit is private.
if (hyundai == jaguar) //ILLEGAL. Cannot use == with classes.
    cout << "Want to swap cars?";
hyundai = jaguar; //LEGAL
```

16. 修改后，它们都将合法，除了以下仍然非法的：

```cpp
if (hyundai == jaguar) //ILLEGAL. Cannot use == with classes.
    cout << "Want to swap cars?";
```

17. private 将对私有成员变量的访问限制为同一类的成员函数。这将任何对私有变量的更改限制为类作者提供的函数。类作者因此可以控制对私有数据的这些更改，防止对类数据的不慎破坏。

18.
   a. 只有一个。编译器会警告你在类中没有 public: 成员（或结构体亦然）。
   b. 没有；我们通常期望在类中至少找到一个 private: 部分。
   c. 在类中，此类部分默认是 private: 部分。
   d. 在结构体中，此类部分默认是 public: 部分。

19. 一个可能的正确答案如下：

```cpp
double difference(BankAccount account1, BankAccount account2)
{
    return (account1.getBalance() - account2.getBalance());
}
```

请注意，以下是不正确的，因为 balance 是私有成员。

```cpp
double difference(BankAccount account1, BankAccount account2)
{
    return (account1.balance - account2.balance); // ILLEGAL
}
```

20.
```cpp
void update(BankAccount& theAccount)
{
    theAccount.update();
    theAccount.update();
}
```

请注意，由于这不是成员函数，你在调用 update 时必须给出对象名和点运算符。

21.
```cpp
BankAccount newAccount(BankAccount oldAccount)
{
    BankAccount temp;
    temp.set(0, oldAccount.getRate());
    return temp;
}
```

22.
```cpp
YourClass anObject(42, 'A'); // LEGAL
YourClass anotherObject; // LEGAL
YourClass yetAnotherObject(); // PROBLEM
anObject = YourClass(99, 'B'); // LEGAL
anObject = YourClass(); // LEGAL
anObject = YourClass; // ILLEGAL
```

标记为 `// PROBLEM` 的语句严格来说并非非法，但它并不意味着你可能认为的含义。如果你希望这是一个名为 yetAnotherObject 的对象声明，那么它是错误的。它是对一个名为 yetAnotherObject 的函数进行的正确函数声明，该函数不带参数并返回 YourClass 类型的值，但这不是预期的含义。从实际角度来看，你可以认为它是非法的。声明一个名为 yetAnotherObject 的对象使其使用默认构造函数初始化的正确方法是如下：

```cpp
YourClass yetAnotherObject;
```

23. 修改后的类定义如下：

```cpp
class DayOfYear
{
public:
    DayOfYear(int theMonth, int theDay);
    //Precondition: theMonth and theDay form a
    //possible date. Initializes the date according to
    //the arguments.
    DayOfYear();
    //Initializes the date to January first.
    void input();
    void output();
    int getMonth();
    //Returns the month, 1 for January, 2 for February, etc.
    int getDay();
    //Returns the day of the month.
private:
    void checkDate();
    int month;
    int day;
};
```

请注意，我们省略了成员函数 set，因为构造函数使 set 不再必要。你还必须添加以下函数定义（并删除 DayOfYear::set 的函数定义）：

```cpp
DayOfYear::DayOfYear(int theMonth, int theDay)
{
    month = theMonth;
    day = theDay;
    checkDate();
}
DayOfYear::DayOfYear()
{
    month = 1;
    day = 1;
}
```

24. 类定义与上一练习相同。构造函数定义将更改为如下：

```cpp
DayOfYear::DayOfYear(int theMonth, int theDay)
    : month(theMonth), day(theDay)
{
    checkDate();
}
DayOfYear::DayOfYear() : month(1), day(1)
{
    //Body intentionally empty.
}
```

25. 所有成员变量都应为私有。属于 ADT 接口的成员函数（即 ADT 的操作成员函数）应为公开。你还可能有仅在其他成员函数定义中使用辅助帮助函数。这些辅助函数应为私有。

26. 所有私有成员变量的声明都是实现的一部分。（不应有公开成员变量。）类的所有公开成员函数的函数声明（在类定义中列出）以及这些函数声明的解释性注释是接口的一部分。所有私有成员函数的函数声明都是实现的一部分。所有成员函数定义（无论函数是公开还是私有）都是实现的一部分。

27. 你只需要阅读接口部分。也就是说，你只需要阅读类公开成员的函数声明（在类定义中列出）以及这些函数声明的解释性注释。你无需阅读任何私有成员函数的函数声明、私有成员变量的声明、公开成员函数的定义或私有成员函数的定义。

28.
```cpp
BankAccount::BankAccount(int dollars, int cents, double rate) : dollarsPart(dollars), centsPart(cents), interestRate(fraction(rate))
{
    if ((dollars < 0) || (cents < 0) || (rate < 0))
    {
        cout << "Illegal values for money or interest rate.\n";
        exit(1);
    }
}
BankAccount::BankAccount(int dollars, double rate)
    : dollarsPart(dollars), centsPart(0), interestRate(fraction(rate))
{
    if ((dollars < 0) || (rate < 0))
    {
        cout << "Illegal values for money or interest rate.\n";
        exit(1);
    }
}
```

29. 为父类定义的功能和数据可以提供给派生类，从而消除在派生类中重新定义功能和数据的需要。这增强了可维护性，因为现在多个类之间没有代码重复，因此代码中只有一个可能需要更改的位置。此外，继承提供了一种干净的方式来隔离仅适用于派生类的代码。由于此类代码仅出现在派生类的定义中，因此通常更容易阅读。

30. 不可以，但派生类可以通过公共函数间接访问父类的私有成员变量。

31. 是的，派生类将有权访问相同的函数。在第 15 章我们将讨论如何使函数对 SportsCar 类的对象与 Automobile 类的对象做不同的事情。

## PRACTICE PROGRAMS

*Practice Programs can generally be solved with a short program that directly applies the programming principles presented in this chapter.*

1. 重新定义 Display 10.1 中的 CDAccount，使其成为类而不是结构体。使用 Display 10.1 中的相同成员变量但使其私有。包含以下成员函数：一个返回初始余额，一个返回到期余额，一个返回利率，一个返回期限。包含一个构造函数，可将所有成员变量设置为任何指定值，以及一个默认构造函数。将你的类定义嵌入到测试程序中。

2. 重新定义练习 1 中的 CDAccount 类，使其具有相同的接口但不同的实现。新实现在许多方面类似于 Display 10.7 中给出的 BankAccount 类的第二个实现。你的 CDAccount 类的新实现将记录余额为两个 int 类型的值：一个为美元，一个为美分。利率成员变量将以分数形式存储利率而不是百分比。例如，4.3% 的利率将以 double 类型的值 0.043 存储。期限以 Display 10.1 中的方式存储。

3. 剧院出售演出座位票，需要一个系统来跟踪已售出票的座位。定义一个名为 ShowTicket 的类型的类。

![](img/88b1f375f11336dbd9dac8b1675d0698_647_0.png)


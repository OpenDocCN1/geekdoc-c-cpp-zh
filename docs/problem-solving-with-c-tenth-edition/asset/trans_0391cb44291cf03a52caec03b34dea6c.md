

+   1. 将类的所有成员变量设为类的私有成员。
+   
+   2. 将程序员需要的每个基本操作设为类的公有成员函数，并完整地说明每个此类公有成员函数的使用方法。
+   
+   3. 将任何辅助函数设为私有成员函数。

在第 11 章和第 12 章中你将学习定义抽象数据类型 ADT 的一些替代方法，但这三条规则是确保一个类是抽象数据类型的常见方法之一。

ADT 的接口告诉你如何在程序中使用 ADT。当你将 ADT 定义为 C++ 类时，接口由类的公有成员函数以及说明如何使用这些公有成员函数的注释组成。ADT 的接口应该是你在程序中使用 ADT 所需要知道的全部内容。

ADT 的**实现**说明该接口如何实现为 C++ 代码。ADT 的实现由类的私有成员以及公有和私有成员函数的定义组成。虽然你需要实现来运行使用 ADT 的程序，但为了编写使用 ADT 的程序的其余部分，你不需要知道任何关于实现的细节；也就是说，为了编写程序的主体部分以及程序主体部分使用的任何非成员函数，你不需要知道任何关于实现的细节。情况与我们在第 4 章和第 5 章中对普通函数定义所倡导的情况类似。ADT 的实现，就像普通函数的实现一样，应该被视为一个你无法看到内部的黑盒子。

在第 12 章中你将学习如何将 ADT 的接口和实现放在与彼此以及使用 ADT 的程序分开的文件中。这样，使用 ADT 的程序员实际上看不到实现。在此之前，我们将把我们 ADT 类的所有细节放在与程序主体部分相同的<|message|> 中，但我们仍然认为接口（在类定义的公有部分给出）和实现（类定义的私有部分和成员函数定义）是 ADT 的两个独立部分。我们将努力编写我们的 ADT，使得 ADT 的使用者只需要知道 ADT 的接口，而不需要知道任何关于实现的细节。为了确保你以这种方式定义你的 ADT，只需确保如果你更改了 ADT 的实现，你的程序仍可在无需更改程序任何其他部分的情况下正常工作。这在下一个编程示例中进行了说明。

使你的类成为 ADT 的最明显的好处是你可以在无需更改程序其他部分的情况下更改实现。但 ADT 提供的益处不止于此。如果你使你的类成为 ADT，你就可以在不同程序员之间分配工作，

![](img/88b1f375f11336dbd9dac8b1675d0698_628_0.png)

一个程序员设计并编写 ADT，而其他程序员使用 ADT。即使你是项目中唯一的程序员，你也将一个较大的任务划分为两个较小的任务，这使得你的程序更容易设计，也更容易调试。

## PROGRAMMING EXAMPLE

## Alternative Implementation of a Class

Display 10.7 包含上一小节中讨论的 ADT 类 BankAccount 的替代实现。在这个版本中，银行账户的数据被实现为三个成员值：一个用于账户余额的美元部分，一个用于账户余额的分部分，以及一个用于利率。

请注意，虽然 Display 10.6 中的实现和 Display 10.7 中的实现都具有名为 interestRate 的成员变量，但在两个实现中存储的值略有不同。如果账户按 4.7% 的利率支付利息，则在 Display 10.6 中的实现中（基本上与 Display 10.5 中的实现相同），interestRate 的值为 4.7。然而，在 Display 10.7 中的实现中，interestRate 的值将为 0.047。这个在 Display 10.7 中显示的替代实现将利率存储为分数而不是百分比数字。这个新实现中的基本区别是，当设置利率时，函数 fraction 被用来立即将利率转换为分数。因此，在这个新实现中，私有成员函数 fraction 在构造函数的定义中使用，但在成员函数 update 的定义中不需要，因为成员变量 interestRate 中的值已经转换为分数。在旧实现中（显示在 Display 10.5 和 Display 10.6 中），情况正好相反。在旧实现中，私有成员函数 fraction 未在构造函数的定义中使用，但在 update 的定义中使用。

尽管我们更改了类 BankAccount 的私有成员，但我们没有更改类定义的公有部分。公有成员函数具有相同的函数声明，并且它们的行为与 Display 10.6 中给出的旧 ADT 类版本中的行为完全相同。例如，尽管这个新实现将 4.7% 这样的百分比存储为分数 0.047，但成员函数 getRate 仍然返回值 4.7，就像它对 Display 10.5 中的旧实现一样。同样，成员函数 getBalance 返回类型为 double 的单个值，该值以带小数点的数字给出余额，就像它在 Display 10.5 中的旧实现中一样。这即使在余额现在存储在两个类型为 int 的成员变量中，而不是存储在单个类型为 double 的成员变量中（像旧版本那样）时也是如此。

公有接口未被更改

### DISPLAY 10.7 Alternative BankAccount Class Implementation (part 1 of 4)

```
1  //Demonstrates an alternative implementation of the class BankAccount.
2  #include <iostream>
3  #include <cmath>
4  using namespace std;
5  //Class for a bank account:
6  class BankAccount
7  {
8  public:
9    BankAccount(int dollars, int cents, double rate);
10   //Initializes the account balance to $dollars.cents and
11   //initializes the interest rate to rate percent.
12
13   BankAccount(int dollars, double rate);
14   //Initializes the account balance to $dollars.00 and
15   //initializes the interest rate to rate percent.
16
17   BankAccount();
18   //Initializes the account balance to $0.00 and the
19   //interest rate to 0.0%.
20
21   void set(int dollars, int cents, double rate);
22   //Postcondition: The account balance has been set to $dollars.cents;
23   //The interest rate has been set to rate percent.
24
25   void set(int dollars, double rate);
26   //Postcondition: The account balance has been set to $dollars.00.
27   //The interest rate has been set to rate percent.
28
29   void update();
30   //Postcondition: One year of simple interest has been
31   //added to the account balance.
32
33   double getBalance();
34   //Returns the current account balance.
35
36   double getRate();
37   //Returns the current account interest rate as a percentage.
38
39   void output(ostream& outs);
40   //Precondition: If outs is a file output stream, then
41   //outs has already been connected to a file.
42   //Postcondition: Account balance and interest rate
43   //have been written to the stream outs.
44
45   private:
46     int dollarsPart;
47     int centsPart;
48     double interestRate;
49     //Expressed as a fraction, for example, 0.057 for 5.7%
```

> Notice that the public members of BankAccount look and behave exactly the same as in Display 10.6

### DISPLAY 10.7 Alternative BankAccount Class Implementation (part 2 of 4)

```
41   double fraction(double percent);
42   //Converts a percentage to a fraction. For example, fraction(50.3)
43   //returns 0.503.
44   double percent(double fractionValue);
45   //Converts a fraction to a percentage. For example, percent(0.503)
46   //returns 50.3.
47   };
48   int main()
49   {
50     BankAccount account1(100, 2.3), account2;
51   
52     cout << "account1 initialized as follows:\n";
53     account1.output(cout);
54     cout << "account2 initialized as follows:\n";
55     account2.output(cout);
56   
57     account1 = BankAccount(999, 99, 5.5);
58     cout << "account1 reset to the following:\n";
59     account1.output(cout);
60     return 0;
61   }
62   BankAccount::BankAccount(int dollars, int cents, double rate)
63   {
64     if ((dollars < 0) || (cents < 0) || (rate < 0))
65     {
66       cout << "Illegal values for money or interest rate.\n";
67       exit(1);
68     }
69     dollarsPart = dollars;
70     centsPart = cents;
71     interestRate = fraction(rate);
72   }
73   BankAccount::BankAccount(int dollars, double rate)
74   {
75     if ((dollars < 0) || (rate < 0))
76     {
77       cout << "Illegal values for money or interest rate.\n";
78       exit(1);
79     }
80     dollarsPart = dollars;
81     centsPart = 0;
82     interestRate = fraction(rate);
83   }
84   BankAccount::BankAccount() : dollarsPart(0), centsPart(0), interestRate(0.0)
```

New

Since the body of main is identical to that in Display 10.6, the screen output is also identical to that in Display 10.6

In the old implementation of this ADT, the private member function fraction was used in the definition of update. In this implementation, fraction is instead used in the definition of constructors and in the set function.


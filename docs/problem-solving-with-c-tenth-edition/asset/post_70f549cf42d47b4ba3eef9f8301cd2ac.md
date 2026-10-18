
+   1. Make all the member variables private members of the class.
+   
+   2. Make each of the basic operations that the programmer needs a public member function of the class, and fully specify how to use each such public member function.
+   
+   3. Make any helping functions private member functions.

In Chapters 11 and 12 you will learn some alternative approaches to defining ADTs, but these three rules are one common way to ensure that a class is an abstract data type.

The interface of an ADT tells you how to use the ADT in your program. When you define an ADT as a C++ class, the interface consists of the public member functions of the class along with the comments that tell you how to use these public member functions. The interface of the ADT should be all you need to know in order to use the ADT in your program.

The **implementation** of the ADT tells how this interface is realized as C++ code. The implementation of the ADT consists of the private members of the class and the definitions of both the public and private member functions. Although you need the implementation in order to run a program that uses the ADT, you should not need to know anything about the implementation in order to write the rest of a program that uses the ADT; that is, you should not need to know anything about the implementation in order to write the main part of the program and to write any nonmember functions used by the main part of the program. The situation is similar to what we advocated for ordinary function definitions in Chapters 4 and 5. The implementation of an ADT, like the implementation of an ordinary function, should be thought of as being in a black box that you cannot see inside.

In Chapter 12 you will learn how to place the interface and implementation of an ADT in files separate from each other and separate from the programs that use the ADT. That way a programmer who uses the ADT literally does not see the implementation. Until then, we will place all of the details about our ADT classes in the same file as the main part of our program, but we still think of the interface (given in the public section of the class definitions) and the implementation (the private section of the class definition and the member function definitions) as separate parts of the ADT. We will strive to write our ADTs so that the user of the ADT need only know about the interface of the ADT and need not know anything about the implementation. To be sure you are defining your ADTs this way, simply make sure that if you change the implementation of your ADT, your program will still work without your needing to change any other part of the program. This is illustrated in the next Programming Example.

The most obvious benefit you derive from making your classes ADTs is that you can change the implementation without needing to change the other parts of your program. But ADTs provide more benefits than that. If you make your classes ADTs, you can divide work among different programmers, with

![](img/88b1f375f11336dbd9dac8b1675d0698_628_0.png)

one programmer designing and writing the ADT and other programmers using the ADT. Even if you are the only programmer working on a project, you have divided one larger task into two smaller tasks, which makes your program easier to design and easier to debug.

## PROGRAMMING EXAMPLE

## Alternative Implementation of a Class

Display 10.7 contains the alternative implementation of the ADT class BankAccount discussed in the previous subsection. In this version, the data for a bank account is implemented as three member values: one for the dollars part of the account balance, one for the cents part of the account balance, and one for the interest rate.

Notice that, although both the implementation in Display 10.6 and the implementation in Display 10.7 each have a member variable called interestRate, the value stored is slightly different in the two implementations. If the account pays interest at a rate of 4.7%, then in the implementation in Display 10.6 (which is basically the same as the one in Display 10.5), the value of interestRate is 4.7. However, in the implementation in Display 10.7, the value of interestRate would be 0.047. This alternative implementation, shown in Display 10.7, stores the interest rate as a fraction rather than as a percentage figure. The basic difference in this new implementation is that when an interest rate is set, the function fraction is used to immediately convert the interest rate to a fraction. Hence, in this new implementation the private member function fraction is used in the definitions of constructors, but it is not needed in the definition of the member function update because the value in the member variable interestRate has already been converted to a fraction. In the old implementation (shown in Display 10.5 and Display 10.6), the situation was just the reverse. In the old implementation, the private member function fraction was not used in the definition of constructors, but was used in the definition of update.

Although we have changed the private members of the class BankAccount, we have not changed anything in the public section of the class definition. The public member functions have the same function declarations and they behave exactly as they did in the old version of the ADT class given in Display 10.6. For example, although this new implementation stores a percentage such as 4.7% as the fraction 0.047, the member function getRate still returns the value 4.7, just as it would for the old implementation in Display 10.5. Similarly, the member function getBalance returns a single value of type double, which gives the balance as a number with a decimal point, just as it did in the old implementation in Display 10.5. This is true even though the balance is now stored in two member variables of type int, rather than in a single member variable of type double (as in the old versions).

The public interface is not changed

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

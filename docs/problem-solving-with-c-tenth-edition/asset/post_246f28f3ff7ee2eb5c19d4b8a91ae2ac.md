
Notice that we only defined functions and data that specifically relate to savings accounts, in this case, functions to deposit and withdraw money. We don’t need to redefine all of the variables and functions relating to bank accounts—such as storing the interest rate, dollars, cents, or defining the update( ) function—because those members will be inherited from the BankAccount class and are automatically created when we construct a SavingsAccount object. For example, if we create a SavingsAccount object, we could invoke the following functions:

```
SavingsAccount account(100, 50, 5.5);
account.deposit(10,25);
account.output(cout);
```

Invoking a function in the derived class,

Invoking a function in the parent class, BankAccount

In this example, inheritance allowed us to reuse code defined in the parent class from the context of the derived class. Moreover, if we later change one of BankAccount’s functions—such as update( )—then the new code automatically will be used from the context of its derived classes when the program is recompiled and linked. An implementation of the SavingsAccount class along with a main function to test the deposit and withdraw functions is given in Display 10.9. For simplicity, we have left verification out of the deposit and withdraw functions, for example, checking for negative amounts, but you should be able to add them easily with some if statements.

Once the SavingsAccount class is defined we can go one step further and derive more specialized classes from the SavingsAccount. For example, to define the CD account class we need a new private member variable to store the days until maturity and define functions to access this variable:

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

Once again, we only defined functions and data that specifically relate to CD accounts, in this case, storing and manipulating the number of days to maturity. We don’t need to redefine all of the variables and functions relating to bank accounts or savings accounts because those members will be inherited from the parent classes. For example, once the functions in the CDAccount class are implemented, we could invoke the following functions from the CDAccount, SavingsAccount, or BankAccount classes given a CDAccount object:

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

The colon indicates that the class SavingsAccount is derived from the class BankAccount

Only new member functions or variables need to be defined

The SavingsAccount constructor invokes the BankAccount constructor. Note the preceding colon.

The deposit function adds the new amount to the balance and changes the member variables via the set function

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

The withdraw function subtracts the amount from the balance and changes the member variables via the set function

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

Invoking a function in SavingsAccount

Invoking a function in CDAccount

Invoking a function in BankAccount

This short example has only scratched the surface of what is possible using inheritance. Additional details are described in Chapter 15. While it does take some effort to learn how to effectively design classes using inheritance, the effort will pay off in the long run. You will end up writing less code that is easier to understand and maintain than code that does not use inheritance.

## SELF-TEST EXERCISES

29. How does inheritance support code reuse and make code easier to maintain?

30. Can a derived class directly access by name a private member variable of the parent class?

31. Suppose the class SportsCar is a derived class of a class Automobile. Suppose also that the class Automobile has public member functions named accelerate and addGas. Will an object of the class SportsCar have member functions named accelerate and addGas?

## CHAPTER SUMMARY

+   - A structure can be used to combine data of different types into a single (compound) data value.
+   - A class can be used to combine data and functions into a single (compound) object.
+   - A member variable or a member function for a class may be either public or private. If it is public, it can be used outside of the class. If it is private, it can be used only in the definition of another member function in the class.
+   - A function may have formal parameters of a class or structure type. A function may return values of a class or structure type.
+   - A member function for a class can be overloaded in the same way as ordinary functions are overloaded.
+   - A constructor is a member function of a class that is called automatically when an object of the class is declared. A constructor must have the same name as the class of which it is a member.
+   - A data type consists of a collection of values together with a set of basic operations defined on these values.
+   - A data type is called an abstract data type (abbreviated ADT) if a programmer who uses the type does not need to know any of the details about how the values and operations for that type are implemented.
+   - One way to implement an abstract data type in C++ is to define a class with all member variables being private and with the operations implemented as public member functions.
+   - Inheritance refers to a parent/child relationship between classes. The child or derived class inherits members from the parent class.

## Answers to Self-Test Exercises

+   1. a. double
+      b. double
+      c. illegal–cannot use struct tag instead of a structure variable
+      d. illegal–savingsAccount undeclared
+      e. char
+      f. TermAccount

+   2. A $9.99
+      A $1.11

3. Many compilers give poor error messages. Surprisingly, the error message from g++ is quite informative.

```
g++ -fsyntax-only c10testq3.cpp
c10testq3.cc:8: semicolon missing after declaration of
'Stuff'
c10testq3.cc:8: extraneous 'int' ignored
c10testq3.cc:8: semicolon missing after declaration of
'struct Stuff'
```

4. A x = {1,2};

+   5. a. Too few initializers, not a syntax error. After initialization, dueDate.month == 12, dueDate.day == 21, dueDate.year == 0. Member variables not provided an initializer are initialized to a zero of appropriate type.
+      b. Correct after initialization: 12 == dueDate.month, 21 == dueDate.day, 2022 == dueDate.year.
+      c. Error: too many initializers.
+      d. May be a design error, that is, an error in intent. The author of the code provides only two digits for the date initializer. There should be four digits used for the year because a program using two-digit dates could fail in ways that vary from amusing to disastrous at the turn of the century.

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

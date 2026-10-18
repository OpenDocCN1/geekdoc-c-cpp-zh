
## DISPLAY 10.6 Class with Constructors (part 2 of 3)

```
24   //Postcondition: One year of simple interest has been added
25   //to the account balance.
26   double getBalance();
27   //Returns the current account balance.
28   double getRate();
29   //Returns the current account interest rate as a percentage.
30   void output(ostream& outs);
31   //Precondition: If outs is a file output stream, then
32   //outs has already been connected to a file.
33   //Postcondition: Account balance and interest rate
34   //have been written to the stream outs.
35 private:
36     double balance;
37     double interestRate;
38     double fraction(double percent);
39     //Converts a percentage to a fraction. For example, fraction(50.3)
40     //returns 0.503.
41 };
42 int main()
43 {
44   BankAccount account1(100, 2.3), account2;
45   cout << "account1 initialized as follows:\n";
46   account1.output(cout);
47   cout << "account2 initialized as follows:\n";
48   account2.output(cout);
49   account1 = BankAccount(999, 99, 5.5);
50   cout << "account1 reset to the following:\n";
51   account1.output(cout);
52   return 0;
53 }
54 BankAccount::BankAccount(int dollars, int cents, double rate)
55 {
56   if ((dollars < 0) || (cents < 0) || (rate < 0))
57   {
58     cout << "Illegal values for money or interest rate.\n";
59     return;
60   }
61   balance = dollars + 0.01 * cents;
62   interestRate = rate;
63 }
64 BankAccount::BankAccount(int dollars, double rate)
65
```

> This declaration causes a call to the default constructor. Notice that there are no parentheses.

> An explicit call to the constructor BankAccount::BankAccount

## DISPLAY 10.6 Class with Constructors (part 3 of 3)

```
66     if ((dollars < 0) || (rate < 0))
67     {
68         cout << "Illegal values for money or interest rate.\n";
69         return;
70     }
71     balance = dollars;
72     interestRate = rate;
73 }
74 BankAccount::BankAccount( ) : balance(0), interestRate(0.0)
75 {
76     //Body intentionally empty
77 }
```

<Definitions of the other member functions are the same as in Display 10.5.

## Screen Output

```
account1 initialized as follows:
Account balance $100.00
Interest rate 2.30%
account2 initialized as follows:
Account balance $0.00
Interest rate 0.00%
account1 reset to the following:
Account balance $999.99
Interest rate 5.50%
```

## Constructor

A constructor is a member function of a class that has the same name as the class. A constructor is called automatically when an object of the class is declared. Constructors are used to initialize objects. A constructor must have the same name as the class of which it is a member.

The constructor with no parameters in Display 10.6 deserves some extra discussion since it contains something we have not seen before. For reference, we reproduce the defining of the constructor with no parameters:

```
BankAccount::BankAccount() : balance(0), interestRate(0.0)
{
    //Body intentionally empty
}
```

The new element, which is shown on the first line, is the part that starts with a single colon. This part of the constructor definition is called the initialization section. As this example shows, the initialization section goes after the parentheses that ends the parameter list and before the opening brace of the function body. The initialization section consists of a colon followed by a list of some or all the member variables separated by commas. Each member variable is followed by its initializing value in parentheses. This constructor definition is completely equivalent to the following way of writing the definition:

```
BankAccount::BankAccount( )
{
    balance = 0;
    interestRate = 0.0;
}
```

The function body in a constructor definition with an initialization section need not be empty. For example, the following definition of the two-parameter constructor is equivalent to the one given in Display 10.6:

```
BankAccount::BankAccount(int dollars, double rate)
    : balance(dollars), interestRate(rate)
{
    if ((dollars < 0) || (rate < 0))
    {
        cout << "Illegal values for money or interest rate.\n";
        exit(1);
    }
}
```

Notice that the initializing values can be given in terms of the constructor parameters.

## Constructor Initialization Section

Some or all of the member variables in a class can (optionally) be initialized in the constructor initialization section of a constructor definition. The constructor initialization section goes after the parentheses that end the parameter list and before the opening brace of the function body. The initialization section consists of a colon followed by a list of some or all the member variables separated by commas. Each member variable is followed by its initializing value in parentheses. The example given below uses a constructor initialization section and is equivalent to the three-parameter constructor given in Display 10.6.

(continued)

```
BankAccount::BankAccount(int dollars, int cents,
                    double rate)
  : balance(dollars + 0.01*cents), interestRate(rate)
{
  if ((dollars < 0) || (cents < 0) || (rate < 0))
  {
    cout <<
      "Illegal values for money or interest rate.\n";
    exit(1);
  }
}
```

Notice that the initializing values can be given in terms of the constructor parameters.

## Calling a Constructor

A constructor is called automatically when an object is declared, but you must give the arguments for the constructor when you declare the object. A constructor can also be called explicitly in order to create a new object for a class variable.

### SYNTAX (for an object declaration when you have constructors)

```
`ClassName ObjectName(ArgumentsForConstructor);`
```

### EXAMPLE

```
`BankAccount account1(100, 2.3);`
```

### SYNTAX (for an explicit constructor call)

```
`Object = ConstructorName(ArgumentsForConstructor);`
```

### EXAMPLE

```
`account1 = BankAccount(200, 3.5);`
```

A constructor must have the same name as the class of which it is a member. Thus, in the syntax descriptions above, _ClassName_ and _ConstructorName_ are the same identifier.

Initializers can also be specified if the object is created as a dynamic variable.

```
`BankAccount *myAcct; myAcct = new BankAccount (300, 4.2);`
```

A constructor is called automatically whenever you declare an object of the class type, but it can also be called again after the object has been declared. This allows you to conveniently set all the members of an object. The technical details are as follows. Calling the constructor creates an anonymous object with new values. An anonymous object is an object that is not named (as yet) by any variable. The anonymous object can be assigned to the named object (that is, to the class variable). For example, the following line of code is a call to the constructor BankAccount that creates an anonymous object with a balance of $999.99 and interest rate of 5.5%. This anonymous object is assigned to object account1 so that it too represents an account with a balance of $999.99 and an interest rate of 5.5%:

```
account1 = BankAccount(999, 99, 5.5);
```

As you might guess from the notation, a constructor behaves like a function that returns an object of its class type. However, since a call to a constructor always creates a new object and a call to a set member function merely changes the values of existing member variables, a call to set may be a more efficient way to change the values of member variables than a call to a constructor. Thus, for efficiency reasons or if you need to change the values of member variables without creating a new object, you may wish to have both the set member functions and the constructors in your class definition.

## PROGRAMMING TIP Always Include a Default Constructor

C++ does not always generate a default constructor for the classes you define. If you give no constructor, the compiler will generate a default constructor that does nothing. This constructor will be called if class objects are declared. On the other hand, if you give at least one constructor definition for a class, then the C++ compiler will generate no other constructors. Every time you declare an object of that type, C++ will look for an appropriate constructor definition to use. If you declare an object without using arguments for the constructor, C++ will look for a default constructor, and if you have not defined a default constructor, none will be there for it to find.

For example, suppose you define a class as follows:

```
class SampleClass
{
public:
    SampleClass(int parameter1, double parameter2);
    void do_stuff();
private:
    int data1;
    double data2;
};
```

Constructor that requires two arguments

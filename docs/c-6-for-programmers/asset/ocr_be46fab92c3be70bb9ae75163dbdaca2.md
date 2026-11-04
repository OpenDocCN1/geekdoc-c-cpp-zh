```
6 class AccountTest
7 {
8     static void Main()
9     {
10     // create two Account objects
11     Account account1 = new Account("Jane Green");
12     Account account2 = new Account("John Blue");
13
14     // display initial value of name for each Account
15     Console.WriteLine($"account1 name is: {account1.Name}");
16     Console.WriteLine($"account2 name is: {account2.Name}");
17     }
18 }
```

account1 name is: Jane Green
account2 name is: John Blue

Fig. 4.9 | Using the Account constructor to set an Account's name when an Account object is created. (Part 2 of 2.)

# Default Constructor

Recall that line 10 of Fig. 4.5

```
Account myAccount = new Account();
```

used new to create an Account object. The empty parentheses in the expression

```
new Account()
```

indicate a call to the class's default constructor—in any class that does not explicitly declare a constructor, the compiler provides a public default constructor (which always has no parameters). When a class has only the default constructor, the class's instance variables are initialized to their default values:

+   - 0 for numeric simple types,
+   - false for simple type bool and
+   - null for all other types.

In Section 10.5, you'll learn that classes can have multiple constructors through a process called overloading.

# There's No Default Constructor in a Class That Declares a Constructor

If you declare one or more constructors for a class, the compiler will not create a default constructor for that class. In that case, you will not be able to create an Account object with the expression new Account() as we did in Fig. 4.5—unless one of the custom constructors you declare takes no parameters.

# Software Engineering Observation 4.4

Unless default initialization of your class's instance variables is acceptable, provide a custom constructor to ensure that your instance variables are properly initialized with meaningful values when each new object of your class is created.
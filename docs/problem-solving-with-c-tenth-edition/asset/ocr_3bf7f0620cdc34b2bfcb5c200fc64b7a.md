direct member variables are copied. If a member variable is a reference, then the copy will point to the same reference.

# PROGRAMMING EXAMPLE
BankAccount Class—Version 1

Display 10.5 contains a class definition for a bank account that illustrates all of the points about class definitions you have seen thus far. This type of bank account allows you to withdraw your money at any time, so it has no term as did the type CDAccount that you saw earlier. A more important difference is that the class BankAccount has member functions for all the operations you would expect to use in a program. Objects of the class BankAccount have two private member variables: one to record the account balance and one to record the interest rate. Let’s discuss some features of the class BankAccount.

First, notice that the class BankAccount has a private member function called fraction. Since fraction is a private member function, it cannot be called in the body of main or in the body of any function that is not a member function of the class BankAccount. The function fraction can only be called in the definitions of other member functions of the class BankAccount. The only reason we have this (or any) private member function is to aid us in defining other member functions for the same class. In our definition of the class BankAccount, we included the member function fraction so that we could use it in the definition of the function update. The function fraction takes one argument that is a percentage figure, like 10.0 for 10.0%, and converts it to a fraction, like 0.10. That allows us to compute the amount of interest on the account at the given percentage. If the account contains $100.00 and the interest rate is 10%, then the interest is equal to $100 times 0.10, which is $10.00.

When you call a public member function, such as update, in the main body of your program, you must include an object name and a dot, as in the following line from Display 10.5:

```
account1.update();
```

One member function calling another

However, when you call a private member function (or any other member function) within the definition of another member function, you use only the member function name without any calling object or dot operator. For example, the following definition of the member function BankAccount::update includes a call to BankAccount::fraction (as shown in Display 10.5):

```
void BankAccount::update()
{
    balance = balance + fraction(interestRate) * balance;
}
```

The calling object for the member function fraction and for the member variables balance and interestRate are determined when the function update is called. For example, the meaning of
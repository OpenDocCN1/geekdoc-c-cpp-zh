```
```
double interestRate;
int numberOfYears;
cout << "How much are you investing ?\n";
cin >> principal;
cout << " What's the annual interest rate(%)?\n";
cin >> interestRate;
cout << "How long for ( years )?\n";
cin >> numberOfYears;
double interest
        = compoundInterest(principal,
            interestRate,
            numberOfYears);
cout << "You will earn ";
cout << interest;
cout << "\n";
return 0;
}
```
```

In this example, we have replaced the computation of the compound interest with a call to the **compoundInterest** function.

Note that the file contains two function definitions, one for a function called **compoundInterest** and another for a function called **main**. In fact our very first program contained a function called **main** as well, we just didn't discuss it at the time.

Every C++ application for the “console” must contain a function called **main**. A console application is just a program that reads and writes text to the screen as though it was still 1973. When the user asks to run your program, the operating system will make sure that the function **main** is called. There are many other kinds of applications, for example, web applications, windows applications, and mobile phone apps. If you're writing a console application, you need a **main** function. The rules for other kinds of application are different and beyond the scope of this book.

Here are some things to notice in our example:

+   - The definitions of the functions are written sequentially in the file. We first define **compoundInterest** completely, then we define **main** completely.

+   - The variable names used when we call the function can be completely different from those used in the definition of the function. When we choose the names of parameters and variables in a function, those names have no meaning outside of the function.

+   - There is a `return` statement at the end of each function. When a function has computed the desired value, it sends it back to the caller using the `return` keyword.
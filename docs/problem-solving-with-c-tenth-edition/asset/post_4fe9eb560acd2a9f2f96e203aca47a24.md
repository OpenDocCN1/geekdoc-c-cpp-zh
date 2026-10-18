
## DISPLAY 14.9  A Recursive Member Function *(part 1 of 2)*

```
//Program to demonstrate the recursive member function update (years).
#include <iostream>
using namespace std;

//Class for a bank account:
class BankAccount
{
public:
    BankAccount(int dollars, int cents, double rate);
    //Initializes the account balance to $dollars.cents and
    //initializes the interest rate to rate percent.

    BankAccount(int dollars, double rate);
    //Initializes the account balance to $dollars.00 and
    //initializes the interest rate to rate percent.

    BankAccount( );
    //Initializes the account balance to $0.00 and
    //initializes the interest rate to 0.0%.

    void update( );
    //Postcondition: One year of simple interest
    //has been added to the account balance.

    void update(int years);
    //Postcondition: Interest for the number of years given has been added to the
    //account balance. Interest is compounded annually.

    double getBalance( );
    //Returns the current account balance.

    double getRate( );
    //Returns the current account interest rate as a percentage.

    void output(ostream& outs);
    //Precondition: If outs is a file output stream, then outs has already
    //been connected to a file.
    //Postcondition: Balance & interest rate have been written to the stream outs.
private:
    double balance;
    double interestRate;
    double fraction(double percent); //Converts a percentage to a fraction.
};

int main( )
{
    BankAccount yourAccount(100, 5);
    yourAccount.update(10);
    cout.setf(ios::fixed);
```

![](img/88b1f375f11336dbd9dac8b1675d0698_855_0.png)

## DISPLAY 14.9 A Recursive Member Function (part 2 of 2)

```
42     cout.setf(ios::showpoint);
43     cout.precision(2);
44     cout << "If you deposit $100.00 at 5% interest, then\n"
45         << "in ten years your account will be worth $"
46         << yourAccount.getBalance( ) << endl;
47     return 0;
48 }
49 
50 void BankAccount::update( )
51 {
52     balance = balance + fraction(interestRate)*balance;
53 }
54 
55 void BankAccount::update(int years)
56 {
57     if (years == 1)
58     {
59         update( );
60     }
61     else if (years > 1)
62     {
63         update(years - 1);
64         update( );
65     }
66 }
```

Overloading (that is, calls to another function with the same name)

Recursive function call

> <Definitions of the other member functions are given in Display 10.5 and Display 10.6, but you need not read those definitions in order to understand this example.>

### Sample Dialogue

```
If you deposit $100.00 at 5% interest, then
in ten years your account will be worth $162.89
```

It is easy to see that this algorithm produces the desired result by checking the three points given in the subsection entitled "Recursive Design Techniques."

- 1. There is no infinite recursion: Each recursive call reduces the number of years by 1 until the number of years eventually becomes 1, which is the stopping case. So there is no infinite recursion.
-   
- 2. Each stopping case performs the correct action for that case: The one stopping case is when years==1. This case produces the correct action, since it simply calls the other overloaded member function called update, and we checked the correctness of that function in Chapter 10.

3. For the cases that involve recursion, if all recursive calls perform correctly, then the entire case performs correctly. The recursive case—that is, years>1—works correctly, because if the recursive call correctly posts years-1 worth of interest, then all that is needed is to post one additional year's worth of interest and the call to the overloaded zero-argument version of update will correctly post one year's worth of interest. Thus, if the recursive call performs the correct action, then the entire action for the case of years>1 will be correct.

In this example, we have overloaded update so that there are two different functions named update: one that takes no arguments and one that takes a single argument. Do not confuse the calls to the two functions named update. These are two different functions that, as far as the compiler is concerned, just coincidentally happen to have the same name. When the definition of the function update with one argument includes a call to the version of update that takes no arguments, that is not a recursive call. Only the call to the version of update with the exact same function declaration is a recursive call. To see what is involved here, note that we could have named the version of update that takes no argument postOneYear(), instead of naming it update(), and then the definition of the recursive version of update would read as follows:

```
void BankAccount::update(int years)
{
    if (years == 1)
    {
        postOneYear();
    }
    else if (years > 1)
    {
        update(years - 1);
        postOneYear();
    }
}
```

### Recursion and Overloading

Do not confuse recursion and overloading. When you overload a function name, you are giving two different functions the same name. If the definition of one of these two functions includes a call to the other, that is not recursion. In a recursive function definition, the definition of the function includes a call to the exact same function with the exact same definition, not to some other function that coincidentally uses the same name. It is not too serious an error if you confuse overloading and recursion, since they are both legal. It is simply a question of getting the terminology straight so that you can communicate clearly with other programmers and so that you understand the underlying processes.

Overloading

## SELF-TEST EXERCISES

15. Write a recursive function definition for the following function:

```
int squares(int n);
//Precondition: n >= 1
//Returns the sum of the squares of numbers 1 through n.
```

For example, squares(3) returns 14 because 1² + 2² + 3² is 14.

16. Write an iterative version of the one-argument member function Bank-Account::update(int years) that is described in Display 14.9.

## CHAPTER SUMMARY

- - If a problem can be reduced to smaller instances of the same problem, then a recursive solution is likely to be easy to find and implement.

- - A recursive algorithm for a function definition normally contains two kinds of cases: one or more cases that include at least one recursive call and one or more stopping cases in which the problem is solved without any recursive calls.

- - When writing a recursive function definition, always confirm that the function will not produce infinite recursion.

- - When you define a recursive function, use the three criteria given in the subsection “Recursive Design Techniques” to confirm that the function is correct.

- - When you design a recursive function to solve a task, it is often necessary to solve a more general problem than the given task. This may be required to allow for the proper recursive calls, since the smaller problems may not be exactly the same problem as the given task. For example, in the binary search problem, the task was to search an entire array, but the recursive solution is an algorithm to search any portion of the array (either all of it or a part of it).

## Answers to Self-Test Exercises

- 1. Hip Hip Hurray

```
2. void stars(int n)
{
    cout << '*';
    if (n > 1)
        stars(n - 1);
}
```

The following is also correct but is more complicated:

```
void stars(int n)
{
    if (n <= 1)
    {
        cout << '*';
    }
    else
    {
        stars(n - 1);
        cout << '*';
    }
}
```

- 3. `void backward(int n)`
- ```cpp
- {
-     if (n < 10)
-     {
-         cout << n;
-     }
-     else
-     {
-         cout << (n % 10); // write last digit
-         backward(n / 10); // write the other digits backward
-     }
- }
- ```

- 4. and 5. The answer to 4 is `writeUp(int n)`; The answer to 5 is `writeDown(int n)`;

```
#include <iostream>
using namespace std;
void writeDown(int n)
{
    if (n >= 1)
    {
        cout << n << " ";
        writeDown(n - 1);
    }
}

void writeUp(int n)
{
    if (n >= 1)
    {
        writeUp(n - 1);
        cout << n << " ";
    }
}
```

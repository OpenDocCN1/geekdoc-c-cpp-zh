# Display 7.2  **BankAccount Class (part 1 of 5)**

```
```cpp
#include <iostream>
#include <cmath>
#include <cstdlib>
using namespace std;

//Data consists of two items: an amount of money for the account balance
//and a percentage for the interest rate.
class BankAccount
{
public:
    BankAccount(double balance, double rate);
    //Initializes balance and rate according to arguments.

    BankAccount(int dollars, int cents, double rate);
    //Initializes the account balance to $dollars cents. For a negative balance both
    //dollars and cents must be negative. Initializes the interest rate to rate percent.

    BankAccount(int dollars, double rate);
    //Initializes the account balance to $dollars.00 and
    //initializes the interest rate to rate percent.

    BankAccount( );
    //Initializes the account balance to $0.00 and the interest rate to 0.0%.

    void update( );
    //Postcondition: One year of simple interest has been added to the account.
    void input( );
    void output( );
    double getBalance( );
    int getDollars( );
    int getCents( );
    double getRate( ); //Returns interest rate as a percentage.

    void setBalance(double balance);
    void setBalance(int dollars, int cents);
    //Checks that arguments are both negative or both nonnegative.

    void setRate(double newRate);
    //If newRate is nonnegative, it becomes the new rate. Otherwise, abort program.

private:
    //A negative amount is represented as negative dollars and negative cents.
    //For example, negative $4.50 sets accountDollars to -4 and accountCents to -50.
    int accountDollars; //of balance
    int accountCents;   //of balance
    double rate;        //as a percent
```
```
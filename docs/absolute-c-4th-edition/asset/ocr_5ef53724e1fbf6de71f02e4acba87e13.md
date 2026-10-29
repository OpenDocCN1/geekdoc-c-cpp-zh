pieces of data associated with it: the account balance, the interest rate for the account, and the term, which is the number of months until maturity. The first two items can be represented as values of type double, and the number of months can be represented as a value of type int. Display 6.1 shows the definition of a structure called CDAccountV1 that can be used for this kind of account. (The V1 stands for version 1. We will define an improved version later in this chapter.)

# Display 6.1 A Structure Definition (part 1 of 2)

```
//Program to demonstrate the CDAccountV1 structure type.
#include <iostream>
using namespace std;

//Structure for a bank certificate of deposit:
struct CDAccountV1
{
    double balance;
    double interestRate;
    int term;//months until maturity
};
```

An improved version of this structure will be given later in this chapter.

```
void getData(CDAccountV1 &theAccount);
//Postcondition: theAccount.balance, theAccount.interestRate, and //theAccount.term have been given values that the user entered at the keyboard.
```

```
int main()
{
    CDAccountV1 account;
    getData(account);

    double rateFraction, interest;
    rateFraction = account.interestRate/100.0;
    interest = account.balance*(rateFraction*(account.term/12.0));
    account.balance = account.balance + interest;

    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(2);
    cout << "When your CD matures in "
         << account.term << " months,\n"
         << "it will have a balance of $"
         << account.balance << endl;

    return 0;
}
```
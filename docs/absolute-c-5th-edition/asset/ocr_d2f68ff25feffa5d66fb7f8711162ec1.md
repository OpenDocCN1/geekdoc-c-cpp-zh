# Structures 241

Display 6.1 shows the definition of a structure called CDAccount for this kind of account. (The v1 stands for version 1. We will define an improved version later in this chapter.)

Display 6.1 A Structure Definition (part 1 of 2)

```
//Program to demonstrate the CDAccountV1 structure type.
#include <iostream>
using namespace;

//Structure for a bank certificate of deposit:
struct CDAccountV1
{
    double balance;
    double interestRate;
    int term; //months until maturity
}

void getData(CDAccountV1 &account);
//Postcondition: account.balance, account.interestRate, and
//account.term have been given values that the user entered at the
//keyboard.

int main() {
    CDAccountV1 account;
    getData(account);

    double rateFraction, interest;
    rateFraction = account.interestRate/100.0;
    interest = account.balance*(rateFraction*(account.term/12.0));
    account.balance = balance + interest;

    cout.set(ios::fixed);
    cout.set(ios::showpoint);
    cout.precision(2);
    cout << "When CD matures in "
         << account.term << " months,\n"
         << "it will have a balance of $$"
         << account.balance << endl;

    return 0;
}
//Uses iostream.
void getData(CDAccountV1 &account)
{
    cout << "Enter account balance: $$";
    cin >> account.balance;

```

An improved version of this structure will be given later in this chapter.

(continued)
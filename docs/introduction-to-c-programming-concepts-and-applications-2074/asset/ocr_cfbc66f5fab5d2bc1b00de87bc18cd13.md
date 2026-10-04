# // QUIZ

1 Match the idea to its name:

2 Imagine you have the following program and want to break it into several files, which will be compiled separately. Specifically, you would like to have: a library header file, a library implementation file, and a main file. Which of the code would end up in each of these files?

+   a top-down
b bottom-up
c separate compilation
d stub
namespace
affold

1 a way of building a program by combining existing, simpler parts

2 a way of writing a minimal function that it can be called when testing some other code

```
#include <iostream>
using namespace std;
bool update_balance(float& balance, float payment, float interest) {
    balance -= payment;
    if (balance <= 0) {
        return true;
    }
    balance *= (1.0+interest/100.0);
    return false;
}
int main() {
    float account_balance=1000.0;
    float payment = 50.0;
    float interest_rate = 3.5;
    int numpments = 1;
    while (update_balance(account_balance,payment,interest_rate)) {
        numpments++;
        payment += 10.0;
    }
    cout << "It takes " << numpments << " increasing payments to pay the balance in the account." << endl;
}
```

3 a way of setting up code so that a particular function can be tested

4 a way of grouping functions and variables with a common purpose

5 a way of dividing a program into multiple files

6 a way of dividing a problem into simpler subproblems
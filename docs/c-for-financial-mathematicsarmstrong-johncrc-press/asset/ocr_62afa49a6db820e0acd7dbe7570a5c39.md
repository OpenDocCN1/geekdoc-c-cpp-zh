# ## 1.2 Running an example program

Let us start with an example program.

Don’t worry what it does for now. The first thing we need to do is work out how to run it.

```
```
#include <iostream>
#include <cmath>
using namespace std;

int main() {
// Interesting code starts
int principal;
double interestRate;
int numberOfYears;

cout << "How much are you investing?\n";
cin >> principal;
cout << "What's the annual interest rate (%)?\n";
cin >> interestRate;
cout << "How long for (years)?\n";
cin >> numberOfYears;

double finalBalance =
pow(1.0 + interestRate * 0.01, numberOfYears)
* principal;
double interest = finalBalance - principal;

cout << "You will earn ";
cout << interest;
cout << "\n";
/* Interesting code ends */
return 0;
}
```
```

You can also find this code on the website of the book $^{3}$. Follow the link for the project “InterestCalculator” for Chapter 1.
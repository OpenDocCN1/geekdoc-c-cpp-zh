and product, and return these computed results to the calling routine. By naming the function calc() and providing five parameters (three for input data and two references for returned values), the following function can be used:

```
void calc(double n1, double n2, double n3, double& sum, double& product)
{
    sum = n1 + n2 + n3;
    product = n1 * n2 * n3;
    return;
}
```

This function has five parameters named n1, n2, n3, sum, and product. Only the last two are declared as references, so the first three arguments are passed by value and the last two arguments are passed by reference. In this function, only the last two parameters are altered. The value of the fourth parameter, sum, is calculated as the sum of the first three parameters, and the last parameter, product, is computed as the product of the parameters n1, n2, and n3. Program 6.9 includes this function in a complete program.

# Program 6.9

```
#include <iostream>
using namespace std;

void calc(double, double, double, double&, double&); // prototype

int main()
{
    double firstnum, secnum, thirdnum, sum, product;

    cout << "Enter three numbers: ";
    cin >> firstnum >> secnum >> thirdnum;

    calc(firstnum, secnum, thirdnum, sum, product); // function call

    cout << "\nThe sum of the numbers is: " << sum << endl;
    cout << "The product of the numbers is: " << product << endl;

    return 0;
}

void calc(double n1, double n2, double n3, double& sum, double& product)
{
```
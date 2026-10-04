# 328 Modularity Using Functions

naming the function calc() and providing five parameters (three for input data and two referenced for values), the following function can be used:

```
void calc(double num1, double num2, double num3, double& total, double& product)
{
    total = num1 + num2 + num3;
    product = num1 * num2 * num3;
    return;
}
```

This function has five parameters named num1, num2, num3, total, and product. Only the last two are declared as references, so the first three arguments are passed by value and the last two are passed by reference. In this function, only the last two parameters are altered. The value of the fourth parameter, total, is calculated as the sum of the first three parameters, and the last parameter, product, is computed as the complete product of the parameters num1, num2, and num3. Program 6.9 includes this function in a complete program.

![](bbox=[0.106, 0.423, 0.178, 0.458])

# Program 6.9

```
#include <iostream>
using namespace std;

void calc(double, double, double, double&, double&); // prototype

int main(){
    double first, secnum, third, sum, product;

    cout << "Enter three numbers: ";
    cin >> first >> secnum >> third;
    calc(first, secnum, third, sum, product); // function call
    cout << "\nThe sum of the numbers is: " << sum << endl;\n    cout << "The product of the numbers is: " << product << endl;

    return 0;
}

void calc(double num1, double num2, double num3, double& total, double& product)
{
    total = num1 + num2 + num3;
    product = num1 * num2 * num3;
    return;
}
```
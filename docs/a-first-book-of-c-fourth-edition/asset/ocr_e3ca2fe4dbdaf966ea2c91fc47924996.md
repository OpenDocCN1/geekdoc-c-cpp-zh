```
cout << "Enter a radius: ";
cin >> radius;
circum = 2.0 * 3.1416 * radius;
cout << "\nThe circumference of the circle is "
<< circum << endl;

return 0;
}
```

2. (Modify) Rewrite the following program to use the named constant FACTOR in place of the expression (5.0/9.0) used in the program:

```
#include <iostream>
using namespace std;

int main()
{
    double fahren, celsius;
    cout << "Enter a temperature in degrees Fahrenheit: ";
    cin >> fahren;
    celsius = (5.0/9.0) * (fahren - 32.0);
    cout << "The equivalent Celsius temperature is "
    << celsius << endl;

    return 0;
}
```

3. (Modify) Rewrite the following program to use the symbolic constant PRIME in place of the value 0.04 used in the program:

```
#include <iostream>
using namespace std;

int main()
{
    double prime, amount, interest;
    prime = 0.04;    // prime interest rate
    cout << "Enter the amount: ";
    cin >> amount;
    interest = prime * amount;
    cout << "The interest earned is "
    << interest << " dollars" << endl;

    return 0;
}
```
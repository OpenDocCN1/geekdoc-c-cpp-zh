# DISPLAY 5.2 void Functions (part 2 of 2)

```
using namespace std;
cout.setf(ios::fixed);
cout.setf(ios::showpoint);
cout.precision(1);
cout << fDegrees
    << " degrees Fahrenheit is equivalent to\n"
    << cDegrees << " degrees Celsius.\n";
return;  // This return is optional.
```

# Sample Dialogue

I will convert a Fahrenheit temperature to Celsius.
Enter a temperature in Fahrenheit: 32.5
32.5 degrees Fahrenheit is equivalent to
0.3 degrees Celsius.

# DISPLAY 5.3 Use of return in a void Function

# Function Declaration

```
void iceCreamDivision(int number, double totalWeight);
//Outputs instructions for dividing totalWeight ounces of
//ice cream among number customers.
//If number is 0, nothing is done.
```

# Function Definition

```
//Definition uses iostream:
void iceCreamDivision(int number, double totalWeight)
{
    using namespace std;
    double portion;
    if (number == 0)
        return;  // If number is 0, then the function execution ends here.
    portion = totalWeight/Number;
    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.precision(2);
    cout << "Each one receives "
         << portion << " ounces of ice cream." << endl;
}
```
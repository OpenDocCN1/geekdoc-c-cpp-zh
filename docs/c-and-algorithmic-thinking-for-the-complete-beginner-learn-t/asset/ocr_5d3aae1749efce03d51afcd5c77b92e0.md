```
```cpp
cout << "Enter the length of Radius: ";
cin >> radius;
area = PI * radius * radius;
cout << "The area of the circle is " << area;
return 0;
}
```
```

> **Notice:** Please note that the constant PI is declared outside of the function main.

# **Exercise 10.1-3**    *Calculating Fuel Economy*

In the United States, a car’s fuel economy is measured in miles per gallon, or MPG. A car’s MPG can be calculated using the following formula:

$$\mathrm{MPG}=\frac{\text{miles driven}}{\text{gallons of gas used}}$$

Write a C++ program that prompts the user to enter the total number of miles he or she has driven and the gallons of gas used. Then the program should calculate and display the car’s MPG.

# **Solution**

This is quite a simple case. The user enters the total number of miles he or she has driven and the gallons of gas used, and then the program should calculate and display the car’s MPG.

```
```cpp
#include <iostream>
using namespace std;
int main() {
    double gallons, miles_driven, mpg;

    cout << "Enter miles driven: ";
    cin >> miles_driven;
    cout << "Enter gallons of gas used: ";
    cin >> gallons;

    mpg = miles_driven / gallons;

    cout << "Your car's MPG is: " << mpg;
    return 0;
}
```
```

# **Exercise 10.1-4**    *Where is the Car? Calculating Distance Traveled*

A car starts from rest and moves with a constant acceleration along a straight horizontal road for a given time. Write a C++ program that prompts the user to enter
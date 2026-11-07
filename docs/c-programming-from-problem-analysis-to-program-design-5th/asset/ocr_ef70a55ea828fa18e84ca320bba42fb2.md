```
```cpp
u = u + static_cast<int>(2 * v + z);
a = u + v * z;
cout << "a = " << a << endl;
}
```
```

What is the output of the following function calls?

+   a. `defaultParam(6);`
+   
+   b. `defaultParam(3, 4);`
+   
+   c. `defaultParam(3, 0, 2.8);`

# PROGRAMMING EXERCISES

+   1. Consider the definition of the function `main`.

```
```cpp
int main()
{
    int x, y;
    char z;
    double rate, hours;
    double amount;
    .
    .
    .
}
```
```

The variables x, y, z, rate, and hours referred to in items a through below are the variables of the function main. Each of the functions described must have the appropriate parameters to access these variables. Write the following definitions:

+   a. Write the definition of the function `initialize` that initializes x and y to 0 and z to the blank character.
+   
+   b. Write the definition of the function `getHoursRate` that prompts the user to input the hours worked and rate per hour to initialize the variables hours and rate of the function main.
+   
+   c. Write the definition of the value-returning function `payCheck` that calculates and returns the amount to be paid to an employee based on the hours worked and rate per hour. The hours worked and rate per hour are stored in the variables hours and rate, respectively, of the function main. The formula for calculating the amount to be paid is as follows: For the first 40 hours, the rate is the given rate; for hours over 40, the rate is 1.5 times the given rate.
+   
+   d. Write the definition of the function `printCheck` that prints the hours worked, rate per hour, and the salary.
+   
+   e. Write the definition of the function `funcOne` that prompts the user to input a number. The function then changes the value of x by assigning the value of the expression 2 times the (old) value of x plus the value of y minus the value entered by the user.
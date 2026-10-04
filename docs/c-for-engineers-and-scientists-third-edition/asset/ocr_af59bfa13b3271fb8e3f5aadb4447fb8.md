# Chapter 4 207

# Nested if Statements

program is to treat the number entered as a temperature in degrees Celsius, convert the number to the equivalent degrees Fahrenheit, and display a suitable message. If the letter n f nor c, the program is to display a message that the data entered is incorrect and terminate. Use an if-else chain in your program to make use of these conversion formulas:

```
Celsius = (5.0 / 9.0) x (Fahrenheit - 32.0)
Fahrenheit = (9.0 / 5.0) * Celsius + 32.0
```

+   8. (Debugging) Using the relationships in Program 4.6, the following program calculates the digital output:

```
int main() {
    int digout;
    double inlbs;

    cout << "Enter the input weight: ";
    cin >> inlbs;

    if (inlbs >= 90) digout = 1111;
    if (inlbs >= 80 && (inlbs <= 90) digout = 1110;
    if (inlbs >= 70) && (inlbs <= 80) digout = 1101;
    if (inlbs >= 60) && (inlbs <= 70) digout = 1100;
    if (inlbs < 1000) digout = 1011;

    cout << "The digital output is " << digout << endl;

    return 0;
}
```

+   a. Will this program produce the same output as Program 4.6?

+   b. Which program is better and why?

+   9. (Debugging) The following program was written to produce the same result as Program 4.6:

```
int main() {
    int digout;
    double inlbs;

    cout << "Enter the input weight: ";
    cin >> inlbs;

    if (inlbs < 60)
        digout = 1011;
    else if (inlbs >= 60)
        digout = 1100;
    else if (inlbs > 70)
        digout = 1101;
    else if (inlbs >= 80)
        digout = 1110;
    else if (inlbs >= 90)
        digout = 1111;
```
```
switch (a) {
    case '0': case '2': case '4': case '6': case '8':
        cout << "is even\n";
        break;
    case '1': case '3': case '5': case '7': case '9':
        cout << "is odd\n";
        break;
    default:
        cout << "is not a digit\n";
        break;
}
```

The most common error with switch-statements is to forget to terminate a case with a break. For example:

```
int main()    // example of bad code (a break is missing)
{
    constexpr double cm_per_inch = 2.54; // number of centimeters in
                                           // an inch
    double length = 1;                    // length in inches or
                                           // centimeters
    char unit = 'a';
    cout << "Please enter a length followed by a unit (c or i)\n";
    cin >> length >> unit;

    switch (unit) {
    case 'i':
        cout << length << "in == " << cm_per_inch*length << "cm\n";
    case 'c':
        cout << length << "cm == " << length/cm_per_inch << "in\n";
    }
}
```

Unfortunately, the compiler will accept this, and when you have finished case 'i' you'll just “drop through” into case 'c', so that if you enter 2i the program will output

```
2in == 5.08cm
2cm == 0.787402in
```

You have been warned!
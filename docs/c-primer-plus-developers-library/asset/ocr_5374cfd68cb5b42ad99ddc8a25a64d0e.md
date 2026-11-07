```
```cpp
{
    using std::cout;
    float price1 = 20.40;
    float price2 = 1.9 + 8.0 / 9.0;

    cout << "\"Furry Friends\" is $" << price1 << "!\n";
    cout << "\"Fiery Fiends\" is $" << price2 << "!\n";

    cout.precision(2);
    cout << "\"Furry Friends\" is $" << price1 << "!\n";
    cout << "\"Fiery Fiends\" is $" << price2 << "!\n";

    return 0;
}
```
```

Here is the output of the program in Listing 17.6:

```
```text
"Furry Friends" is $20.4!
"Fiery Fiends" is $2.78889!
"Furry Friends" is $20!
"Fiery Fiends" is $2.8!
```
```

Note that the third line of this output doesn't include a trailing decimal point. Also the fourth line displays a total of two digits.

# Printing Trailing Zeros and Decimal Points

Certain forms of output, such as prices or numbers in columns, look better if trailing zeros are retained. For example, the output to Listing 17.6 would look better as $20.40 than as $20.4. The iostream family of classes doesn't provide a function whose sole purpose is to accomplish that. However, the ios_base class provides a setf() (for set flag) function that controls several formatting features. The class also defines several constants that can be used as arguments to this function. For example, the following function call causes cout to display trailing decimal points:

```
```cpp
cout.setf(ios_base::showpoint);
```
```

In the default floating-point format, it also causes trailing zeros to be displayed. That is, instead of displaying 2.00 as 2, cout will display it as 2.00000 if the default precision of 6 is in effect. Listing 17.7 adds this statement to Listing 17.6.

In case you're wondering about the notation ios_base::showpoint, showpoint is a class-scope static constant that is defined in the ios_base class declaration. Class scope means that you have to use the scope-resolution operator (::) with the constant name if you use the name outside a member function definition. So ios_base::showpoint names a constant defined in the ios_base class.
# STEP 5

When you change the value to anything above 30, then build and run the code, you can see that the only line to be outputted to the screen is the second cout statement, displaying the current value of num. This is because the initial if statement is False, so it ignores the code within the braces.

![](bbox=[0.067, 0.21, 0.491, 0.283])

# STEP 6

You can include an if statement within a do…while loop. For example:

```
```cpp
{
    float temp;

    do
    {
        cout << "\nEnter the temperature (or -10000 to exit): " << endl;
        cin >> temp;
        if (temp <= 0)
        {
            cout << "\nBrrrr, it's really cold!" << endl;
        }
        if (temp > 0)
        {
            cout << "\nAt least it's not freezing!" << endl;
        }
    }
    while (temp != -10000);

    cout << "\nGood bye\n" << endl;

    return 0;
}
```
```

![](bbox=[0.067, 0.673, 0.491, 0.953])

# STEP 7

The code in Step 6 is simplistic but effective. First we created a floating point integer called temp, then a do…while loop that asks the user to enter the current temperature.

![](bbox=[0.509, 0.183, 0.934, 0.248])

# STEP 8

The first if statement checks to see if the user’s inputted value is less than or equal to zero. If it is, then the output is ‘Brrr, it’s really cold!’. Otherwise, if the input is greater than zero, the code outputs ‘At least it’s not freezing!’.

![](bbox=[0.509, 0.333, 0.934, 0.438])

# STEP 9

Finally, if the user enters the value -10000, which is impossibly cold so is therefore a unrealistic value, the do…while loop is terminated and a friendly ‘Good bye’ is displayed to the screen.

![](bbox=[0.509, 0.519, 0.934, 0.69])

# STEP 10

Using if is quite powerful, if it’s used correctly. Just remember that if the condition is true then the code executes what’s in the braces. If not, it continues on its merry way. See what else you can come up with using if and a combination of loops.

![](bbox=[0.509, 0.779, 0.934, 0.953])
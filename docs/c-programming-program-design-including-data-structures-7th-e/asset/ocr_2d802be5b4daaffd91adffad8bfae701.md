```
int main()
{
    int dividend, divisor, quotient;                         //Line 1

    try                                                     //Line 2
    {
        cout << "Line 3: Enter the dividend: ";            //Line 3
        cin >> dividend;                                    //Line 4
        cout << endl;                                       //Line 5

        cout << "Line 6: Enter the divisor: ";             //Line 6
        cin >> divisor;                                     //Line 7
        cout << endl;                                       //Line 8

        if (divisor == 0)                                   //Line 9
            throw divisor;                                  //Line 10

        quotient = dividend / divisor;                      //Line 11

        cout << "Line 12: Quotient = " << quotient
             << endl;                                       //Line 12
    }
    catch (int x)                                           //Line 13
    {
        cout << "Line 14: Division by " << x
             << endl;                                       //Line 14
    }

    return 0;                                               //Line 15
}
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: 14

Line 6: Enter the divisor: 5

Line 12: Quotient = 2

**Sample Run 2:** In this sample run, the user input is shaded.

Line 3: Enter the dividend: 23

Line 6: Enter the divisor: 0

Line 14: Division by 0

This program works the same way as the program in Example 14–5.

The program in Example 14–7 illustrates how to handle division by zero, division by a negative integer, and input failure exceptions. It also shows how to throw and catch an object. This program is similar to the programs in Examples 14–5 and 14–6.
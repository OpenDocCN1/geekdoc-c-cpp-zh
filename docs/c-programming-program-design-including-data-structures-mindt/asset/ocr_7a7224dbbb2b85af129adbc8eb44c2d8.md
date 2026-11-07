```
```cpp
cout << "Enter temperature in Fahrenheit: ";    //Line 7
cin >> fahrenheit;                             //Line 8
cout << endl;                                  //Line 9

cout << "5 / 9 = " << 5 / 9
     << "; fahrenheit - 32 = "
     << fahrenheit - 32 << endl;               //Line 9a

celsius = 5 / 9 * (fahrenheit - 32);           //Line 10

cout << fahrenheit << " degree F = "
     << celsius << " degree C." << endl;       //Line 11

return 0;                                      //Line 12
}                                              //Line 13
```
```

**Sample Run:** In this sample run, the user input is shaded.

```
```text
Enter temperature in Fahrenheit: 110
5 / 9 = 0; fahrenheit - 32 = 78
110 degree F = 0 degree C.
```
```

Let us look at the sample run. We see that the value of 5 / 9 = 0 and the value of fahrenheit - 32 = 78. Because fahrenheit = 110, the value of the expression fahrenheit - 32 is correct. Now let us look at the expression 5 / 9. The value of this expression is 0. Because both of the operands, 5 and 9, of the operator / are integers, using integer division, the value of the expression is 0. That is, the value of the expression 5 / 9 = 0 is also calculated correctly. So by the precedence of the operators, the value of the expression 5 / 9 * (fahrenheit - 32) will always be 0 regardless of the value of fahrenheit. So the problem is in the integer division. We can replace the expression 5 / 9 with 5.0 / 9. In this case, the value of the expression 5.0 / 9 * (fahrenheit - 32) will be a decimal number. Because fahrenheit and celsius are int variables, we can use the cast operator to convert this value to an integer, that is, we use the following expression:

```
```cpp
celsius = static_cast<int> (5.0 / 9 * (fahrenheit - 32) + 0.5);
```
```

(Note that in the preceding expression, we added 0.5 to round the number to the nearest integer.)

The revised program is:

```
```cpp
#include <iostream>                         //Line 1

using namespace std;                         //Line 2

int main()                                    //Line 3
{
    int fahrenheit;                           //Line 5
    int celsius;                              //Line 6
```
```
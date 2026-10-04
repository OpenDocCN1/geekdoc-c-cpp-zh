# Chapter 7

# 379

One-Dimensional Arrays
The first temperature entered is stored in temp[0], the second temperature is entered stored in temp[1], and so until five temperatures have been entered.

One caution about storing data in an array: C++ does not check the value of the index being used (called a bounds check). If an array has been declared as consisting of 10 elements, for example, and if you use an index of 12, which is outside the bounds of the array, C++ will not notify you of the error when it is compiled. The program attempts to access index 12 by skipping the appropriate number of bytes from the start of the array. Usually, this attempt returns a value of the correct type, but simply overwrites the referenced memory locations. This leads to more errors, which are troublesome to locate when the value legitimately assigned to the storage location is at a different point in the program.

During output, an element can be displayed using a cout statement, or complete sections of the array can be displayed by including a cout statement in a loop. Both of these methods are shown:

```
cout << volts[6];

and

cout << "The value of element " << i << " is " << temp[i];

and

int NUMELS = 20;
for (int k = 5; k < NUMELS; k++)
cout << k << " " << amount[k] << endl;
```

The first statement displays the values of the subscribed variable volts[6]. The second statement displays the values of subscript i and temp[i]. Before this statement can be executed, it must have an assigned value. Finally, the last example includes a cout statement in a loop that displays the value of the index and the value of elements 5 to 20.
Program 7.1 illustrates these input and output techniques, using an array named temp defined to store five integer numbers. The program includes for two loops. The first loop is used to cycle through each array element and allows the user to input array values. After five values have been entered, the second loop is used to display the stored values.

# Program 7.1

```
#include <iostream>
using namespace std;

int main()
{
    const int MAXTEMPS = 5;
    int i, temp[MAXTEMPS];
```

![](bbox=[0.118, 0.713, 0.185, 0.763])
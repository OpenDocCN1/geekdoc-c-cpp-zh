would result in an input failure, because you are trying to input the character `W` into the `int` variable a. If the input were:

```
35 67.93 48
```

then the input statement:

```
cin >> a >> x >> b;
```

would result in storing 35 in a, 67.93 in x, and 48 in b.

Now consider the following read statement with the previous input (the input with three values):

```
cin >> a >> b >> c;
```

This statement stores 35 in a and 67 in b. The reading stops at . (the decimal point). Because the next variable c is of the data type `int`, the computer tries to read . into c, which is an error. The input stream then enters a state called the fail state.

What actually happens when the input stream enters the fail state? Once an input stream enters the fail state, all further I/O statements using that stream are ignored. Unfortunately, the program quietly continues to execute with whatever values are stored in variables and produces incorrect results. The program in Example 3–8 illustrates an input failure. This program on your system may produce different results.

# EXAMPLE 3-8

```
```cpp
//Input Failure program

#include <iostream>

using namespace std;

int main()
{
    int a = 10;                         //Line 1
    int b = 20;                         //Line 2
    int c = 30;                         //Line 3
    int d = 40;                         //Line 4

    cout << "Line 5: Enter four integers: ";       //Line 5
    cin >> a >> b >> c >> d;                      //Line 6
    cout << endl;                                  //Line 7
    cout << "Line 8: The numbers you entered are:" //Line 8
    cout << endl;
    cout << "Line 9: a = " << a << ", b = " << b
         << ", c = " << c << ", d = " << d << endl; //Line 9

    return 0;
}
```
```
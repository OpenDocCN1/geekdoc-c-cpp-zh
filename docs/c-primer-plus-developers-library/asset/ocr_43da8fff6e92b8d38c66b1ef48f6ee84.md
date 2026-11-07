By the way, if you want to display a value in hexadecimal or octal form, you can use some special features of cout. Recall that the iostream header file provides the endl manipulator to give cout the message to start a new line. Similarly, it provides the dec, hex, and oct manipulators to give cout the messages to display integers in decimal, hexadecimal, and octal formats, respectively. Listing 3.4 uses hex and oct to display the decimal value 42 in three formats. (Decimal is the default format, and each format stays in effect until you change it.)

# Listing 3.4 **hexoct2.cpp**

```
```cpp
// hexoct2.cpp -- display values in hex and octal
#include <iostream>
using namespace std;
int main()
{
    using namespace std;
    int chest = 42;
    int waist = 42;
    int inseam = 42;

    cout << "Monsieur cuts a striking figure!" << endl;
    cout << "chest = " << chest << " (decimal for 42)" << endl;
    cout << hex;      // manipulator for changing number base
    cout << "waist = " << waist << " (hexadecimal for 42)" << endl;
    cout << oct;      // manipulator for changing number base
    cout << "inseam = " << inseam << " (octal for 42)" << endl;
    return 0;
}
```
```

Here's the program output for Listing 3.4:

```
```
Monsieur cuts a striking figure!
chest = 42 (decimal for 42)
waist = 2a (hexadecimal for 42)
inseam = 52 (octal for 42)
```
```

Note that code like the following doesn't display anything onscreen:

```
```cpp
cout << hex;
```
```

Instead, it changes the way cout displays integers. Thus, the manipulator hex is really a message to cout that tells it how to behave. Also note that because the identifier hex is part of the std namespace and the program uses that namespace, this program can't use hex as the name of a variable. However, if you omitted the using directive and instead used std::cout, std::endl, std::hex, and std::oct, you could still use plain hex as the name for a variable.
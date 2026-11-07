The `ostream` class overloads the `<<` operator to make this usage equivalent to the function call `hex(cout)`. The manipulators are in the `std` namespace. Listing 17.3 illustrates using these manipulators. It shows the value of an integer and its square in three different number bases. Note that you can use a manipulator separately or as part of a series of insertions.

# Listing 17.3    **manip.cpp**

```
```cpp
// manip.cpp -- using format manipulators
#include <iostream>
int main()
{
    using namespace std;
    cout << "Enter an integer: ";
    int n;
    cin >> n;

    cout << "n        n*n\n";
    cout << n << "        " << n * n << " (decimal)\n";
// set to hex mode
    cout << hex;
    cout << n << "        ";
    cout << n * n << " (hexadecimal)\n";

// set to octal mode
    cout << oct << n << "        " << n * n << " (octal)\n";

// alternative way to call a manipulator
    dec(cout);
    cout << n << "        " << n * n << " (decimal)\n";

    return 0;
}
```
```

Here is some sample output from the program in Listing 17.3:

```
```text
Enter an integer: 13
n       n*n
13      169 (decimal)
d        a9 (hexadecimal)
15       251 (octal)
13      169 (decimal)
```
```
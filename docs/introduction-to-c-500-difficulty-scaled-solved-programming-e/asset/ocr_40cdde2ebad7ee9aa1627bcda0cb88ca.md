# 3 • Data Input/Output 39

Let's see an example:

```
#include <iostream> // Example 3.6
using namespace std;

int main()
{
    double i = 12.428, j = 5.67321;

    cout.precision(2);
    cout.width(7);
    cout.fill('*');
    cout << fixed << i << '\t' << j << '\n';
    return 0;
}
```

The program outputs: **12.43    5.67**. As you can see, the precision remains in effect for variables, while the width is applied only to display i.

# DATA INPUT WITH cin

In this section we will learn how to get data from an input stream, the keyboard, to use data in variables, and use it in our programs. For example, an input stream may be associated with a file on the hard disk, or a peripheral device (e.g., modem). cin is an object of the istream class. By default, the cin object is associated with the standard input device (e.g., keyboard). For those who know C, cin corresponds to stdin. The type of the variable after the >> determines the type of input data that will be read and stored in that variable. Just as the ostream class overloads the << operator, the istream class overloads the >> shift operator to read the data. When used in this way, the >> operator extracts the data from the input stream and stores it in the indicated variable. The >> suggests that the direction of data flow is from left to right. The istream class provides several functions to get the input data. For now, we will read numeric values and other types of (e.g., pointer) in the next chapters. Here, we'll see in Chapter 18, that we can use cin to get data for user types (e.g., class) in the same way we use with basic types (e.g.). Let's see an example:

```
#include <iostream> // Example 3.7
using std::cout;
using std::cin;
using std::fixed;
```

```
int main()
{
    int i;
    double j;

    cout << "Enter number: ";
    cin >> i; // Read an integer and store it into i.
    cout << "Enter number: ";
    cin >> j;

    cout << i << '  \t' << fixed << j << '\n';
    return 0;
}
```
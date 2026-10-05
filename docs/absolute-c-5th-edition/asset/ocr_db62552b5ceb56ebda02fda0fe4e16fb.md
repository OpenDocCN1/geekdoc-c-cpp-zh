# Programmer-Defined Functions

Display 3.6 The Function round (part 2 of 2)

```
do {
    cout << "Enter a double value: ";
    cin >> doubleValue;
    cout << "Rounded that number is " << round(doubleValue) << endl;\n    cout << "Again? (y/n): ";
    cin >> ans;
    while (ans == 'y' || ans == 'Y');
    cout << "End of testing.\\n";
}
return 0;
//cmath
int round(double number) {
    return static_cast<int>(floor(number + 0.5));
}
```

Sample Dialogue
Enter a double value: 9.6
Rounded, that number is 10
Again? (y/n): y
Enter a double value: 2.49
Rounded, that number is 2
Again? (y/n): n
End of testing.

# Self-Test Exercises

+   7. What is the output produced by the following program?

```
#include <iostream>
using namespace std;
char mystery(int firstParameter, int secondParameter);
int main() {
    cout << mystery(10, 9) << "ow\n";
    return 0;
}
```

(continued)
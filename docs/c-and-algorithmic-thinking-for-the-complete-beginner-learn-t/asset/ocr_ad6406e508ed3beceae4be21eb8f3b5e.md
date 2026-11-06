| Second digit = 7 | The second digit can be isolated if you divide the remaining digits by 100 to get the integer quotient digit2 = (int)(753 / 100) |
| --- | --- |
| Remaining digits = 53 | The remaining digits are now r = 753 % 100 |
| Third digit = 5 | The third digit can be isolated if you divide the remaining digits by 10 to get the integer quotient digit3 = (int)(53 / 10) |
| Fourth digit = 3 | The last remaining digit, which happens to be the fourth digit, is digit4 = 53 % 10 |

The C++ program that solves this algorithm is shown here.

```
```cpp
#include <iostream>
using namespace std;
int main() {
    int digit1, digit2, digit3, digit4, number, r, sum;

    cout << "Enter a four-digit integer: ";
    cin >> number;

    digit1 = (int)(number / 1000);
    r = number % 1000;

    digit2 = (int)(r / 100);
    r = r % 100;

    digit3 = (int)(r / 10);
    digit4 = r % 10;

    sum = digit1 + digit2 + digit3 + digit4;
    cout << sum;
    return 0;
}
```
```

The trace table for the program that you have just seen is shown here.

| Step | Statement | Notes | number | digit1 | digit2 | digit3 | digit4 | r | sum |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | cout << "Enter a ..." | The message "Enter a ..." is displayed | | | | | | | |
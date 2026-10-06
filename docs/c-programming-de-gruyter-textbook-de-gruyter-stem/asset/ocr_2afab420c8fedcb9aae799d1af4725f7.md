# 2.4 The Fundamental Control Structures of Algorithms 57

![](bbox=[0.111, 0.083, 0.75, 0.305])

of the integer, and then its tens, its hundreds.... We can divide the integer by 10 continuously until the quotient is 0. This is a loop process, and no matter which integer it is, we have to output at least one digit (even if it is 0). Therefore we can use a do-while loop structure: first execute the loop body and then evaluate the loop condition.

Source code:

```
//2_6.cpp
#include <iostream>
using namespace std;
int main() {
    int n, right_digit, newnum = 0;
    cout << "Enter the number: ";
    cin >> n;

    cout << "The number in reverse order is ";
    do {
        right_digit = n % 10;
        cout << right_digit;
        n /= 10;
    }
    while (n != 0);
    cout<<endl;
}
```

Result:

| Enter the number: 365
The number in reversed digit order is 563 |
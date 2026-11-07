```
5 / 2 = 2
14 / 7 = 2
34 % 5 = 4
4 % 6 = 4
```

> **NOTE**  
> You should be careful when evaluating the mod operator with negative integer operands. You might not get the answer you expect. For example, −34 % 5 = −4, because in the division −34 / 5, the quotient is −6 and the remainder is −4. Similarly, 34 % −5 = 4, because in the division −34 / 5, the quotient is −6 and the remainder is 4. Also, −34 % −5 = −4, because in the division −34 / −5, the quotient is 6 and the remainder is −4.

The following example shows how arithmetic operators work with floating-point numbers.

# EXAMPLE 2-4

The following C++ program evaluates various floating-point expressions. (The details of how the expressions are evaluated are left as an exercise for you.)

```
```cpp
// This program illustrates how floating-point expressions
// are evaluated.

#include <iostream>

using namespace std;

int main()
{
    cout << "5.0 + 3.5 = " << 5.0 + 3.5 << endl;
    cout << "3.0 + 9.4 = " << 3.0 + 9.4 << endl;
    cout << "16.3 - 5.2 = " << 16.3 - 5.2 << endl;
    cout << "4.2 * 2.5 = " << 4.2 * 2.5 << endl;
    cout << "5.0 / 2.0 = " << 5.0 / 2.0 << endl;
    cout << "34.5 / 6.0 = " << 34.5 / 6.0 << endl;
    cout << "34.5 / 6.5 = " << 34.5 / 6.5 << endl;

    return 0;
}
```
```

**Sample Run:**

```
5.0 + 3.5 = 8.5
3.0 + 9.4 = 12.4
16.3 - 5.2 = 11.1
4.2 * 2.5 = 10.5
5.0 / 2.0 = 2.5
34.5 / 6.0 = 5.75
34.5 / 6.5 = 5.30769
```
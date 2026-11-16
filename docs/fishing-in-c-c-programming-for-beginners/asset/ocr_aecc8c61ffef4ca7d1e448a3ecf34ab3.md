# Bitwise XOR operator

^ is the bitwise XOR operator.This operator returns zero if

| x | y | x^y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    int a=9,b=5;
    int c=a^b;
    cout<<c;
}
```

Here, the output will be 12.

a=9=1001,b=5=101
So, c=a^b=1001^101
=1001^0101
=1100
=12
So, a&b= 1001&101
=1001&0101
=0001
=1

# Bitwise OR operator

| is used for bitwise OR operation. It returns one when anyone of all the inputs given is one. If none of the input given is one then it returns zero.

| x | y | x|y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

This fact can be illustrated from the following program

```
#include<iostream>
using namespace std;
int main()
{
    int a=9,b=5;
    int c=a|b;
    cout<<c;
    return 0;
}
```

Here, output will be 13.

Since, a=9=1001 ; b=5=101
a|b=1001|101
=1001|0101
=1101
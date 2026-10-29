# Display 13.4 Evaluating the Recursive Function Call power(2, 3)

# SEQUENCE OF RECURSIVE CALLS

# HOW THE FINAL VALUE IS COMPUTED

power(2, 0) *2

power(2, 1) *2

power(2, 2) *2

power(2, 3)

Start Here

1

*2

1*2 is 2

2

*2

2*2 is 4

4

*2

4*2 is 8

8

power(2, 3) is 8

```
if (n <= 1)
    return 1;
else
    return ( mystery(n - 1) + n );
}
```

13. What is the output of the following program? What well-known mathematical function is rose?

```
#include <iostream>
using std::cout;
using std::endl;

int rose(int n);
//Precondition: n >= 0.

int main()
{
    cout << rose(4) << endl;
```
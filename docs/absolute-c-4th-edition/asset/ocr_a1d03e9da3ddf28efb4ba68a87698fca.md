resumes the suspended computation. The resumed computation determines the final value for `power(2, 1)` from the above return statement as follows:

`power(2, 0) * 2 is 1*2, which is 2.`

Thus, the final value returned for `power(2, 1)` is 2. So, the following would set the value of `result4` equal to 2:

```
int result4 = power(2, 1);
```

Larger numbers for the second argument will produce longer chains of recursive calls. For example, consider the statement

```
cout << power(2, 3);
```

The value of `power(2, 3)` is calculated as follows:

```
power(2, 3) is power(2, 2)*2
    power(2, 2) is power(2, 1)*2
        power(2, 1) is power(2, 0)*2
            power(2, 0) is 1 (stopping case)
```

When the computer reaches the stopping case `power(2, 0)`, there are three suspended computations. After calculating the value returned for the stopping case, it resumes the most recently suspended computations to determine the value of `power(2, 1)`. After that, the computer completes each of the other suspended computations, using each value computed as a value to plug into another suspended computation, until it reaches and completes the computation for the original call, `power(2, 3)`. The details of the entire computation are illustrated in Display 3.4.

# Self-Test Exercises

+   12. What is the output of the following program?

```
#include <iostream>
using std::cout;
using std::endl;

int mystery(int n);
//Precondition: n >= 1.

int main()
{
    cout << mystery(3) << endl;
    return 0;
}

int mystery(int n)
{

```
```
return 0;
}
```

Ans. The output of the preceding program is as follows:

```
First value ≡ A
Second value ≡ U
Third value ≡ U
Fourth value ≡ U
```

# Q11. What will be the output of the following program?

```
#include <iostream.h>
#define PI 3.14
#define circumference(a) (2*PI*a)

int main()
{
    double p= PI;
    double result;
    cout << " Value of p is " << p << endl;
    result = circumference(4);
    cout << " Value of function macro is " << result << endl;
    return 0;
}
```

Ans. The output of the preceding program is as follows:

```
Value of p is 3.14
Value of function macro is 25.12
```

# Q12. What will be the output of the following program?

```
#include <iostream.h>

int main()
{
    double value1, value2;
    value1= 12 + 24 / 6;
    value2= 24 - 3 / 6;
    cout << "The value of value1 is " << value1 << endl;
    cout << "The value of value2 is " << value2 << endl;
    return 0;
}
```

Ans. The output of the preceding program is as follows:

```
The value of value1 is ≡ 16
The value of value2 is ≡ 12
```
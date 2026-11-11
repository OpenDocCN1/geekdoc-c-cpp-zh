```
```cpp
student Johnny;

Johnny.standard="8";
Johnny.roll_num=22;

cout << "The student is in " << Johnny.standard<<" standard."<<endl;
cout << "The roll number of the student is " << Johnny.roll_num <<endl;
return 0;
}
```
```

Ans. The output of the preceding program is as follows:

The student is in 8 standard.
The roll number of the student is 22

# **Q4.** What will be the output of the following program?

```
```cpp
#include <iostream.h>

int main()
{
    union example
    {
        double num;
        double num2;
    };
    example numbers;
    numbers.num= 10.2665;

    cout << "The value of the numbers.num is: " << numbers.num << endl;
    cout << "The value of the numbers.num2 is: " << numbers.num2 << endl;
    return 0;
}
```
```

Ans. The output of the preceding program is as follows:

The value of the numbers.num is: 10.2665
The value of the numbers.num2 is: 10.2665

# **Q5.** What will be the output of the following program?

```
```cpp
#include <iostream.h>

int main()
{
    int x = 10, y = 3, sum, sub, mul;
    sum = x + y;
    sub = x - y;
    mul = x * y;
    cout << "Addition of " << x << " and " << y << " is: " << sum << endl;
```
```
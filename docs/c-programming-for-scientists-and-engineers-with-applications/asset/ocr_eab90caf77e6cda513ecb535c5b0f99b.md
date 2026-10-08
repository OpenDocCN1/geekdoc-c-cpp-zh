```
sumk += k;
printf("In func sumk = %d\n", sumk);
}
```

The numbered lines are executed in the following order with the following effect on storage allocation:

+   1  i, sum exists, sumk is nonexistent;
3  i, sum exists but are suspended, sumk exists with default value 0;
2  i, sum exists but is suspended;
3  i, sum are suspended, sumk is reactivated; and
2  i, sum are reactivated, sumk exists but is suspended.

The output is as follows:

```
In func sumk = 0
In main sum = 0
In func sumk = 1
In main sum = 1
In func sumk = 3
In main sum = 3
```

Notice that sumk is automatically initialized to zero in the function when it is declared. It is updated using the values of i. Since it is a static variable it will stay updated until the program terminates. The effect is to calculate ((0 + 0) + 1) + 2.

static Variable Global to Several Functions

```
#include <stdio.h>

int func1();
int func2();

int main()
{
    int i, sum;
    for (i = 0; i < 3; i++) {
        sum = func1();
        printf("In main sum = %d\n", sum);
        sum = func2();
        printf("In main sum = %d\n", sum);
    }
```
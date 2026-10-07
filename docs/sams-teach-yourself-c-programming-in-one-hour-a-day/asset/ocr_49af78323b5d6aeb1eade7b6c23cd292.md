# Answers for Lesson 5

```
1: #include <stdio.h>
2:
3: int main( void )
4: {
5:     int number1 = 10,
6:     number2 = 5;
7:     int x, y, z;
8:
9:     x = product(number1, number2);
10:    y = divide_em(number1, number2);
11:    z = divide_em(number1, 0);
12:
13:    printf("%nnumber1 is %d and number2 is %d", x);
14:    printf("%nnumber1 / number2 is %d", y);
15:    printf("%nnumber1 / 0 is %d", z);
16:
17:
18:    return 0;
19: }
```

10. The code is as follows:

```
/* Averages five float values entered by the user. */

#include <stdio.h>

float v, w, x, y, z, answer;

float average(float a, float b, float c, float d, float e);

int main( void )
{
    puts("Enter five numbers:");
    scanf("%f%f%f%f%f", &v, &w, &x, &y, &z);

    answer = average(v, w, x, y, z);

    printf("The average is %f.\n", answer);

    return 0;
}

float average(float a, float b, float c, float d, float e)
{
    return ((a+b+c+d+e)/5);
}
```

11. The following is the answer using type int variables. It can run only with values less than or equal to 9. To use values larger than 9, you need to change the values to type long.
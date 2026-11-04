```
for(; ++i;)
    printf("\n%d ", i);
return 0;
}
```

Answer: The first loop ends when i && i-1 becomes false. This happens once i becomes 1. Therefore, the loop executes twice and the program outputs 3 and 2. Let's see the second loop. The expression ++i is equivalent to ++i != 0. Does this expression ever become 0? Yes, since the type of i is unsigned char, once it becomes 255 the next increment makes it 0. Therefore, the second loop outputs the values of i from 2 up to 255.

# C.6.13 Write a program that reads two integers and displays the sum of the integers between them. For example, if the user enters 3 and 8, the program should display 22 because 4+5+6+7 = 22. The program should check which one of the two input numbers is the greater and act accordingly.

```
#include <stdio.h>
int main(void)
{
    int i, j, sum;

    printf("Enter numbers: ");
    scanf("%d%d", &i, &j);

    sum = 0;
    if(i < j)
    {
        for(i = i+1; i < j; i++)
            sum += i;
    }
    else if(j < i)
    {
        for(j = j+1; j < i; j++)
            sum += j;
    }
    printf("Sum = %d\n", sum);
    return 0;
}
```

# C.6.14 Write a program that reads the grades of 100 students and displays the average of the passed students and the average of the failed students, before it ends. A student passes the exams with a grade equal to or greater than 5. The program should force the user to enter grades within [0, 10]. If the user enters -1, the insertion of grades should end.

```
#include <stdio.h>
int main(void)
{
    int i, suc, fail;
    float grd, sum_suc, sum_fail;

    suc = fail = 0;
    sum_suc = sum_fail = 0;
```
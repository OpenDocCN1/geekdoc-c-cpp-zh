```
k++;
}
if(b >= 1 && b <= 2)
{
    sum += b;
    k++;
}
if(c >= 1 && c <= 2)
{
    sum += c;
    k++;
}
if(k != 0)
    return sum/k;
else
    return -1;
}
```

# C.11.8 What is the output of the following program?

```
#include <stdio.h>

void test(int *ptr1, int *ptr2);

int main(void)
{
    int i = 10, j = 20;
    test(&i, &j);
    printf("%d %d\n", i, j);
    return 0;
}

void test(int *ptr1, int *ptr2)
{
    int m, *tmp;
    tmp = ptr1;
    ptr1 = &m;
    *ptr1 = 100;
    *ptr2 += m;
    ptr2 = tmp;
    *ptr2 = 100;
}
```

Answer: When test() is called, we have ptr1 = &i and ptr2 = &j. The statements ptr1 = &m; and *ptr1 = 100; make m equal to 100. Since ptr2 points to the address of j, *ptr2 is 20. Therefore, the statement *ptr2 += m; makes j equal to 20+100 = 120. Since tmp points to the address of i, the statement ptr2 = tmp; is equivalent to ptr2 = &i. Therefore, the statement *ptr2 = 100; changes the value of i to 100. As a result, the program outputs: 100 120
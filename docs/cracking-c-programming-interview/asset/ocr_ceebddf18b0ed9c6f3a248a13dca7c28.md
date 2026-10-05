```
ptr = str;
ptr++;
**ptr;
printf("%s", ptr);
}
```

+   (a) Imdia

+   (b) Jndia

+   (c) mdia

+   (d) odia

# 17. Determine the output of the following program if the base address of an array is 1000.

```
#include<stdio.h>
void fun(int arr[])
{
    printf("%u %u %u", *(arr+2)+1, (*arr)+2, *
(((*arr)+1)+1));
}
int main()
{
    int a[][3] = {5, 6, 7, 8, 9, 4, 3, 2, 1};
    fun(&a);
    return 0;
}
```

# 18. What is the output of the following program?

```
#include<stdio.h>
int main()
{
    int a[][2][4] = {5, 6, 7, 8, 9, 11, 12, 1};
    printf("&d ", *(*(a+0))+1)+2);
    return 0;
}
```

+   (a) 11
```
int *endptr = &array1[10];
for(ip1 = &array1[0]; ip1 < endptr; ip1++)
*ip2++ = *ip1;
```

As we mentioned, there is no element array1[10], but it is legal to compute a pointer to this (nonexistent) element, as long as we only use it in pointer comparisons like this (that is, as long as we never try to fetch or store the value that it points to.)

# Prorgam 8.3: In the following program, two different pointer variables point to the first and the last element of an integer array.

```
#include<stdio.h>
main()
{
int *px, *py;
int a[5]={1, 2, 3, 4, 5};
px=&a[0];
py=&a[4];
printf("px=%u py=%u", px, py);
printf("\n\n py-px=%u", py-px);
}
```

Execute this program and observe the result.

# 8.3.3 Similarities between Pointers and One-dimensional Arrays

There are a number of similarities between arrays and pointers in C. If you have an array

```
int a[10];
```

you can refer to a[0], a[1], a[2], etc., or to a[i] where i is an int. If you declare a pointer variable ip and set it to point to the
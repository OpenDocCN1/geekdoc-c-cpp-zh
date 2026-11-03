Inside func() : sizeof(a) = 2
Inside func() : sizeof(*a) = 8
Contents of array after calling func() are -
13 14 15 16
17 18 19 20
21 22 23 24

![](bbox=[0.08, 0.28, 0.95, 0.65])

# 8.19 Array Of Pointers

We can declare an array that contains pointers as its elements. Every element of this array is a pointer variable that can hold address of any variable of appropriate type. The syntax of declaring an array of pointers is similar to that of declaring arrays except that an asterisk is placed before the array name.

datatype *arrayname[size];

For example to declare an array of size 10 that contains integer pointers we can write-
int *arrp[10];

```
/*P8.23 Program for understanding the concept of array of pointers*/
#include<stdio.h>
main()
{
    int *pa[3];
    int i,a=5,b=10,c=15;
    pa[0]=&a;
    pa[1]=&b;
    pa[2]=&c;
    for(i=0;i<3;i++)
    {
        printf("pa[%d] = %u\t",i,pa[i]);
        printf("*pa[%d] = %d\n",i,*pa[i]);
    }
}
```

Output:

pa[0] = 2012    *pa[0] = 5
pa[1] = 2560    *pa[1] = 10
pa[2] = 3020    *pa[2] = 15
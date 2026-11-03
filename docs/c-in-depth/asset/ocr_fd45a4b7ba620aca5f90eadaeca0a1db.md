![](bbox=[0.15, 0.07, 0.9, 0.22])

# (c) pi = pi-3;

Now pi contains address 1000, and if dereferenced it will return information stored at bytes 1000 and 1001.

![](bbox=[0.15, 0.4, 0.9, 0.52])

# (d) printf("%d", *(pi+2) );

Here the pointer will not move to address 1004 since we have not assigned any new value to it. The integer stored at bytes 1004 and 1005 will be printed.

![](bbox=[0.15, 0.7, 0.9, 0.82])

It is important to note that when we move a pointer somewhere else in memory by incrementing/decrementing or adding/subtracting integers then it not necessary that the pointer still points to a variable of same data type or a valid memory location. The task of allocating memory locations to variables is done by the compiler. We don't know where and in what order it has stored them. We should take care that we move the pointers in such a way that they always point to valid memory locations. In case of arrays, elements are stored in consecutive order. So this arithmetic is generally applied in arrays.

```
/*P8.4 Program to show pointer arithmetic*/
#include<stdio.h>
main()
{
 int a=5,*pi=&a;
 char b='x',*pc=&b;
 float c=5.5,*pf=&c;
 printf("Value of pi = Address of a = %u\n",pi);
 printf("Value of pc = Address of b = %u\n",pc);
 printf("Value of pf = Address of c = %u\n",pf);
 pi++;
 pc++;
 pf++;
 printf("Now value of pi = %u\n",pi);
 printf("Now value of pc = %u\n",pc);
 printf("Now value of pf = %u\n",pf);
}
```

# Output:

Value of pi = Address of a = 1000
# 6.3.1. Addition

The addition operation can be performed effectively using pointers in a way that addition of a number to a pointer is possible.

+   - Example:
+   ```
+   #include<stdio.h>
+   void main()
+   {
+   int i=4,*x,*y;
+   x=&i;
+   y=x+9;
+   printf("%d",y);
+   }
+   ```

The above example is a rough program. You can see that x and y are declared as pointer variables and i is initialized to 4. The next step being that the address of i is assigned to x and the value of x is added 9 and placed in the variable y which is printed in the next line. In a similar way, subtraction using pointers can also be accomplished. y=x-9;

# 6.3.2. Pointer Comparison

The comparison between pointer variable can be done provided both the variables point to the objects of same data type. Such comparisons can be useful when both pointer variables point to the elements of the same array. The comparison can test for either equality or inequality and also a Pointer variable can be compared with zero.

The program below gives us a description of how its is carried out.

```
#include<stdio.h>
void main()
{
static int sub[]={10,20,30,40,50,60};
int *a,*b; a=&sub[4]; b=(sub+4);
if(a==b)
printf("pointers point to the same location.");
else
```
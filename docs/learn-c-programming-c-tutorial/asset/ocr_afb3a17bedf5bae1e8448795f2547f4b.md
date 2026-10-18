If you want to return a single-dimension array from a function, you would have to declare a function returning a pointer as in the following example:

```
int * myFunction()
{




}

```

Second point to remember is that C does not advocate to return the address of a local variable to outside of the function, so you would have to define the local variable as static variable.

Now, consider the following function which will generate 10 random numbers and return them using an array and call this function as follows:

```
#include <stdio.h>

/* function to generate and return random numbers */
int * getRandom( )
{
static int r[10];
int i;

/* set the seed */
srand( (unsigned)time( NULL ) );
for ( i = 0; i < 10; ++i)
{
r[i] = rand();
printf( "r[%d] = %d\n", i, r[i]);
}

return r;
}
/* main function to call above defined function */
```

![](bbox=[0.127, 0.9435, 0.3755, 0.9825])
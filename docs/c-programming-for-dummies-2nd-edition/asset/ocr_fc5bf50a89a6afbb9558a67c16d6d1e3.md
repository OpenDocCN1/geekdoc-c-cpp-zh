```
```c
#include <stdio.h>

int main()
{
    int prime;

    prime = 701;
    printf("Shadrach is %d\n",prime);
    prime = 709;
    printf("Meshach is %d\n",prime);
    prime = 719;
    printf("Abednego is %d\n",prime);
    return(0);
}
```
```

Exercise 6-10: Create new source code from Listing 6-6. As you can see, the variable prime is used over and over, each time changing its value. The new value that's assigned replaces any existing value. Build and run the project.

The output from Exercise 6-10 is the same as from Exercise 6-9.

Listing 6-7 illustrates how variables can interact with each other.



```
```c
#include <stdio.h>

int main()
{
    int a,b,c;

    a = 5;
    b = 7;
    c = a + b;
    printf("Variable c=%d\n",c);
    return(0);
}
```
```

Line 9 is the one to notice:

> c = a + b;
```
int *ip3;
ip3 = &i;
```

Don't write

```
int *ip3;
*ip3 = &i;
```

or you'll be trying to mix pointer and the value to which it points Also, when we write
int *ip;

although the asterisk affects ip's type, it goes with the identifier name ip, not with the type int on the left. To declare two pointers at once, the declaration looks like
int *ip1, *ip2;

Some people write pointer declarations like this:
int* ip;

This works for one pointer, because C essentially ignores whitespace. But if you ever write
int* ip1, ip2; /* PROBABLY WRONG */

it will declare one pointer-to-int ip1 and one plain int ip2, which is probably not what you meant.

What is all of this good for? If it was just for changing variables like i from 5 to 7, it would not be good for much. What it's good for, among other things, is when for various reasons we don't know exactly which variable we want to change.

# Program 8.1: A simple program to illustrate the relationship between two integer variables, their corresponding addresses and their associated pointers.

```
#include<stdio.h>
main()
```
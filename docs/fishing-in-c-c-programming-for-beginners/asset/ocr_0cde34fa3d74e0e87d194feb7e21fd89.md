# # Pointers

This part includes two special symbols & and *

& - It is called address of variable.

Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    int a=5;
    cout<<&a;
    return 0;
}
```

Here, it will display the memory address of variable stored. Output depends on compilers, in my compiler it displayed 0x22fe4c. In yours, it may be different.

* Asterisk, also called value at the address of is used to access the value stored at the address of a variable.

A pointer may be declared as

```
int *a;
```

Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    int *a;
    cout<<*a;
    return 0;
}
```

In this program, we have not assigned any address to a, but we are trying to access the value stored at that address. This simply crashes the program with the following output:
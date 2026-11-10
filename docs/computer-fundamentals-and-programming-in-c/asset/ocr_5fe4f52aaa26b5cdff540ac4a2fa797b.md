The second declaration makes the object that it points at read-only and of course, both the object and what it points at might be constant. Because we have declared the value pointed to by `ptr` to be `const`, the compiler will check for any statements that attempt to modify the value pointed to by `ptr` and flag such statements as error. For example, the following statement will now result in an error message from the compiler:

```
```c
*p = 100; /* ERROR */
```
```

As the declaration asserted that what `ptr` points to must not be changed. But the following assignment is valid.

```
```c
n = 50;
```
```

The value pointed to has changed but here it was not tried to use the pointer to make the change. Of course, the pointer itself is not constant, so it is always possible to change what it points to:

```
```c
int v = 100;
ptr = &v;  /* OK - changing the address in ptr */
```
```

This will change the address stored in `ptr` to point to the variable `v`.

It is to be noted that the following declarations are equivalent.

```
```c
const int *ptr=&n;
int const *ptr=&n;
```
```

# 13.20.2 Constant Pointers

Constant pointers ensure that the address stored in a pointer cannot be changed. Consider the following statements:

```
```c
int n = 10;
int *const ptr = &n;  /* Defines a constant */
```
```

Here is how one could ensure that a pointer always points to the same object; the second statement declares and initializes `ptr` and indicates that the address stored must not be changed.

Any attempt to change what the pointer points to elsewhere in the program will result in an error message when you compile:

```
```c
int v = 5;
ptr = &v;  /* Error - attempt to change a constant
              pointer */
```
```

It is still legitimate to change the value that `ptr` points to using `ptr` though:

```
```c
*ptr = 100;     /* OK - changes the value of v */
```
```

This statement alters the value stored in `v` through the pointer and changes its value to 100.

You can create a constant pointer that points to a value that is also constant:

```
```c
int n = 25;
const int *const ptr = &n;
```
```

`ptr` is a constant pointer to a constant so everything is fixed. It is not legal to change the address stored in `ptr` as well as `ptr` cannot be used to modify what it points to.

# 13.20.3 Constant Parameters

Recall that arrays are passed to functions by address and it is also known that function implementations can alter the original array’s contents. To prevent an array argument from being altered in a function, use the `const` qualifier as demonstrated in the following programs.

*Version 1*

```
```c
#include <stdio.h>
void change(char *);
int main(void)
{
    char s[]="Siva";
    change(s);
    printf("\n The string after calling change():\n%s", s);
    return 0;
}
void change(char *t)
{
    *t='V';
}
```
```

# Output

The string after calling change():Viva

*Version 2*

```
```c
#include <stdio.h>
void change(const char *);
int main(void)
{
    char s[]="Oxford University";
    change(s);
    printf("\n The string after calling change():\n%s", s);
    return 0;
}
void change(const char *t)
{
    *t='V';
}
```
```

![](bbox=[0.665, 0.735, 0.793, 0.784])

# Output

Compiler error: Assignment of read-only location

The same error will occur when the following program is compiled.

```
```c
#include <stdio.h>
void change(const int [], int);
```
```
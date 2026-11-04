```
```c
int x = 7;
int *p = &x;
```
```

The reason for the restriction is that pointers may only be used to access other data in your program. The compiler is allowed to assume that your program is correct and pointers always refer to valid data. The compiler is allowed to optimize your code based on this assumption; if you violate this rule then your program may crash.

Another point to keep in mind: using a pointer allows you to modify the data it points to by altering the contents of the given memory address. Here is an example:

```
```c
// x is initially 7
int x = 7;

// p points to the location of x
int *p = &x;

// update the contents of x via p
*p = 1234;

// x is now equal to 1234!
```
```

# **const Pointers**

A constant pointer, sometimes referred to as "pointer to const," is a pointer which cannot be used to modify the data it points to, an example of which is here:

```
```c
const char *name_ptr = "Test";
```
```

If we put the const after the *, then the meaning of the const changes. If the declaration begins with "char * const" then the pointer can never be modified to point to
# Pointer Traps

Pointer variables give the programmer great flexibility, but they can lead to difficult to find and correct errors in your programs. We will examine the common problems and give hints about how to avoid them.

Let's assume the following type and variable declarations:

```
int *first = NULL;
int *second;
int *third;
int num = 4;
```

We also assume that the following code has been executed:

```
second = new int;
*second = 2;
```

# Dereferencing NULL

It is an error to dereference NULL. This is the safest error to make, since the system will usually catch the error at run time.

```
cout << *first << endl; // Error, first is NULL
```

It is just as much a problem to dereference NULL with the -> operator in the case that your type is a class or struct. A NULL pointer does not point to anything. Dereferencing obtains the pointer points to.

# Dangling Pointer

It is an error to dereference a pointer that has not been correctly given a value. This error will probably cause an eventual crash, but usually after running incorrectly for a while.

```
cout << *third << endl; // Error, third has no value
```
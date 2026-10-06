```
int intval = 255958283;
void *vptr = &intval;
```

```
printf("The value at vptr as an int is %d\n", ((int*) vptr));
printf("The value at vptr as a char is %d\n", ((char*) vptr));
```

Initialise the void pointer vptr to point to an integer variable intval.
In the first printf statement, we insert (int *) in front of vptr before we dereference
it using *. This casts vptr to an integer pointer, and so the value of intval is printed as
an integer.

In the second printf statement, we insert (char *) in front of vptr before we
dereference it. This casts vptr to a char pointer, and so what's printed is the value of the char
which makes up the first part of intval.

# # What do you use pointers?

That's all there is to pointers, other than to ask why bother? We can already access
a variable with a name, so why do we need to have some complicated alternative way of
getting to the contents of a variable

There are several ways in which pointers are useful, which we will explore in more detail in
l chapters. But a few of the important ones are:

+   - function calls - in the next chapter we will look at how to split C code into functions; pointers are very useful for allowing a function to return multiple values.
- string handling - in C, a string is a continuous block of memory with a letter stored in each byte; pointers make it possible to perform efficient operations on strings.
- arrays - in C, an array variable can be used to store a list of values of the same type, which like a string is stored in a continuous block of memory; pointers make accessing arrays easier or more efficient.

> > INCREMENTING POINTERS
You can use ++ and -- on pointers, but you need to be careful! (*a)) increments the value pointed to by a, but * ((a)) increments the pointer itself rather than the value it points at -
this will move a to point at the memory address immediately after a
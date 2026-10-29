# Pointer Types

There is a bit of an inconsistency (or at least a potential for confusion) in how C++ names pointer types. If you want a parameter whose type is, for example, a pointer to variables of type int, then the type is written int*, as in the following example:

```
void manipulatePointer (int* p);
```

If you want to declare a variable of the same pointer type, the * goes with the variable, as in the following example:

```
int *p1, *p2;
```

In fact, the compiler does not care whether the * is attached to the int or the variable name, so the following are also accepted by the compiler and have the same meanings:

```
void manipulatePointer (int* p); //Accepted but not as nice.
int* p1, *p2; //Accepted but possibly confusing.
```

However, we find the first versions to be clearer. In particular, note that when declaring variables there must be one * for each pointer variable.

This code will output the following to the screen:

```
42
42
```

As long as p1 contains a pointer that points to v1, then v1 and *p1 refer to the same variable. So when you set *p1 equal to 42, you are also setting v1 equal to 42.

The symbol & that is used to obtain the address of a variable is the same symbol that you use in function declarations to specify a call-by-reference parameter. This is not a coincidence. Recall that a call-by-reference argument is implemented by giving the address of the argument to the calling function. So, these two uses of the symbol & are very closely related, although they are not exactly the same.

You can assign the value of one pointer variable to another pointer variable. For example, if p1 is still pointing to v1, then the following will set p2 so that it also points to v1:

```
p2 = p1;
```

Provided we have not changed v1’s value, the following will also output 42 to the screen:

```
cout << *p2;
```

Be sure you do not confuse

```
p1 = p2;
```

and

```
*p1 = *p2;
```

pointers in assignment statements
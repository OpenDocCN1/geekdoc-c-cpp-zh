initializer lists is described in §12.2.3 and the ways of passing arguments to template functions in §23.5.2 and §28.6.2.

# 12.2.1 Reference Arguments

Consider:

```
void f(int val, int& ref)
{
++val;
++ref;
}
```

When f() is called, ++val increments a local copy of the first actual argument, whereas ++ref increments the second actual argument. Consider:

```
void g()
{
int i = 1;
int j = 1;
f(i,j);
}
```

The call f(i,j) will increment j but not i. The first argument, i, is passed by value; the second argument, j, is passed by reference. As mentioned in §7.7, functions that modify call-by-reference arguments can make programs hard to read and should most often be avoided (but see §18.2.5). It can, however, be noticeably more efficient to pass a large object by reference than to pass it by value. In that case, the argument might be declared a const reference to indicate that the reference is used for efficiency reasons only and not to enable the called function to change the value of the object:

```
void f(const Large& arg)
{
// the value of “arg”cannot be changed
// (except byusing explicit type conversion; §11.5)
}
```

The absence of const in the declaration of a reference argument is taken as a statement of intent to modify the variable:

```
void g(Large& arg); // assume that g() modifies arg
```

Similarly, declaring a pointer argument const tells readers that the value of an object pointed to by that argument is not changed by the function. For example:

```
int strlen(const char *); // number of characters in a C-style string
char* strcpy(char* to, const char* from); // copy a C-style string
int strcmp(const char*, const char*); // compare C-style strings
```

The importance of using const arguments increases with the size of a program.

Note that the semantics of argument passing are different from the semantics of assignment. This is important for const arguments, reference arguments, and arguments of
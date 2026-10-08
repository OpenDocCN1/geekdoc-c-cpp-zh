Note that even though the compiler will allow an argument of the wrong type to be passed, such as a `char*` to a parameter of type `int`, the use of such an argument of a wrong type is an error. As Dennis Ritchie said, “C is a strongly typed, weakly checked, programming language.”

# **27.2.3 Function definitions**

You can define functions exactly as in C++ and such definitions are function prototypes:

```
```
double square(double d)
{
    return d*d;
}

void ff()
{
    double x = square(2);    /* OK: convert 2 to 2.0 and call */
    double y = square();     /* argument missing */
    double y = square("Hello"); /* error: wrong argument type */
    double y = square(2,3);  /* error: too many arguments */
}
```
```

A definition of a function with no arguments is not a function prototype:

```
```
void f() { /* do something */ }

void g()
{
    f(2); /* OK in C; error in C++ */
}
```
```

Having

```
```
void f();  /* no argument type specified */
```
```

“f() can take any number of arguments of any type” seemed really strange. In response, I invented a new notation where “nothing” was explicitly stated using the keyword `void` (`void` is a four-letter word meaning “nothing”):

```
```
void f(void);  /* no arguments accepted */
```
```
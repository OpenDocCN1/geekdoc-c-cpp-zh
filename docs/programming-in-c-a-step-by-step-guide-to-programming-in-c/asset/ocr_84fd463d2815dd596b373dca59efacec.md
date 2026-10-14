There is a basic difference between the simple replacement discussed above and the replacement of macros with arguments. Subsequent occurrence of a macro with arguments is known as a *macro call*. When a macro is called, the preprocessor substitutes the *string*, replacing the formal parameters with actual parameters.

A simple example of a macro with arguments is

```
#define CUBE(x) (x*x*x)
```

If the following statement appears later in the program

```
volume=CUBE(side);
```

then the preprocessor would expand this statement to:

```
volume=(side*side*side);
```

Consider the following statement:

```
volume=CUBE(a+b);
```

This would expand to:

```
volume=(a+b*a+b*a+b);
```

which would obviously not produce the correct results. This is because the preprocessor performs a blind text substitution of the argument a+b in place of x. This shortcoming can be corrected by using parentheses for each occurrence of a formal argument in the *string*.

Example:

```
#define CUBE(x) ((x)*(x)*(x))
```

This would result in correct expansion of CUBE(a+b) as shown below: volume=((a+b)*(a+b)*(a+b));

Some commonly used definitions are:

```
#define MAX(a,b) (((a) > (b))?(a):(b))
#define MIN(a,b) (((a) < (b))?(a):(b))
```
As we mentioned, these prototypes help to ensure that the compiler can generate correct code for calling the functions, as well as allowing the compiler to catch certain mistakes you might make.

In general terms, a function prototype can be written as

```
data-type name(type1, type2, ..., type n)
```

Examples:

int sample(int, int) or int sample(int a, int b);

float fun(int, float) or float fun( int a, float b);

void demo(void); Here void indicates function neither return any value to the caller nor it has any arguments.

If you write the function definition after the definition of its caller function, then the prototype is required in the caller, but the prototype is optional if you write the definition of the function before the definition of the caller function. But it is good programming practice to include the function prototype wherever it is defined.

If prototypes are a good idea, and if we're going to get in the habit of writing function prototype declarations for functions we call that we've written (such as multbyfour), what happens for library functions such as printf? Where are their prototypes? The answer is in that boilerplate line

```
#include <stdio.h>
```

we've been including at the top of all of our programs. stdio.h is conceptually a file full of external declarations and other information pertaining to the “Standard I/O” library functions, including printf. The #include directive arranges all of the declarations within stdio.h that are considered by the compiler, rather as if we'd typed them all in ourselves. Somewhere within these declarations is an external function prototype declaration for printf, which satisfies the rule
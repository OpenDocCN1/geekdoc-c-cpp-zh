# Chapter 32. Types Part V: Compound Literals and Generic Selections

```
}
```

This outputs:

```
i is type int
l is type long
f is type float
d is type double
c is type something else
```

Which should be no surprise, because, like we said, that code in main() is replaced with the following
it is compiled:

```
printf("i %s\n", "int");
printf("l %s\n", "long");
printf("f %s\n", "float");
printf("d %s\n", "double");
printf("c %s\n", "something else");
```

And that's exactly the output we see.

Let's do one more. I've included some macros so that when you run:

```
int i = 10;
char *s = "Foo";
PRINT_VAL(i);
PRINT_VAL(s);
```

you get the output:

```
i = 10
s = Foo!
```

We'll have to make use of some macro magic to do that.

```
#include <stdio.h>
#include <string.h>
```

```
// Macro that gives back a format specifier for a type
#define FMTSPEC(x) _ \
int: "%d", \ \
long: "%ld", \ \
float: "%f", \ \
double: "%f", \ \
char: "%s", \ \
// TODO: add more types
```

```
// Macro that prints a variable in the form "name = value"
#define PRINT_VAL(x) do {
char fmt[512]; \
printf(fmt, sizeof(fmt), "#x = %s\n", FMTSPEC(x)); \ \
printf(fmt, (x)); \
} while(0)
```

```
int main(void)
{
	int i = 10;
	float f = 3.14159;
```
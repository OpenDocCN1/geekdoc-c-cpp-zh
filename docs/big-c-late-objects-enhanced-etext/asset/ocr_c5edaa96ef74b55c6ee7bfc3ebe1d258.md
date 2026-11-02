# Local Variables

Do not define all local variables at the beginning of a block. Define each variable just before it is used for the first time.

Every variable must be either explicitly initialized when defined or set in the immediately following statement (for example, through a >> instruction).

```
int pennies = 0;
```

or

```
int pennies;
 cin >> pennies;
```

Move variables to the innermost block in which they are needed:

```
while ( . . . )
{
    double xnew = (xold + a / xold) / 2;
    . . .
}
```

Do not define two variables in one statement:

```
int dimes = 0, nickels = 0; // Don't
```

When defining a pointer variable, place the * with the type, not the variable:

```
Link* p; // OK
```

not

```
Link *p; // Don't
```

Use auto only with types that are complex and not very informative, such as iterators.

For example, prefer

```
unordered_map<string, int> scores = . . ;
 auto pos = scores.find("Harry");
```

over

```
unordered_map<string, double>::iterator pos = scores.find("Harry");
```

# Constants

In C++, do not use #define to define constants:

```
#define CLOCK_RADIUS 5 // Don't
```

Use const instead:

```
const double CLOCK_RADIUS = 5; // The radius of the clock face
```
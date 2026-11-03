that scope.

As we mentioned in the start, Information can be passed into a
function two ways: by

use of external variables and use of the parameter mechanism.
Although there are

exceptions, it is preferred to use the second method for this purpose
because it leads to

better modularity and conciseness of code. Using external variables
carelessly may often

result in surprises and magic. Global variables cascade their change
throughout the

program, which clearly can be harmful for your logic. The message
or parameter passing

technique is free from these hazards since changes are localized.
Programs are therefore,

easier to write and maintain. All functions have external storage
class. This means that

we can use the keyword extern in function definitions and in function
prototypes. For

example:

```
extern double sum(double a, double b);
```

# 3.4.3 Storage Class register

The register storage class makes variables to work as high speed
register. Obviously, it
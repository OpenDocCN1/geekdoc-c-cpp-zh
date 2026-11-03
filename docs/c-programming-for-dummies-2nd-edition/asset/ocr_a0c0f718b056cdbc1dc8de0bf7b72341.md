Because the variable was declared as *static*, its value is retained between function calls.

+   - As a bonus, *static* variable declarations are initialized to zero.
+   - The keyword *static* defines a storage class. See the nearby sidebar, "Variable keyword roundup."
+   - You need not declare variables as *static* unless their values must be retained each time the function is called. This situation crops up from time to time. Also refer to the later section "Using external variables."
+   - Values returned from a function need not be declared *static*. When you return a value, such as

```
return(a);
```

only the variable's value is returned, not the variable itself. The only challenge with this approach occurs when allocating memory as the buffer. The buffer's data is discarded and should be declared *static* if you want the calling function to access it. See Chapter 19.

# Variables, Variables Everywhere

Sometimes, a variable must be like cellular phone service: available everywhere and accessed from any function. Often referred to as a *global* variable, in C it's officially known as an external variable.

# Using external variables

External variables solve specific problems by making the variable declaration available to all functions in the source code file. Any function can access the variable. It doesn't have to be passed to or returned from a function.

Listing 16-6 shows how external variables are declared and used. The variables *age* and *feet* are external. Both are used in, and manipulated by, all functions in the source code.
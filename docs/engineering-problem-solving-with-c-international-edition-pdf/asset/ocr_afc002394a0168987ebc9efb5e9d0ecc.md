Step 3:
integer a [5] <------- [ ] integer a
integer b [10] <------ [ ] integer b

Step 4:
integer a [5] <------- [ ] integer a
integer b [10] <------ [ ] integer b
             [5] integer hold

Step 5:
integer a [10] <------ [ ] integer a
integer b [10] <------ [ ] integer b
             [5] integer hold

Step 6:
integer a [10] <------ [ ] integer a
integer b [5] <------- [ ] integer b
             [5] integer hold

Step 7:
integer a [10]
integer b [5]
Function variables are released.

Step 8:
All memory is released.

Recall that function arguments and formal parameters must agree in order, type and number, but the names do not have to be the same. In the above example we chose to use the same identifiers for the function arguments and the formal parameters. This is allowable because the identifiers are defined within different statement blocks. However, it is important to realize that a and b defined in the main function occupy different memory locations than a and b defined in the function header. Function arguments that correspond to pass by reference parameters must be variables, since their values can be modified. Constants and expressions cannot be passed as arguments to pass-by-reference parameters.

# Modify!

+   1. Modify the driver program developed in the previous section by adding the following function call:

```
swapIntegers(10, 5):
```

What results do you see when you attempt to compile and execute the program? Explain.
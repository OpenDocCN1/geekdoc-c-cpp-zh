Note that the static variable, `staticVar`, is initialized once and keeps its value between function calls.

So a static variable is a variable that is only seen within the function in which it is defined (like a local variable) but whose lifetime is that of the entire program (like a global variable).

# Initializing Arrays In Static Storage

C does not allow for the initialization of automatic (local) arrays. Only static or external arrays may be initialized with a list of values. Therefore, to initialize an array, it's best to declare the array as `static`.

If a static array is used within a function, then the initial values will be assigned to the array only once. Any changes made to the array elements will remain in effect throughout the execution of the program.

Here are some examples of initializing arrays in static storage:

```
static short digits[10] = { 0,1,2,3,4,5,6,7,8,9 };
static char msg[6] = "Hello";
```

Note that a character string always includes a null terminator (`\0`) at the end.

If the array bound is greater than the number of initializers, the extra elements are initialized to 0. If no bound is given, the bound is taken to be the number of initializers.

Note that static and external variables that are not initialized will automatically be initialized to 0. Automatic and register variables that are not initialized will have unpredictable results!
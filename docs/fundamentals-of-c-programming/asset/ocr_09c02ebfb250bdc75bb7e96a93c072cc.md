will result in an error because the prototype for sqrt specifies only one numeric parameter, not two.

Some functions do not accept parameters; for example, the C++ function to generate a pseudorandom number, rand, is called with no arguments:

```
std::cout << rand() << '\n';
```

The rand function returns an int value, but the caller does not pass the function any information to do its task. The rand prototype is

```
int rand()
```

Notice the empty parentheses that indicate this function does not accept any parameters.

Unlike mathematical functions that must produce a result, C++ does not require a function to return a value to its caller. The C++ function exit expects an integer value from the caller, but it does not return a result back to the caller. A prototype for a function that returns nothing uses void as the return type, as in:

```
void exit(int);
```

The exit function immediately terminates the program's execution. The integer argument passed to exit is returned to the operating system which can use the value to determine if the program terminated normally or due to an error. C++ programs automatically return zero when main finishes executing—no exit call is necessary.

Note that since exit does not return a value to the caller, code such as

```
std::cout << exit(8) << '\n'; // Illegal!
```

will not compile since the expression exit(8) evaluates to nothing, and the std::cout stream object requires an actual value of some kind to print. A void function is useful for the side effects it produces instead a value it computes. Example side effects include printing something on the console, sending data over a network, or animating a graphical image.

# 8.2 Standard Math Functions

The cmath library provides much of the functionality of a scientific calculator. Table 8.1 lists only a few of the available functions.
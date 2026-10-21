You have chosen the function name to reflect the particular task in hand, which is OK for two functions, but you may also need the same function for several other types of argument. It seems a pity that you have to keep inventing names. Ideally, you would use the same function name `max()` regardless of the argument type, and have the appropriate version executed. It probably won’t be any surprise to you that you can indeed do this, and the C++ mechanism that makes it possible is called **function overloading**.

# What Is Function Overloading?

Function overloading allows you to use the same function name for defining several functions as long as they each have different parameter lists. When the function is called, the compiler chooses the correct version for the job based on the list of arguments you supply. Obviously, the compiler must always be able to decide unequivocally which function should be selected in any particular instance of a function call, so the parameter list for each function in a set of overloaded functions must be unique. Following on from the `max()` function example, you could create overloaded functions with the following prototypes:

```
int max(int array[], int len);             // Prototypes for
long max(long array[], int len);            // a set of overloaded
double max(double array[], int len);        // functions
```

These functions share a common name, but have a different parameter list. In general, overloaded functions can be differentiated by having corresponding parameters of different types, or by having a different number of parameters.

Note that a different return type does not distinguish a function adequately. You can’t add the following function to the previous set:

```
double max(long array[], int len);       // Not valid overloading
```

The reason is that this function would be indistinguishable from the function that has this prototype:

```
long max(long array[], int len);
```

If you define functions like this, it causes the compiler to complain with the following error:

```
error C2556: 'double max(long [],int)' : overloaded function differs only by return
type from 'long max(long [],int)'
```

and the program does not compile. This may seem slightly unreasonable, until you remember that you can write statements such as these:

```
long numbers[] = {1, 2, 3, 3, 6, 7, 11, 50, 40};
int len = sizeof numbers/sizeof numbers[0];
max(numbers, len);
```

The fact that the call for the `max()` function doesn’t make much sense here because you discard the result does not make it illegal. If the return type were permitted as a distinguishing feature, the compiler would be unable to decide whether to choose the version with a long return type or a double return type in the instance of the preceding code. For this reason the return type is not considered to be a differentiating feature of overloaded functions.
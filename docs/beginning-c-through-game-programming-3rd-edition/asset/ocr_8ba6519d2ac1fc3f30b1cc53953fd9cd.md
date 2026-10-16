# Specifying Default Arguments

The function askNumber() has two parameters—high and low. You can tell this from the function prototype:

```
int askNumber(int high, int low = 1);
```

Notice that the second parameter, low, looks like it’s assigned a value. In a way, it is. The 1 is a default argument meaning that if a value isn’t passed to low when the function is called, low is assigned 1. You specify default arguments by using = followed by a value after a parameter name.

# Trap

Once you specify a default argument in a list of parameters, you must specify default arguments for all remaining parameters. So the following prototype is valid:

```
void setDisplay(int height, int width, int depth = 32, bool fullScreen = true);
```

while this one is illegal:

```
void setDisplay(int width, int height, int depth = 32, bool fullScreen);
```

By the way, you don’t repeat the default argument in the function definition, as you can see in the function definition of askNumber().

```
int askNumber(int high, int low)
```

# Assigning Default Arguments to Parameters

The askNumber() function asks the user for a number between an upper and a lower limit. The function keeps asking until the user enters a number within the range, and then it returns the number. I first call the function in main() with:

```
int number = askNumber(5);
```

As a result of this code, the parameter high in askNumber() is assigned 5. Because I don’t provide any value for the second parameter, low, it gets assigned the default value of 1. This means the function prompts the user for a number between 1 and 5.

# Trap

When you are calling a function with default arguments, once you omit an argument, you must omit arguments for all remaining parameters. For example, given the prototype

```
void setDisplay(int height, int width, int depth = 32, bool fullScreen = true);
```
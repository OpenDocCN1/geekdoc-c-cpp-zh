# Chapter 5

You have two choices when entering the command-line arguments. After you build the example in the IDE, you can open a command window at the folder containing the .exe file and then enter the program name followed by the command-line arguments. Alternatively, you can specify the command-line arguments in the IDE before you execute the program. Just open the project properties window by selecting Project > Properties from the main menu and then extend the Configuration Properties tree in the left pane by clicking the plus sign (+). Click the Debugging folder to see where you can enter command line values in the right pane.

Here is some typical output from this example entered in a command window:

```
C:\Visual C++ 2005\Examples\Ex5_09 trying multiple "argument values" 4.5 0.0
argc = 6
Command line arguments received are:
argument 1: Ex5_09
argument 2: trying
argument 3: multiple
argument 4: argument values
argument 5: 4.5
argument 6: 0.0
```

# How It Works

The program first output the value of argc and then the values of each argument from the argv array in the for loop. You could make use of the fact that the last element in argv is null and code the output of the command line argument values like this:

```
int i = 0;
while(argv[i] != 0)
    cout << "argument " << (i+1) << ": " << argv[i++] << endl;
```

The while loop ends when argv[argc] is reached because that element is null.

# Accepting a Variable Number of Function Arguments

You can define a function so that it allows any number of arguments to be passed to it. You indicate that a variable number of arguments can be supplied when a function is called by placing an ellipsis (which is three periods, . . .) at the end of the parameter list in the function definition. For example:

```
int sumValues(int first,...)
{
    //Code for the function
}
```

There must be at least one ordinary parameter, but you can have more. The ellipsis must always be placed at the end of the parameter list.

Obviously there is no information about the type or number of arguments in the variable list, so your code must figure out what is passed to the function when it is called. The native C++ library defines va_start, va_arg, and va_end macros in the stdarg.h header to help you do this. It’s easiest to show how these are used with an example.
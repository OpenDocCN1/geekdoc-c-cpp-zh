# Functions 259

+   - The function has been defined in the program before the function call is encountered.

+   - The value returned by the function has been declared before the function call is encountered. Declaring the return and argument types for a function is known as a prototype declaration.

The function declaration not is only used to declare the function's return type, but is also used to tell the compiler how many arguments the function takes and what their types are. This is analogous to declaring methods inside the @interface section when defining a new class.

To declare absoluteValue as a function that returns a value of float and takes a single argument, also of type float, you could use the following prototype declaration:

```
float absoluteValue(float);
```

As you can, you have to specify the argument type inside the parentheses, and its name. You can optionally specify a "dummy" name after the type, if you like:

```
float absoluteValue(float x);
```

This name doesn't have to be the same as the one used in the function definition—the compiler ignores it anyway.

A foolproof way to write a prototype declaration is to simply make a copy of the first line from the actual definition of the function. Remember to place a semicolon at the end. If the function takes a variable number of arguments (such as is the case with NSLog and scanf), the compiler must be informed. The declaration

```
void NSLog(NSString *format, ...);
```

ells the compiler that NSLog takes an NSString object as its first argument and is followed by any number of additional arguments (the use of ...). NSLog is declared in the special file <Foundation/Foundation.h>, which is one reason why you have been placing the following line at the start of each of your programs:

```
#import <Foundation/Foundation.h>
```

Without this result, the compiler can assume that NSLog takes a fixed number of arguments, which can result in incorrect code being generated.

The compiler automatically converts your numeric arguments to the appropriate types when a function is called only if you have placed the function's definition or have declared the function and its argument types before the call.

> ¹ Technically speaking, it is defined in the file NSObjectRuntime.h, which is imported from inside the file Foundation.h
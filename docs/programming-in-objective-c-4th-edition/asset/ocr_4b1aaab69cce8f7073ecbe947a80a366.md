will warn you that the return type defaults to int, which is an indication that you're doing something wrong!

The default return type for functions differs from that for methods. Recall that, if no return type is specified for a method, the compiler assumes that it returns a value of type id. Again, you should always declare the return type for a method instead of relying on this fact.

# Declaring Return Types and Argument Types

We mentioned earlier that the Objective-C compiler assumes that a function returns a value of type int as the default case. More specifically, whenever a call is made to a function, the compiler assumes that the function returns a value of type int unless either of the following has occurred:

+   * The function has been defined in the program before the function call is encountered.
* The value returned by the function has been declared before the function call is encountered. Declaring the return and argument types for a function is known as a prototype declaration.

The function declaration is not only used to declare the function's return type, but it is also used to tell the compiler how many arguments the function takes and what their types are. This is analogous to declaring methods inside the @interface section when defining a new class.

To declare absoluteValue as a function that returns a value of type float that takes a single argument, also of type float, you could use the following prototype declaration:

```
float absoluteValue (float);
```

As you can see, you have to specify just the argument type inside the parentheses, not its name. You can optionally specify a “dummy”
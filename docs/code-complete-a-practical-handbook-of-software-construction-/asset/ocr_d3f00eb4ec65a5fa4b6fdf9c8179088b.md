# Use named parameters

In some languages, you can explicitly associate formal parameters with actual parameters. This makes parameter usage more self-documenting and helps avoid errors from mismatching parameters. Here’s an example in Visual Basic:

```
Visual Basic Example of Explicitly Identifying Parameters
Private Function Distance3d(
    ByVal xDistance As Coordinate, _
    ByVal yDistance As Coordinate, _
    ByVal zDistance As Coordinate _
)
    ...
End Function
...
Private Function Velocity(
    ByVal latitude as Coordinate, _
    ByVal longitude as Coordinate, _
    ByVal elevation as Coordinate _
)
    ...
    Distance = Distance3d( xDistance := latitude, yDistance := longitude, _
        zDistance := elevation )
    ...
End Function
```

This technique is especially useful when you have longer-than-average lists of identically typed arguments, which increases the chances that you can insert a parameter mismatch without the compiler detecting it. Explicitly associating parameters may be overkill in many environments, but in safety-critical or other high-reliability environments the extra assurance that parameters match up the way you expect can be worthwhile.

# Make sure actual parameters match formal parameters

Formal parameters, also known as “dummy parameters,” are the variables declared in a routine definition. Actual parameters are the variables, constants, or expressions used in the actual routine calls.

A common mistake is to put the wrong type of variable in a routine call—for example, using an integer when a floating point is needed. (This is a problem only in weakly typed languages like C when you’re not using full compiler warnings. Strongly typed languages such as C++ and Java don’t have this problem.) When arguments are input only, this is seldom a problem; usually the compiler converts the actual type to the formal type before passing it to the routine. If it is a problem, usually your compiler gives you a warning. But in some cases, particularly when the argument is used for both input and output, you can get stung by passing the wrong type of argument.

Develop the habit of checking types of arguments in parameter lists and heeding compiler warnings about mismatched parameter types.
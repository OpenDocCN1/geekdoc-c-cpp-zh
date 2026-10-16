```
(DEFINE (function_name parameters)
    (expression)
)
```

Of course, this form of DEFINE is the definition of a named function.

The following example call to DEFINE binds the name square to a functional expression that takes one parameter:

```
(DEFINE (square number) (* number number))
```

After the interpreter evaluates this function, it can be used, as in

```
(square 5)
```

which displays 25.

To illustrate the difference between primitive functions and the DEFINE special form, consider the following:

```
(DEFINE x 10)
```

If DEFINE were a primitive function, EVAL's first action on this expression would be to evaluate the two parameters of DEFINE. If x were not already bound to a value, this would be an error. Furthermore, if x were already defined, it would also be an error, because this DEFINE would attempt to redefine x, which is illegal. Remember, x is the name of a value; it is not a variable in the imperative sense.

Following is another example of a function. It computes the length of the hypotenuse (the longest side) of a right triangle, given the lengths of the two other sides.

```
(DEFINE (hypotenuse side1 side2)
    (SQRT (+ (square side1) (square side2))))
```

Notice that hypotenuse uses square, which was defined previously.

# 15.5.5 Output Functions

Scheme includes a few simple output functions, but when used with the interactive interpreter, most output from Scheme programs is the normal output from the interpreter, displaying the results of applying EVAL to top-level functions.

Note that explicit input and output are not part of the pure functional programming model, because input operations change the program state and output operations have side effects. Neither of these can be part of a pure functional language. Therefore, this chapter does not describe the explicit input or output functions of Scheme.
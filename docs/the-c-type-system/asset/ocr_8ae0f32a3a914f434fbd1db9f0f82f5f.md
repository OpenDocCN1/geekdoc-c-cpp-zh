change, but the names we use *matter*. While the use of v for *velocity* is common, speed is a more accurate description of this value’s purpose. *Velocity* is a technical term with a specific meaning in physics; it represents *both* magnitude (speed) and direction. If we name code elements as accurately and properly as we can, we reduce the risk of those names being misunderstood.

Selecting good names is a first step toward making code clearer and easier to read. However, we can do much more to improve our code’s clarity and remove ambiguity about what those identifiers represent. We might reasonably ask, for example, in what units the angle, speed, and elapsedTime parameters are measured. We’ll address that later in the chapter, but first we need a more sophisticated mechanism than the double type allows.

# Adding Clarity Through Types

All the Displacement method’s parameters are of the same type: double. This makes it easy for anyone, including ourselves, to accidentally mix up argument values when calling the method—without any warning from the compiler.

The double type itself is not the specific culprit here; we’d have the same problem if the parameters were all string or all bool types. Even if each parameter were of a different built-in numeric type, plenty of potential for problems would still remain because of the presence of the implicit promotion rules between them. Moreover, clarifying the parameter names doesn’t necessarily help the calling code, especially if the method is called with plain constant values like so:

```
var result = Displacement(.523, 65, 4);
```

Hard-coded values such as those used in this example are called *magic numbers* because there’s no explanation of their meaning or purpose. We could replace the magic numbers with better-named variables to make their purpose clearer, but the caller of the method might still supply the arguments in the wrong order.

One common way for the calling code to address such out-of-order errors is to specify the parameter name for each argument. Let’s see that in practice before looking at how to use different types to distinguish between the argument values.

# Named Arguments

Embedding the parameter name for each argument being passed to a method makes the purpose of those arguments much more visible in the calling code, as shown here:

```
var result = Displacement(angle: .523, speed: 65, elapsedTime: 4);
```
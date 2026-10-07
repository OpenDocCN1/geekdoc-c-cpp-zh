because that a basic attribute of a rectangle. Only the class' accessor methods should be able to set or retrieve that origin. That's consistent with the notion of data encapsulation.
But how do you release the memory used by your origin? Releasing the rectangle object's memory does not release the memory allocated for the origin. It will release the reference to that object's data, but not the data itself. One way to release the memory is to insert a line such as the following main:

```
[[myRect origin]];
```

This releases the XYPoint object that the origin method returns. You must do this before you release the memory for the Rectangle object itself because the variables contained in an object is valid after an object's memory is released. So the correct code sequence would be as follows:

```
[[myRect origin]]; // Release the origin's memory
[myRect release]]; // Release the rectangle's memory
```

It's a bit of a burden to have to remember the origin's memory yourself. After all, you weren't the one who allocated it; the Rectangle class did. In the next section, Overriding Methods," you will learn how to have the Rectangle class release the memory.
With your modified method, recompiling and running Program 8.5 produces the error messages shown as Figure 8.8.

![](bbox=[0.263, 0.488, 0.735, 0.568])

Figure 8.8 Compiler error messages

Oops! The problem here is you've referenced some instance variables from the XYPoint class in your modified method, so now the compiler needs more information about it than the @class directive provides. In this case, you must go back to your Rectangle.h header file and replace that directive with an import instead, like so:
#import "XYPoint."

# Program 8.5B Output

```
Origin at (100, 200)
Origin at (100, 200)
```

That's better. Time, changing the value of myPoint to (50, 50) inside main had no effect on the rectangle's origin because a copy of the point was created inside the Rectangle's setOrigin:method.
Incidentally, we didn't synthesize the origin methods here because the synthesized setOrigin:method would have behaved just like the you originally wrote. That
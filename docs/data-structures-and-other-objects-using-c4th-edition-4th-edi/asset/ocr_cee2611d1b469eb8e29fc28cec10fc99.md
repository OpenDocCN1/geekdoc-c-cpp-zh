original value in the calling program. Therefore, the complete output from the code is:

```
x coordinate is 6 y coordinate is -4
Rotations: 3
x coordinate is 6 y coordinate is -4
```

The value of the argument, sample, did not change.

# Value Parameters

A **value parameter** is declared by writing the type name followed by the parameter name. With a value parameter, the argument provides the initial value for the formal parameter. The value parameter is implemented as a local variable of the function, so that any changes made to the parameter in the body of the function will leave the argument unaltered.

Example:
`int rotations_needed(point p);`

**Reference parameters.** _Reference parameters_ are important types of parameters in C++. Our example of a reference parameter is similar to the rotations_needed function. But this time the point p will be a reference parameter. The new function does not return a value; it merely rotates p into the upper-right quadrant, as shown here:

```
void rotate_to_upper_right(point& p)
// Postcondition: The point p has been rotated in 90-degree
// increments until p has been moved into the upper-right
// quadrant (where x >= 0 and y >= 0).
{
    while ((p.get_x() < 0) || (p.get_y() < 0))
        p.rotate90();
}
```

In C++, a reference parameter is declared by placing the type name followed by the symbol & and the parameter name. So, we have written point& p in the parameter list.

Here is the key to reference parameters: Any use of the parameter within the body of the function will access the argument in the calling program. Let's look at an example in a program:

the effect of a reference parameter
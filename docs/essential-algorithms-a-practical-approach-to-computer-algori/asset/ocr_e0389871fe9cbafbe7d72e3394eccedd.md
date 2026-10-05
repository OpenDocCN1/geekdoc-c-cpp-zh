# General Recursion Removal

The previous sections explained how you can remove tail recursion and how you can remove recursion from the Fibonacci algorithm, but they don't give a general algorithm for removing recursion in other situations. For example, the Hilbert curve is highly recursive, so you can use tail recursion removal on it. You might be able to work on it long enough to come up with a nonrecursive version, but that would be hard.

A general way to remove recursion is to mimic what the program performs. Before making a recursive call, the program stores information about its current state on the stack. Then, it returns the information off the stack so that it can resume execution where it left off.

To mimic this behavior, divide the algorithm into sections that come before each recursive call, and name them 1, 2, 3, and so forth.

Create a variable named section that indicates which section should execute next. Set this variable to 1 initially so that the algorithm starts with the first section of code.

Create a While loop that executes recursive as long as section is greater than 0. Move all the algorithm code inside the While loop and place inside it series of If-Else statements. Make each If statement compare the variable section to a section number, and execute the corresponding code if they match. (You can use a Switch or Select statement instead of a series of If-Else statements if you prefer.).

When the algorithm enters a section of code, increment the variable section so that the algorithm knows which section to execute the next time it passes through the loop.

When the algorithm normally calls recursive, push all parameters current values onto stacks. Also, push section onto a stack so that the algorithm will know which section to execute when it returns from the fake recursion. Update any parameters that would be used by the fake recursion. Finally, set section = 0 to begin the fake recursive call at the first section of code.

The following pseudocode describes the original Hilbert curve algorithm presented in this chapter broken into sections after each recursion:

```
Hilbert(Integer: depth, Float: dx, Float: dy)
// Section 1.
If (depth > 0) Then Hilbert(depth - 1, dx, dy)

// Section 2.
DrawRelative(dy, dx)
If (depth > 0) Then Hilbert(depth - 1, dx, dy)

// Section 3.
DrawRelative(dy, dx)
```
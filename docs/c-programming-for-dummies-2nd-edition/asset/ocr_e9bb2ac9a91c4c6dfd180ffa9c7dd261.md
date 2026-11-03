When a function consumes an argument, you must clearly tell the compiler what type of argument is required. In Listing 10-4, both the prototype at Line 3 and the graph() function's definition at Line 20 state that the argument must be an int. The variable count is used as the int argument, which then serves as the variable's name inside the function.

The graph() function is called in Line 13, in the midst of the while loop. It's called using the value variable. That's okay; the variable name used in a function call need not match the variable name used inside the function. Only the variable's data type must match, and both count and value are int types.

The graph() function, from Line 20 through Line 27, displays a row of asterisks. The length of the row (in characters) is determined by the value sent to the function.

**Exercise 10-6:** Fire up your editor and feverishly type the source code from Listing 10-4. Save it. Build it. Can you guess what the output might look like before running?

Functions don't necessarily need to consume variables. The graph() function from Listing 10-4 can gobble any int value, including an immediate value (literal) or a constant.

**Exercise 10-7:** Edit the source code from Exercise 10-6, changing Line 13 so that the graph() function is passed a constant value of 64. Build and run.

![](bbox=[0.15, 0.68, 0.25, 0.8])

It's possible to pass a string to a function, but until you've read Chapter 12 on arrays and especially Chapter 18 on pointers, I don't recommend it. A string is really an array, and it requires special C language magic to pass an array to a function.

# Sending multiple values to a function

C offers no limit on how many arguments a function can handle. As long as you properly declare the arguments as specific data types and separate them all with commas, you can stack 'em up like commuters on a morning train, similar to this prototype:

```
void railway(int engine, int boxcar, int caboose);
```

In the preceding line, the railway() function is prototyped. It requires three int arguments: engine, boxcar, and caboose. The function must be passed three arguments, as shown in the prototype.
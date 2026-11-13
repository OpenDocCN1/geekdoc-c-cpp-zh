
## PROGRAMMING EXAMPLE: An Extension of write_vertical

Suppose we want to extend write_vertical to a more powerful function, called super_write_vertical, which handles all integers including negative integers. With a negative input, the new function prints the negative sign on the first line of output, above any of the digits. For example,

```
super_write_vertical(-361)
```

produces this output with a minus sign on the first line:

```
-
3
6
1
```

How do we handle a negative number? The first step seems clear enough: Print the negative sign. After this, we must print the digits of number, which are the same as the digits of abs(number). (The abs function is the “absolute value” function from <cstdlib>. It leaves positive numbers unchanged and removes the negative sign from negative numbers.) So, the pseudocode for super_write_vertical is an extension of our original pseudocode:

```
if (the number is negative)
    Write a negative sign.
    Write the digits of abs(number) stacked vertically.
} else if (the number has only one digit)
    Write that digit.
else
{
    Write the digits of number/10 stacked vertically.
    Write the single digit of number % 10.
}
```

If you think recursively, you will recognize that the step write the digits of abs(number) stacked vertically is a simpler version of our original problem (simpler because the negative sign does not need to be written). This suggests the implementation in Figure 9.2 on page 440, with two recursive calls: one for the new case that writes the digits of abs(number) and a second call for the original case that writes the digits of number/10. We also have added some highlighted comments, identifying two particular locations, Spot #1 and Spot #2, to aid in taking a closer look at recursion.

## A Closer Look at Recursion

### How function calls are executed

The computer keeps track of function calls in the following way: When a function call is encountered, the first step is to save some information that will allow the computation to return to the correct location after the function call is completed. The computer also provides memory for the called function's formal parameters and any local variables that the called function uses. Next, the actual arguments are plugged in for the formal parameters, and the code of the called function begins to execute.

If the execution should encounter another function call—recursive or otherwise—then the first function's computation is stopped temporarily. This is because the second function call must be executed before the first function call can continue. Information is saved that indicates precisely where the first function call should resume when the second call is completed. The second function is given memory for its own parameters and local variables. The execution then proceeds to the second function call. When the second function call is completed, the execution returns to the correct location within the first function. And the first function resumes its computation.

This mechanism is used for both recursive and nonrecursive function calls. As an example of the function-call mechanism in a recursive function, let's completely trace the function call super_write_vertical(-36). Initially, we call super_write_vertical with number set to -36. The actual argument, -36, is copied to the formal parameter, number, and we start executing the code with number having the value -36. At the moment when the function's execution begins, all of the important information that the function needs to work is stored in a special memory block called the function's activation record. The activation record contains information as to where the function should return when it is done with its computation, and it also contains the values of the function's local variables and parameters. For example, if our super_write_vertical function was called from a main program, then the activation record might contain this information:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_469_0.png)

The “return location” specified in a real activation record does not actually refer to lines of code in the main function, but when you’re imagining an activation record you can think of a return location in this manner.

With the activation record in place, the function starts executing. Because the number is negative, the boolean test of the if-statement is true, and the negative sign is printed. At this point, the computation is about to make a recursive call, indicated here:

```
if (number < 0)
{
    cout << "-" << endl;
    super_write_vertical(abs(number));
    // This is Spot #1 referred to in the text.
}
```

A recursive call is made in the super_write_vertical function.

This function call generates its own activation record with its own value of number (which will be 36) and its own return location. The new activation record is placed on top of the other activation record, like this:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_470_0.png)

In fact, the collection of activation records is stored in a stack data structure called the run-time stack. Each function call pushes the next activation record on top of the run-time stack.

In our example, the second call of super_write_vertical executes with its own value of number equal to 36. The function's code executes, taking the last branch of the if-else control structure, arriving at another recursive call shown here:

Another recursive call is made in the super_write_vertical function.

```
else
{
    super_write_vertical(number/10);
    // This is Spot #2 referred to in the text.
}
cout << number % 10 << endl;
```

To execute this recursive call, another activation record is created (with number now set to 3), and this activation record is pushed onto the run-time stack:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_471_0.png)

The super_write_vertical function begins executing once more. With number set to 3, the function enters the section to handle a one-digit number. At this point, the digit 3 is printed, and no other work is done during this function call.

When the third function call ends, its activation record is popped off the stack. But just before it is popped, the activation record provides one last piece of information—telling where the computation should continue. In our example, the third activation record is popped off the stack, and the computation continues at Spot #2 in Figure 9.2 on page 440. At this point we have the two remaining activation records shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_471_1.png)

As we said, the computation is now at Spot #2 in Figure 9.2 on page 440. This is the highlighted location shown here:

```
else
{
    super_write_vertical(number/10);
    // This is Spot #2 referred to in the text.
    cout << number % 10 << endl;
}
```

The next statement is an output statement. What does it print? From the activation record on top of the stack, we see that number is 36, so the statement prints 6 (which is 36 % 10). The second function call then finishes, returning to Spot #1 in Figure 9.2 on page 440. But there is no more work to do after Spot #1, so the first function call also returns. The total effect of the original function call was to print three characters: a minus sign, then 3, and finally 6. The tracing was all accomplished with the usual function call mechanism—no special treatment was needed to trace recursive calls. In the example there are two levels of recursive calls.

- 1. super_write_vertical(-36) made a recursive call to super_write_vertical(36);
- 2. super_write_vertical(36) made a recursive call to super_write_vertical(3).

In general, function calls may be much deeper than this, but even at the deepest levels the function call mechanism remains the same as the example that we have traced.

## General Form of a Successful Recursive Function

C++ places no restrictions on how recursive calls are used in function definitions. However, in order for a recursive function definition to be useful, any call of the function must ultimately terminate with some piece of code that does not depend on recursion—in other words, there must be a stopping case. The function may call itself, and that recursive call may call the function again. The process may be repeated any number of times. However, the process will not terminate unless eventually one of the recursive calls does not itself make a recursive call. The general outline of a recursive function definition is as follows:

### Key Design Concept

Find smaller versions of a problem within the larger problem itself.

### Recursive Thinking

Suppose that a problem has one or more cases in which some of the subtasks are simpler versions of the same problem you are trying to solve in the first place. These subtasks are solved by recursive calls.

A function that makes recursive calls must also have one or more cases in which the entire computation is accomplished without recursion. These cases without recursion are called stopping cases or base cases.

Often a series of if-else statements determines which of the cases will be executed. A typical scenario is for the original function call to execute a case that includes a recursive call. That recursive call may in turn execute a case that requires another recursive call. For some number of times each recursive call produces another recursive call, but eventually one of the stopping cases applies.

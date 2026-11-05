Every program ever written is composed of the three elements above, and very little else! You can use this to good effect when designing an algorithm of how your program is going to work. At the moment we have only considered programs which run in a straight line and then stop. The path which a program follows is sometimes called its "thread of execution". When you call a function the thread of execution is transferred into the function until it is complete.

# ### Conditional Execution - if

The program above to work out of wood and glass for our glazing man is nice; in fact our customer will probably be quite pleased with it. However, it is not perfect. The problem is not with the program, but with the user.

If you give the program a window width of -1 it goes ahead and works out a stupid result. Our program does not have any checking for invalid widths and heights. The user might have grounds for complaint if the program fails to recognise that he has given a stupid value, in fact a number of cases are currently being fought in the United States courts where a program has failed to recognise invalid data, produced garbage and caused a lot of damage.

What we want to do is notice the really stupid replies and tell the user that he has done something dubious. In our program specification, which we give the customer, we have said something like this (this is our metadata):

The program will reject window dimensions outside the following ranges:

+   - width less than 0.5 metres
+   - width greater than 5.0 metres
+   - height less than 0.75 metres
+   - height greater than 3.0 metres

This means that we have done all we can; if the program gets 1 rather than 10 for the width then that is the users' problem, the important thing from our point of view is that the above specification stops us from being sued!

In order to allow us to do this the program must notice naughty values and reject them. To do this we can use the construction:

```
if (condition)
    statement or block we do if the condition is true
else
    statement or block we do if the condition is false
```

The condition determines what happens in the program. So what do we mean by a condition? C# has a way in which true and false can be explicitly stated in a program. We have already seen that the bool type is used to store this logical state.

We can create conditions which return a logical result. These are called "logical conditions". Which is logical. The simplest condition is simply the value true or false, for example:

```
if (true)
    Console.WriteLine ("hello mum");
```

This is valid, although rather useless as the condition is always true, so "hello mum" is always printed (note that we left the else portion off - this is OK because it is optional).

# ### Conditions and Relational Operators

To make conditions work for us we need a set of additional relational operators which we can use in logical expressions. Relational operators work on operands, just like numeric ones. However any expression involving them can only produce one of two values, true or false. Relational operators available are as follows:
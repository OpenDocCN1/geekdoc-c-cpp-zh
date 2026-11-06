![](bbox=[0.12, 0.095, 0.2, 0.15])

When you retrieve the value that is in a variable, you are not removing it from the variable. The value is still inside the variable.

Book 1  
Chapter 3  

Storing Data in C++

# ### Declaring multiple variables

Many years ago, when we first learned the original C programming language (which was the language that served as the predecessor to C++), we thought it odd that we had to first say the type of the variable and then the name. But this actually works out well because it makes declaring multiple variables of the same type easy. If you want to declare three integer variables in a row, you can do it all in one shot, like this:

```
~~~
int tom, dick, harry;
~~~
```

This statement declares three separate variables. The first is called tom; the second is called dick; and the third is called harry. Each of these three variables holds an integer. You have not put anything in any of them, so you may follow that with some code to stuff each of them full with a number. For example, this code puts the number 10 in tom, the number 20 in dick, and the number 3254 in harry.

```
~~~
tom = 10;
dick = 20;
harry = 3254;
~~~
```

![](bbox=[0.12, 0.517, 0.2, 0.568])

When you run your applications, the computer executes the statements in the order that they appear in your code. Therefore, in the preceding code, the computer first creates the three storage bins. Then it puts a 10 inside tom. (Now doesn't that sound yummy?) Next, dick gets a 20. And finally, harry consumes a 3254.

# ### Changing values

Although a variable can hold only one thing at a time, you can still change what the variable holds. After you put something else in a variable, it forgets what it originally had. So when people accuse us of being forgetful, we can just say, 'Yes, but you should see that computer we work with all day long!'

You put something new in the variable in the same way you originally put something in it.

Look closely at the code for the `ChangeVariable` example in Listing 3-2. Notice that the first part of the application is just like Listing 3-1. But then we added two more lines (shown in bold) that look pretty much like the previous two: The first one sticks something (20) in the same variable as before, and the next one writes this new value out to the console.
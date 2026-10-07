# Chapter 7 More on Classes

numerator /= u;
dominator /= u;

Notice something new about this reduce method: It declares three integer variables u, v, and temp. These variables are local, meaning that their values exist only during execution of the reduce method and that they can be accessed only from within the method in which they are defined. In that sense, they are similar to the variables you have been declaring inside your main routine; those variables were local to main and could be accessed directly from within the main routine. None of the methods you developed could directly access those variables defined in main.

Local variables have no default value, so you must set them to some value before using them. The three local variables in the reduce method are set to values before they are used, so that's not a problem here. Unlike your instance variables (which retain their values through method calls), these local variables have no memory. Therefore, after the method returns, the values of these variables disappear. Every time a method is called, each local variable defined in method is reinitialized to the value specified (if any) with the variable's declaration.

# Method Arguments

The names you use to refer to a method's arguments are also local variables. When the method is executed, whatever arguments are passed to the method are copied into these variables. Because the method is dealing with a copy of the arguments, it cannot change the original values passed to the method. This is an important concept. Suppose you had a method called calculate::, defined as follows:

```
(void) calculate: (double) x
{
  x *= 2;
...
}
```

Also suppose that you used the following message expression to invoke it:
[myData calculate: ptVal];

Whatever value was contained in the local variable x when the calculate method was executed. Changing the value of x inside calculate would have no effect on the value of ptVal—only on the copy of its value stored inside x.

Incidentally, in the case of arguments that are objects, you can change the instance variables stored in that object. That's because when you pass an object as an argument, you actually pass a reference to where the data is stored. Because of that, you can modify that data. You'll learn more about that in the next chapter.
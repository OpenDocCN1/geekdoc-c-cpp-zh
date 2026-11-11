Functions can also be written which *don’t* have a return type. These functions are called *void* functions. They are valid, especially for performing certain operations that are to be done over and over but aren’t particularly mathematical in and of themselves, like printing text to a serial or spinning a motor or something of the like.

Functions also have *arguments*. A function doesn’t *have* to have arguments, but you can *give* a function an argument. A function’s arguments are defined in its declaration. You can tell the types of the arguments as well as the placeholder names. You can then treat the arguments as variables within the body of the function and feed in the actual values when you call the function later in the program.

Again, though, a function doesn’t necessarily *have* to have an argument. This isn’t a requirement for a working function. Remember that as you go forward!

The syntax for prototyping a function is like so:

```
functionType functionName(arguments, if any);
```

And the syntax for actually writing a function is like so:

```
functionType functionName(arguments, if any) {

// code within the function

// return valueName if necessary;

}
```

So, let’s make a function which will return the volume of a cone as a float. This is going to need two arguments, radius and height. It will be a double since we’re working with pi and want it to be as accurate as possible. We will feed in doubles as arguments, too.

We could prototype the function near the start of our program like so:

```
double volumeOfCone(double radius, double height);
```

Then at some point in the program afterward, but not within another function, we
method name is; we don’t care about that, only about the parameters and the return type.

# Declaring a Delegate

Now you know what a delegate is and what it does. It’s time to look at how you create one and this will help you to understand them a bit better.

The delegate we are going to create is one that will represent a method (any method) that can use two numbers in some kind of math operation. What we are going to be saying is: we have these numbers and we need somebody, anyone, doesn’t matter who, to do some math with them and then give us back the result.

There may well be a method floating around that can add the numbers and return the result, or that multiplies them. There might be a method that takes those numbers, squares them, adds them together, and then returns the square root. Hold on, isn’t the Pythagorean Theorem? The point I am making is that all we want is any method that can do something with our numbers and get a result.

We know what we want so let’s make it happen.

We create delegates in the namespace in the same way that we do a struct, a class, and an interface. Just like those, you should get into the habit of placing each delegate into a file of its own – keep them separate for the sake of ease and readability.

So, create a new .cs file and call it whatever your delegate will be called. I’m calling mine MathDelegate.cs but you can call yours whatever you want. Now add the code below to create your delegate:

```
public delegate float MathDelegate(float a, float b);
```

Your MathDelegate.cs file (or whatever you called it) should look like this:

```
using System;
```
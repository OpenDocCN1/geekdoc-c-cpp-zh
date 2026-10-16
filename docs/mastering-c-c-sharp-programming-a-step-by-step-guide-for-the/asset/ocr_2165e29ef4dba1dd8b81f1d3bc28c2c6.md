The first line is nothing more than simple input and, after that, we read the user’s text in and stored it inside a string object. The next bit turned it into the right data type, in our case, the double type and then we did the same with the height of the cylinder.

Next, the value of PI was defined. Then we use some of the math operations we looked at in the last section to calculate what the cylinder surface area and volume are.

```
double pi = 3.1415926536; // We’ll look at a different way to do PI later on.
```

```
// These are the standard formulas for cylinder volume and surface area.
double volume = pi * radius * radius * height;
double surfaceArea = 2 * pi * radius * (radius + height);
```

Last, the result is output to the user:

```
// Now the results can be output
Console.WriteLine("The cylinder's volume is: " + volume + " cubic units.");
Console.WriteLine("The cylinder's surface area is: " + surfaceArea + " square units.");
```

```
// Before you close, wait for a response from the user...
Console.ReadKey();
```

That is our very first useful program written in C#.

# What’s Next?

Now we’ve learned enough to create a useful program, we can kick things up a notch and take things further. Next, we’re going back to
```
// At this point, x will have been incremented to 1.
Console.WriteLine(x);
```

In the prefix case, things are a bit different:

```
int x = 0;

// The value after the increment is assigned, so y will be set to 1.
int y = ++x;

// At this point, x will have been incremented to 1.
Console.WriteLine(x);
```

Decrement operators work in a similar fashion. To test your understanding, what does the following code correspond to? No, I'm not advocating that you write this kind of code; I just want to make sure evaluation order is clear in case you encounter such code.

```
int x = 0;
int y = (x += 1);
Console.WriteLine("X = " + x);
Console.WriteLine("Y = " + y);
```

# FUN WITH SIDE EFFECTS

This should be nothing more than a pop quiz, but the combination of the behavior of different operators can yield interesting results. At your next visit to a programmer's nightclub, try to distinguish C developers from C# developers by having them evaluate the following:

```
int x = 0;
x += x++;
```

Even blogs have been subtitled with this fun expression. (If you don't believe me, take a look at http://blogs.msdn.com/lucabol.)

It should be clear that all arithmetic operations, including the ones discussed here, are subject to overflow checking only when they appear in a checked context. Therefore, the following code will run forever when it doesn't appear in a checked context because the value of x will overflow:

```
for (int x = 0; true; x++)
{
    Console.WriteLine(x);
}
```
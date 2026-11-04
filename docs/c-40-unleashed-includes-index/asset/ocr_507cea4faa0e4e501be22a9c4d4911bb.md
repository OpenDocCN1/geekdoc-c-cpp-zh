```
void PrintName(string name)
{
    if (name != null)
    {
        // Imagine this code is much,
        // much
        // longer...
        Console.WriteLine(name);
    }
}
```

The second case is where a method has a *return type*, requiring the return statement to specify an expression as its operand. That expression should be implicitly convertible to the return type of the containing method:

```
void Add(int a, int b)
{
    return a + b;
}
```

All possible execution paths through the code should eventually lead to a point where a return occurs (modulo edge cases like having an infinite loop). If this condition is not met, the compiler will complain (see Figure 7.30).

![](bbox=[0.07, 0.49, 0.55, 0.6])

FIGURE 7.30 All code paths should return a value.

With a void-returning method, it's fine to just fall out of the current method upon reaching the end of the method. There's no value to return anyway.
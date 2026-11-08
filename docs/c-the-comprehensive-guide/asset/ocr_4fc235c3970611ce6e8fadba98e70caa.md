For a constructor without arguments, this can be done in one of these ways:

```
f(Thing());
Thing d = Thing();
```

The following is also fine:

```
Thing d(12);
```

You now have `d` that has been initialized with 12. Now you could conclude that you initialize such a `d` without constructor arguments like this:

```
Thing d();    // ⚠ Error: Declaration of d as a function
```

And you would be wrong! You have now declared a function `d` that takes no arguments and returns a `Thing`. Please note: You have declared it and not defined it. This is similar to `int mydata();` as a function declaration in a header file. As soon as you want to use `d` in any way, such as with `d.print()`, the compiler complains with the most obscure error messages, such as that “d has not yet been defined” or “a function call was expected.”

If you want to try it out, you don’t need a `Thing`. Try it with `int` or `short`:

```
// https://godbolt.org/z/3G5Po9zEj
int main() {
    int d1(12);    // defines an int and initializes it with 12
    int b1 = d1+1;
    int d2();      // ⚠ declares a function d2 without parameters, return int
    int b2 = d2+1;
    int d3{};      // defines an int and initializes it with 0
    int b3 = d3+1;
}
```

My error message today:

```
arithmetic on a pointer to the function type 'int ()'
```

The solution is to consistently utilize `{...}`, as `Thing d{};` does what you expect.

> **Old Equal Sign or Standardized Initialization?**
> 
> The new initialization with `{...}` is supported by all current compilers. So you have a choice. The “old style” cannot be eradicated (and it is debatable whether this would make sense), but you should use the new style wherever you are not just initializing a native data type such as `int`. This will equip you for the tricky cases.

# 4.2.11  Initialize with “auto”

A word about initialization. It always consists of
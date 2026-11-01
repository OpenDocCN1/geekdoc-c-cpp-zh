```
return 0;
}

inline int radiation(int health)
{
    return (health / 2);
}
```

# Specifying Functions for Inlining

To mark a function for inlining, simply put `inline` before the function definition. That's what I do when I define the following function:

```
inline int radiation(int health)
```

Note that you don't use `inline` in the function declaration:

```
int radiation(int health);
```

By flagging the function with `inline`, you ask the compiler to copy the function directly into the calling code. This saves the overhead of making the function call. That is, program control doesn't have to jump to another part of your code. For small functions, this can result in a performance boost.

However, inlining is not a silver bullet for performance. In fact, indiscriminate inlining can lead to worse performance because inlining a function creates extra copies of it, which can dramatically increase memory consumption.

> **Hint**
> 
> When you inline a function, you really make a request to the compiler, which has the ultimate decision on whether to inline the function. If your compiler thinks that inlining won't boost performance, it won't inline the function.

# Calling Inlined Functions

Calling an inlined function is no different than calling a non-inlined function, as you see with my first call to `radiation()`.

```
health = radiation(health);
```

This line of code assigns `health` one half of its original value.

Assuming that the compiler grants my request for inlining, this code doesn't result in a function call. Instead, the compiler places the code to halve `health`
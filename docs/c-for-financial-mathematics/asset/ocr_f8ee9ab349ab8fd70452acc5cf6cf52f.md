# # Chapter 12

# ## More Sophisticated Classes

In this chapter we discuss a variety of additional features that C++ provides to allow you to write more complex and interesting classes.

# ## 12.1 Inlining member functions

We discussed in Section 5.4.4 that you can use the keyword `inline` with a function, as a hint to the compiler that you want the machine code for the function to be copied every time it is used. This has the advantage of being slightly faster because calling a method uses a little computer power. For example, we chose to inline the functions `hornerFunction` used in the definition of `norminv`.

You can also inline member functions of a class. The procedure is to simply place the definition inside the class in place of the declaration.

```
```
class Point {
public:
 double getX() const {
 return x;
 }
 // other members of Point
private:
 double x;
 double y;
};
```
```

In this example, `getX` is inlined. This means that using this function will result in code that is no slower than code that accesses `x` directly. Using a method has the advantage that if we change our mind about how a `Point` stores its data we can do so without needing to rewrite the code that uses `Point`.

You will probably have noticed that writing an inline function is much less tedious than writing a separate declaration and definition. Unfortunately it isn't advisable to use inlining functions just to avoid typing. You should write separate definitions only if you actually want the function to be inlined.
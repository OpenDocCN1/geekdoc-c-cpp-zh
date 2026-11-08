This means that you should also treat variables of your class as simple values, and so the following applies:

+   - You can assign a completely new value to a variable of your type, instead of changing its internal state.
+   - Prefer passing a variable by value (*call-by-value*). Only when you are sure should you use references (or pointers).
+   - Do not hesitate to return your type as a result.

# Value Parameters

In the example, the functions receive their own data types as value parameters:

```
ostream& operator<<(ostream& os, Date d);
Date easter(Year year);
```

Both functions only read their parameters and do not want to change them. Two ways to pass parameters in this case are by *value* and by *constant reference*.

Passing by value is the safest way to protect your program as it grows from getting confused in a mess of references. Pass a reference, and if the original object no longer exists outside, then the program may crash as soon as the reference is used in the function.

The disadvantage is that the variable has to be copied for this. This costs time and memory during program execution. However, you should still prefer this option to protect yourself from hard-to-find errors in a larger project.

An alternative to passing by value is the *constant reference*. It looks like this in this case:

```
ostream& operator<<(ostream& os, const Date& d) {
    return d.print(os);  // d is const
}
```

But this now results in an error: d must not be changed because that is exactly what you said with `const Date&`. However, `d.print...` could change `d`; at least, that’s how it looks to the compiler. To remedy this, you need to tell the compiler that `print` does not change the object. To do this, add a `const` after the method declaration:

```
ostream& print(ostream& os) const;
```

Now the `d.print(os)` call works—and additionally, you are now also *const-correct*. I go into all these aspects of `const` in [Chapter 13].

# Returns

If you want to return your new type, just do it. Normally, you do not return a reference—and if you do, it is at most one that you received as a parameter, like os in the following:
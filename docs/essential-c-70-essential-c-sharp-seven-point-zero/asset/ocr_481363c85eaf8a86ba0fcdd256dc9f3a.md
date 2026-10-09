Note that the `@` symbol is still required even when only placing the new lines within the curly braces.

# **A D V A N C E D  T O P I C**

# ### Understanding the Internals of String Interpolation

String interpolation is a shorthand for invoking the `string . Format()` method. For example, a statement such as

```
System . Console . WriteLine ($"Your full name is { firstName } { lastName }." )
```

will be transformed to the C# equivalent of

```
object[] args = new object[] { firstName , lastName }; 
Console . WriteLine(string . Format("Your full name is {0} {1} .", args));
```

This leaves in place support for localization in the same way it works with composite string and doesn't introduce any post-compile injection of code via strings.

# #### String Methods

The `string` type, like the `System . Console` type, includes several methods. There are methods, for example, for formatting, concatenating, and comparing strings.

The `Format()` method in Table 2.5 behaves similarly to the `Console . Write()` and `Console . WriteLine()` methods, except that instead of displaying the result in the console window, `string . Format()` returns the result to the caller. Of course, with string interpolation the need for `string . Format()` is significantly reduced (except for localization support). Under the covers, however, string interpolation compiles down to CIL that leverages `string . Format()`.

All of the methods in Table 2.5 are **static**. This means that, to call the method, it is necessary to prefix the method name (e.g, `Concat`) with the type that contains the method (e.g, `string`). As illustrated later in this chapter, however, some of the methods in the `string` class are **instance** methods. Instead of prefixing the method with the type, instance methods use the variable name (or some other reference to an instance). Table 2.6 shows a few of these methods, along with an example.
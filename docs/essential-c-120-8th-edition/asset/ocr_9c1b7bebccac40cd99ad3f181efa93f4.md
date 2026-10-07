# Chapter 3: More with Data Types

public (string First, string Second) ParseNames(string fullName)

is shown in Listing 3.4.

# Listing 3.4: The C# Equivalent of Compiler-Generated CIL Code for a ValueTuple Return

```
[return: System.Runtime.CompilerServices.TupleElementNames(
    new {"First", "Second"})
public System.ValueTuple<string, string> ParseNames(
    string fullName)
{
    // ...
}
```

On a related note, C# 7.0 does not enable the use of custom item names when using the explicit System.ValueTuple<...> data type. Therefore, if you replace var in Example 8 of Tuple 3.1, you will end up with warnings that each item name will be ignored.

Here are a few additional miscellaneous facts to keep in mind about System.ValueTuple<...

+   There are each generic System.ValueTuple<...> corresponding to the possibility of supporting tuples with up to seven items. For the eighth tuple, System.ValueTuple<T1, T2, T3, T4, T5, T6, T7, TRest>, the last type parameter allows specifying an additional ValueTuple, thus enabling support for n items. If, for example, you specify a tuple with parameters, the compiler automatically generates System.ValueTuple<T1, T2, T3, T4, T5, T6, T7, System.ValueTuple<T1>> as the underlying implementing type. (For completeness, System.ValueTuple<T1> will rarely be used, since the C# tuple syntax requires a minimum of two items.)

+   There is a non-generic System.ValueTuple that serves as a tuple factory with Create() methods corresponding to each ValueTuple arity. The ease of using a tuple literal var t1 = ("Inigo Montoya", 42) supersedes the Create() method for C# 7.0 (or later) programmers.

+   For all practical purposes, C# developers can essentially ignore System.ValueTuple and System.ValueTuple<T>.

# 13.2. Code Reading - Generic Bubble Sort

That is,

```
void Sort<T>(IList<T> arr, T pivot), where T : IEquatable<T>,
       IComparable<T> { /* ... */ }
```

As described before, the where clause is the type constraint for a generic type T. The constraint through the interfaces IEquatable<T> and IComparable<T>, from the System namespace, meets those requirements. As declared, the Sort<> method can only used with the types that "implement" both IEquatable<T> and IComparable<T> interfaces.

Unfortunately, that is not enough, however. As we have seen in the int version of the Sort() method, the generic type will also have to support some kind of "subtraction" or "difference" operations. All numeric types support such operations (e.g., the binary minus operator). As stated in the beginning of the lesson, C# currently does not support such constraints for generic types.

There is really no good workaround. You can use a non-generic version (e.g., using object as a type), but that does not solve the problem either. (Numbers, or types that support "difference", are a small number of special types out of many possible types based on object.)

As promised, however, we will show you one example of how to do this without sacrificing generics too much.

The "bubble sort" implementation of generic Sort<T>(IList<T> arr, T pivot) is not much different from its non-generic int counterpart. The most important requirement is that the method uses a generic Compare<T>() method, which takes three arguments of type T, with the same "comparison" requirements.

The implementation of the Compare<T>() method relies on the fact that the type T supports Equals<T>() and CompareTo<T>() methods. This requirement is satisfied by the interface-based type constraint, where T : IEquatable<T>, IComparable<T>.

In addition, `Compare<T>()` uses the custom `Distance<T>()` method, which is essentially a generalization of `Math.Abs()`. The implementation of the `Distance<T>()` method uses another helper method, `Subtract<T>()`. This is where the "magic" happens. `Subtract<T>(T l, T r)` computes the different between two given argument values, `l` and `r`, using the – operator.

As indicated, not all types (even those that implement `IEquatable<T>` and `IComparable<T>`) support the binary subtraction operation. All numeric types support the minus operation. As we will see later in the book, one can define an implementation for the minus – operator for the custom types (known as the "operator overloading"), and those types can be used with our `Sort<T>()` method.

The implementation of `Subtract<T>()` seems quite complicated. Let’s break it down.

First, the `notnull` constraint requires the type `T` should be non-nullable. This is fine in our case because our primary uses will be for numeric types and, possibly, for other custom values types (which cannot be null).

Then, the method uses the "expression body". That is, it is one large expression. As stated, whether ones uses an expression body or a block body is a matter of taste and preference in most cases.

C# has an interesting feature called the "switch expression". This is not to be confused with the traditional "switch statement", which is found in virtually all C-style languages. The `switch` expression feature of C# is "borrowed" from the functional style programming languages. It uses "pattern matching", which is also a concept from the functional programming.

A general syntax is like this:

```
<expression> switch {
<pattern1> => <value1>,
<pattern2> => <value2>,
// ....
_ => <defaultvalue>,
}
```

In this notation, switch is the only keyword. In addition, it uses the "fat arrow" (→), comma (,), underscore (_), and a pair of curly braces ({ and }).

Despite the use of the curly braces, it is an expression, not a statement. It cannot be used as a stand-alone statement. In the sample code, the value of the switch expression is used in the expression body. If we had used a block body, then we would have used return to return this value.

The switch expression works as follows: The type, value, and other properties, etc. of <expression> are computed first. Then they are "matched" against a series of patterns in the switch expression. If it matches any of the patterns, by going through the patterns from top to bottom, then the value of the entire expression is the value specified on the right hand side of ⇒ for that matched pattern.

The patterns in the switch expression have to be "exhaustive". That is, the list of the patterns has to cover all possible cases of the <expression>.

The optional _ identifier like a wildcard. It can be used as a "catch-all" case. If none of the explicit patterns matches, then the value of the default case is used.

C#, as of 9.0, supports many kinds of "patterns". It even supports Boolean combinations of all different patterns, using and, or, and not.

In this sample code, we use the type patterns. (Refer to the C# language reference for all the possible pattern types.) The <expression> is an anonymous tuple, (l, r), in which l and r are the arguments of type T passed in to the Subtract<T>() method.

The first pattern, (sbyte il, sbyte ir), for instance, will match if the type `T` is `sbyte`. When it matches, the variables `il` and `ir` of type `sbyte` can be used for `l` and `r`, respectively. This syntax makes it unnecessary to explicitly have to cast these variables.

If the third pattern matches because `T` is type `int`, for instance, then the overall value of the `switch` expression is `(T)(dynamic)(il - ir)`.

Notice the double casting. The expression `il - ir` (which is the value of `il` subtracted by `ir`) is a value of `int` type, in this specific case. But, we still need to cast it to `T` to satisfy the method signature.

The compiler at this point does not know anything about the relationship between the types `T` and `int`. Hence, we will need to cast it to the `dynamic` type first, and then it can be cast to the desired type `T`. At runtime, if the third pattern is matched, then `T` is `int`. But, the compiler does not know that at build time.

The keyword `dynamic` allows us to bypass the compiler's static type checking, and its use is generally not recommended. We are doing this in this sample code only because of the limitations of the generics in C#.

We do this for all signed integer and floating point types. When a pattern matches, we use the native minus operations for that specific type.

For any other types (for the `_` `default` pattern), we simply compute its "minus" value, `(T)((dynamic)l - (dynamic)r)`, and hope for the best. If the type `T` happens to have a minus (-) operation defined, then it will work. Otherwise it will throw a runtime exception.

We could have just thrown an exception, but doing so would have prevented us from using this method for any (custom) types other than the (already-known) numeric types.

In this sample code, we just take a risk and try to compute `(T)((dynamic)l - (dynamic)r)`. Clearly, the caller of this method should know what to expect when they use non-numeric types. In this expression, notice again the double casting.

Without `dynamic`, the compiler would not let us compute the subtraction of the two values of an arbitrary type T.

In this particular implementation, we are supporting only the signed integer types through the explicit patterns.

The example is just for illustration, and in fact, we could do away with the whole switch expression since at the end of the day, we are computing `(T)((dynamic)l - (dynamic)r)` for types. E.g, T Subtract<T>(T l, T r) ⇒ (T)((dynamic)l - (dynamic)r); (If we throw an exception for non-matched types, or do something else, then these explicit patterns are required.)

If we want to include all unsigned integer types as patterns as well, what changes would be necessary in the implementation of Sort<T>() and its helper methods?

(Note that the reason why we could not list unsigned integer type patterns in this particular implementation was because the minus operation could result in a value of signed integer types.)

Now that we have the implementation of Compare<T>() with the help of Distance<T>() and Subtract<T>(), the implementation of Sort<T>() is complete.

As shown earlier, we can easily verify this implementation using an array or list of any type T which is an IEquatable<T> and an IComparable<T> and which supports the minus (-) operation. The demo program merely uses an array of int type for simplicity.

## Summary

We explored generics a little bit deeper in this (optional) lesson. As stated, the current "limitation" of the C# generics, as illustrated in this chapter, will be removed

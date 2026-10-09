The first pattern, (sbyte il, sbyte ir), for instance, will match if the type `T` is `sbyte`. When it matches, the variables `il` and `ir` of type `sbyte` can be used for `l` and `r`, respectively. This syntax makes it unnecessary to explicitly have to cast these variables.

If the third pattern matches because `T` is type `int`, for instance, then the overall value of the `switch` expression is `(T)(dynamic)(il - ir)`.

Notice the double casting. The expression `il - ir` (which is the value of `il` subtracted by `ir`) is a value of `int` type, in this specific case. But, we still need to cast it to `T` to satisfy the method signature.

The compiler at this point does not know anything about the relationship between the types `T` and `int`. Hence, we will need to cast it to the `dynamic` type first, and then it can be cast to the desired type `T`. At runtime, if the third pattern is matched, then `T` is `int`. But, the compiler does not know that at build time.

The keyword `dynamic` allows us to bypass the compiler's static type checking, and its use is generally not recommended. We are doing this in this sample code only because of the limitations of the generics in C#.

We do this for all signed integer and floating point types. When a pattern matches, we use the native minus operations for that specific type.

For any other types (for the `_` `default` pattern), we simply compute its "minus" value, `(T)((dynamic)l - (dynamic)r)`, and hope for the best. If the type `T` happens to have a minus (-) operation defined, then it will work. Otherwise it will throw a runtime exception.

We could have just thrown an exception, but doing so would have prevented us from using this method for any (custom) types other than the (already-known) numeric types.

In this sample code, we just take a risk and try to compute `(T)((dynamic)l - (dynamic)r)`. Clearly, the caller of this method should know what to expect when they use non-numeric types. In this expression, notice again the double casting.
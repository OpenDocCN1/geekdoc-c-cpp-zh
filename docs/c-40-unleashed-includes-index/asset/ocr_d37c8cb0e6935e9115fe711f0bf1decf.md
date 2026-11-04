# OverflowException

Still in the domain of arithmetic, we find OverflowException, which occurs in a checked context whenever an arithmetic operation, cast, or conversion overflows. For more information about the checked context, see Chapter 5, “Expressions.”

Use of checked contexts is intended to make the application more robust against overflow conditions that will produce incorrect results. By default, C# programs compile with unchecked arithmetic, cast, and conversion operations. Visual Basic reverses this default, which has the potential to negatively impact performance.

It's not uncommon to leave this exception type unhandled when no overflow conditions are expected, but checked contexts are used regardless to guard against incorrect results if overflow ever occurs. This is typically the case in financial or scientific computing, though it's not uncommon to use different types (like BigInteger) altogether to remove limitations on the precision and range of numeric values.

A few examples of overflows are shown here:

```
checked {
    int tooHigh = int.MaxValue + 1; // add.ovf
    int tooLow = int.MinValue - 1;  // sub.ovf
    byte b = 200;
    sbyte s = (sbyte)b;             // conv.ovf
}
```

# NullReferenceException

For people coming from the native code land, NullReferenceException is your modern access violation counterpart in the managed world. If your background lies somewhere else, just remember this exception is something you never want to see in your code.

It's too bad reference types by default permit the null reference, making this exception far too common in improperly tested code. Failure to return a proper object is often signaled by means of a null reference, giving callers a great opportunity to shoot themselves in the foot by omitting a null check. So don't fall into this trap yourself. Instead, check against null values wherever necessary:

```
string s = GetStringMaybeNull();
string oops = s.ToUpper();
```

Another common source of NullReferenceException errors is the improper use of the as keyword where a regular cast is more desirable:

```
object o = GetSomeObject();
string s = o as string;     // No null check? Cast!
string oops = s.ToUpper();
```
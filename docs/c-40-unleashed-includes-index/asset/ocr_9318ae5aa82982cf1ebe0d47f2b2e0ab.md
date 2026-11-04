```
```csharp
static long Max(long a, long b)
{
    Console.WriteLine(MethodInfo.GetCurrentMethod());
    return a > b ? a : b;
}
```
```

A little bit of reflection is used to print the invoked method to reveal the method that was chosen by overload resolution. This proves especially handy for the dynamic case because the IDE won’t (and can’t) help us predict the outcome of a dynamic operation.

The following piece of code now contrasts static and dynamic uses of those methods. Notice the use of cast expression syntax to treat a literal as a dynamic object, simply for illustration purposes:

```
```csharp
//
// Static typing - fully resolved at compile time
//
Max(3, 5);
Max(3, 5L); // the first parameter can be implicitly converted to long
Max(3L, 5L);

//
// Dynamic typing - same resolution at runtime, based on runtime types
//
Max((dynamic)3, 5);
Max(3, (dynamic)5L); // same as above, but discovered by the runtime binder
Max((dynamic)3L, (dynamic)5L);
```
```

Both the static and dynamic case will produce the same output, revealing the methods that were called:

```
```
Int32 Max(Int32, Int32)
Int64 Max(Int64, Int64)
Int64 Max(Int64, Int64)
```
```

From this, you can clearly see how the same decisions are made about the best match for the Max overload but being deferred until runtime in the latter case. Figure 22.4 shows the call stack (with Show External Code turned on) for a call that was dispatched dynamically. Hitting the same method through the static path will reveal an immediate call from the Main method, illustrating the compile-time resolution that took place.

From Figure 22.4, you can also already see the DLR getting involved. The [Lightweight Function] entry on the call stack is in fact nothing but a function that was generated through LCG, at runtime, to create a fast call path into the targeted Max method after overload resolution took place. The frame right below this dynamically generated method stems from the generated call site code, as you learn in the “DLR Internals” section.
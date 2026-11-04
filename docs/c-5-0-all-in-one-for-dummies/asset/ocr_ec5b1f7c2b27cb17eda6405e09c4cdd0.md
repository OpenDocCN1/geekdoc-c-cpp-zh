+   ◆ `Console.WriteLine(dynamicVariable);`: Because there is no overload of `WriteLine` that accepts a `dynamic` type explicitly, the entire method call is dispatched dynamically.

# Making static operations dynamic

If the compiler chooses to make a static operation dynamic — as it did in item 6 in the preceding section — the compiler rebuilds the code on the fly to have it handle the dynamic variable. What does that mean for you? Glad you asked.

Take item 6, `Console.WriteLine(dynamicVariable);`. This piece of code forces the compiler to build intermediary code, which checks for the type of variable at runtime in order to come up with something that is writable to the console. The compiled code first checks if the input is a static type that it knows. Next, it checks for a type present in the program. Then it will just try a few things that might work. It will fail with an error if it finds nothing.

If this must happen, that's fine. But remember that it is slower than all git out. This is why `Variant` got such a bad rap in Visual Basic classic. Dynamic is something you don't use until you need it. It puts a tremendous strain on the machine running the program, especially if all variables are dynamic.

# Understanding what’s happening under the covers

Here’s an example right out of MSDN. Microsoft points out this simple method:

```
class C
{
    public dynamic MyMethod(dynamic d)
    {
        return d.Foo();
    }
}
```

This is pretty straightforward stuff — a method that accepts a `dynamic` class and returns the results of the type’s `Foo` method. Not a big deal.

Here is the compiled C# code:

```
class C
{
    [return: Dynamic]
    public object MyMethod([Dynamic] object d)
    {
        if (MyMethod<>_SiteContainer0.p__Site1 == null)
        {
            MyMethod<>_SiteContainer0.p__Site1 =
```
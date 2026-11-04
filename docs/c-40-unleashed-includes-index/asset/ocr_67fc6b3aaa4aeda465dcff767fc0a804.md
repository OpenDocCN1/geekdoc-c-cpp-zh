To wrap up our discussion about how call sites get created, let's look at the other call site that got generated for the binary addition operator:

```
<Add>o__SiteContainer0.<p>__Site2 =
    CallSite<Func<CallSite, object, object, object>>.Create(
        Binder.BinaryOperation(
            CSharpBinderFlags.None,
            ExpressionType.Add, typeof(Dyn),
            new CSharpArgumentInfo[] {
                CSharpArgumentInfo.Create(CSharpArgumentInfoFlags.None, null),
                CSharpArgumentInfo.Create(CSharpArgumentInfoFlags.None, null)
            }
        )
    );
```

From the factory method used on the C# Binder type, it's clear we're dealing with such an operation. The ExpressionType parameter should look familiar to those who've studied expression trees in Chapter 21, in the section, “Expression Trees.” If we had used checked around our + operator use, we would have seen ExpressionType.AddChecked. The argument information objects are relatively boring, given no special properties are attributed to them.

By now, it should be clear that call site objects, together with the language-specific binder types, capture all information about the operation intended by the user (well, short of precise static types, that is).

# Dynamic Dispatch

Once the compiler has done its duty of generating code that will construct call site objects at runtime, all remaining work is left to the runtime. We already discussed in detail how call sites are built, but we haven't yet discussed how the invocation of the dynamic operation is initiated. In the code that was generated for our running example, the dispatch can be found at the end:

```
private static void Add([Dynamic] object a, [Dynamic] object b)
{
    // Code to ensure the call site objects are instantiated.

    <Add>o__SiteContainer0.<p>__Site1.Target(
        <Add>o__SiteContainer0.<p>__Site1, typeof(Console),
        <Add>o__SiteContainer0.<p>__Site2.Target(
            <Add>o__SiteContainer0.<p>__Site2, a, b));
}
```
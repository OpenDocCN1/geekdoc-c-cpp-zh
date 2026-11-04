```
{
    <Add>o__SiteContainer0.<>p__Site1 =
        CallSite<Action<CallSite, Type, object>>.Create(
            Binder.InvokeMember(
                CSharpBinderFlags.ResultDiscarded,
                "WriteLine", null, typeof(Dyn),
                new CSharpArgumentInfo[] {
                    CSharpArgumentInfo.Create(
                        CSharpArgumentInfoFlags.IsStaticType
                        | CSharpArgumentInfoFlags.UseCompileTimeType,
                        null),
                    CSharpArgumentInfo.Create(
                        CSharpArgumentInfoFlags.None, null)
                }
            )
        );
}
if (<Add>o__SiteContainer0.<>p__Site2 == null)
{
    <Add>o__SiteContainer0.<>p__Site2 =
        CallSite<Func<CallSite, object, object, object>>.Create(
            Binder.BinaryOperation(
                CSharpBinderFlags.None,
                ExpressionType.Add, typeof(Dyn),
                new CSharpArgumentInfo[] {
                    CSharpArgumentInfo.Create(
                        CSharpArgumentInfoFlags.None, null),
                    CSharpArgumentInfo.Create(
                        CSharpArgumentInfoFlags.None, null)
                }
            )
        );
}

<Add>o__SiteContainer0.<>p__Site1.Target(
    <Add>o__SiteContainer0.<>p__Site1, typeof(Console),
    <Add>o__SiteContainer0.<>p__Site2.Target(
        <Add>o__SiteContainer0.<>p__Site2, a, b));
}
```

That's a whole lot of code, isn't it? In the generated code, two distinct phases can be seen, the first of which creates new CallSite objects if they haven't been created yet. Those objects are kept on a generated type known as the site container. By making this object a single instance (it's a static type with a bunch of static fields on it), the call site can maintain state across method calls to the enclosing method. In our example, the Add method
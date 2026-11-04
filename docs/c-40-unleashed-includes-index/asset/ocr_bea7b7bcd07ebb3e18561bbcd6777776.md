```
return (int)a + (int)b; // from Figure 22.14
return site.Update(site, a, b);
}
```

![](bbox=[0.12, 0.26, 0.6, 0.47])

FIGURE 22.14 Code produced by the C# binder to add two Int32 objects together.

This is exactly why the call site needs to pass itself on invocation; it is the way for the DLR to get to the Target delegate field and substitute it for a more specialized one each time it learns more about invocation targets.

Given this new delegate, any subsequent call presenting two Int32 objects as the input will result in the specialized code fragment being executed. This short-circuits all the logic that lives in the C# binder. This logic is nontrivial; you should understand that the binder in Microsoft.CSharp.dll has knowledge of the language-specific rules for overload resolution, implicit conversions, and so on. For example, if we throw an int and a long at the binder, it will apply the C# rule that an Int32 can be implicitly converted into an Int64, so that the addition can be carried out between two Int64s:

```
if (a is long && b is int)
    return (long)a + (long)b;
```

Of course, this resolution for operations also incorporates lookups for things such as operator overloads, as shown in Figure 22.15, which shows a part of the expression tree handed back by the C# runtime binder upon seeing DateTime and TimeSpan objects.

![](bbox=[0.05, 0.78, 0.62, 0.95])

FIGURE 22.15 An operator overload used to add a DateTime and a TimeSpan.
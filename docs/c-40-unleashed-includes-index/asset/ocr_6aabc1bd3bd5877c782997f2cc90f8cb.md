```
```csharp
try
{
    AddToPackage(fruit);
}
catch (BadFoodException)
{
    TossAway(fruit, RecycleBins.GeneralGarbage);
}
catch (RottenAppleException)
{
    TossAway(fruit, RecycleBins.Compost);
}
```
```

Notice in the preceding fragment that you don't need to specify a variable name for an exception object in a catch block. Anyway, because RottenAppleException derives from BadFoodException, the former will never execute. The compiler will actually prevent you from writing this kind of code. Figure 8.14 shows the error message produced by the compiler when it detects a meaningless ordering of exception handlers.

![](bbox=[0.06, 0.455, 0.715, 0.583])

**FIGURE 8.14** Ordering of catch clauses matters.

# ### Don't Catch All Exceptions

It might be tempting in some cases to write a catch-all handler by using either the root type System.Exception or by simply omitting a type:

```
```csharp
try
{
    // Do something here.
}
catch /* or with (Exception ex) */
{
    // Catches all exceptions.
}
```
```

In general, this is highly discouraged. There will be exceptions you can't handle properly, so there's no point in even attempting to catch those. Because lots of people actually
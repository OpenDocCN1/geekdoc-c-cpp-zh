# # Chapter 5 Dynamic Programming in C#

You’d expect the converter to copy every property from the source to the destination where the properties have the same name and the source object has a public get accessor and the destination type has a public set accessor. This kind of runtime code generation can be best handled by creating an expression, and then compiling and executing it. You want to generate code that does something like this:

```
```csharp
// Not legal C#, explanation only
TTest ConvertFromImaginary(TSource source)
{
    TDest destination = new TDest();
    foreach (var prop in sharedProperties)
    {
        destination.prop = source.prop;
    }
    return destination;
}
```
```

You need to create an expression that creates code that executes the pseudo code written above. Here’s the full method to create that expression and compile it to a function. Immediately following the listing, I’ll explain all the parts of this method in detail. You’ll see that while it’s a bit thorny at first, it’s nothing you can’t handle.

```
```csharp
private void createConverterIfNeeded()
{
    if (converter == null)
    {
        var source = Expression.Parameter(typeof(TSource), "source");
        var dest = Expression.Variable(typeof(TDest), "dest");
        var assignments = from srcProp in typeof(TSource).GetProperties(
            BindingFlags.Public |
            BindingFlags.Instance)
            where srcProp.CanRead
            let destProp = typeof(TDest).GetProperty(
                srcProp.Name,
                BindingFlags.Public |
                BindingFlags.Instance)
            in
            // (code continues but not shown in image excerpt)
    }
}
```
```
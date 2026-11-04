Now nobody can ever call this method (without playing dirty tricks using reflection APIs, that is) because no instance can be created to invoke the method on. By marking the class as static, the compiler enforces that only static members are defined.

# Overload Resolution

Actually, the fact that two Reverse extension methods show up illustrates how overload resolution applies to extension methods, too. When we write the following code, the compiler considers the extension method on string to be a better match than the one that's defined on IEnumerable<T>, with T substituted for char:

```
var input = Console.ReadLine();
Console.WriteLine(input.Reverse());
```

Hence, our method will take precedence over the one defined by the LINQ APIs. Also, extension methods are considered only when no suitable instance method is found. In other words, they are performed as a “last-chance lookup” operation after all attempts to find instance methods fail:

```
static class StringExtensions
{
    public static string Substring(this string s, int startIndex)
    {
```

Although it’s valid to define an extension method like the preceding one, you won’t be able to call it through “instance invocation syntax” because System.String already has a Substring method that takes in an int parameter:

```
var art = "Bart".Substring(1);
```

Because an instance method is found, the compiler doesn’t have to go and look for some extension method that takes a string as the first parameter and accepts an integer after it. If we still want to call our extension method, we can do so by using static method invocation syntax:

```
var art = StringExtensions.Substring("Bart", 1);
```

Notice that because of this order of overload resolution, only attempting to use extension methods after all instance method lookups fail, an extension method cannot be called because it’s a “better match than” an instance method. For example:

```
static class StringExtensions
{
    public static string Substring(this string s, byte startIndex)
    {
```
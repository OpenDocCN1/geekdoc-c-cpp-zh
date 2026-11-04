```
```csharp
void PrintName(dynamic d)
{
    Console.WriteLine(d.Name);
}
```
```

In the preceding, an obvious dynamic call site is the call to `Name` because the left side of the operation is typed to be dynamic. As you will see later, `Console.WriteLine` gets turned into a dynamic call as well because its argument is typed as `dynamic` here, too. However, it's possible to call the same method with objects of many different runtime types, such as `FileInfo`, `DirectoryInfo`, `MethodInfo`, `Person`, and so on. Because all of those types expose some `Name` property, the call will succeed.

Depending on the runtime type of `d`, a different call needs to be made, though; recall the runtime itself uses strong typing. This is what call sites keep track of. Their core role is to provide dispatching services, making sure inputs get routed to the correct call underneath. All of this happens in concert with various DLR services, as detailed later.

# ### The dynamic Type

Now that we've identified key terminology related to dynamic operations, let's take a step back and look at the “language surface” for the feature in C# 4.0. In essence, there's just the `dynamic` keyword, which indicates that discovery of operations need to be deferred until runtime, relying on the `dynamic` runtime type rather than the `static` compile-time type. For example, in the following piece of code, `s` is statically typed to be a `string`:

```
```csharp
string s = "Hello world";
Console.WriteLine(s.ToUpper());
```
```

The compiler does make sure it's impossible to assign anything other than a `string` (or in more general cases, anything that's not compatible with the variable's type) to `s`. Notice that the use of casts may result in runtime exceptions:

```
```csharp
string s = (string)GetObject(); // object GetObject();
Console.WriteLine(s.ToUpper());
```
```

However, the invariant we stated before still holds: You should never to be able to see anything that's not a `string` being held by variable `s`. The fact the runtime prevents you from doing such an invalid thing is key to type safe and memory safety.

Because the variable is statically typed to `System.String`, the compiler knows precisely which `ToUpper` method we're talking about. This method's return type is `System.String`, and hence the overload of `Console.WriteLine` is statically determined, too. If you were to look at the generated IL code, this would be immediately apparent.

Whereas we've been using a rather specific type in the preceding example, there's another end to the static typing spectrum, where we would be using the most common supertype
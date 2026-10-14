```
```cil
.property instance valuetype Speed Speed()
{
    .get instance valuetype Speed Velocity::get_Speed()
} // end of property Velocity::Speed
```
```

Apart from the CIL-specific markers .property, instance, and valuetype, the call to get_Speed is a regular method call. The compiler has synthesized the get_Speed method too, and its signature looks like this in the CIL:

```
```cil
.method public hidebysig specialname instance valuetype Speed
    get_Speed() cil managed
{
    --snip--
}
```
```

If Speed had a corresponding set accessor, it would be emitted as a method named set_Speed that takes a Speed parameter and returns void. The CIL markers hidebysig and specialname aren’t used during execution, but they’re used by tools that work with CIL.

The compiler implements the get_Speed accessor as a method that takes no parameters and returns a value of Speed by value. It’s almost exactly as if we’d written our own method returning a Speed like this:

```
```csharp
public Speed get_Speed()
{
    // return a Speed value
}
```
```

The Speed property’s get accessor returns a copy of a Speed instance by value, in exactly the same way as any method returning a Speed by value.

It’s easy to mistake using a property or indexer for directly accessing a field, since the method calls injected by the compiler are conveniently hidden. However, it’s important to be aware that accessing a property or indexer calls a method and typically copies values.

> **NOTE**  Indexers *are special instance methods that allow an object to be accessed as if it were an array or similar sequence-like object. They’re implemented via methods in the same way as properties.*

# Using Expressions with Operators

Expressions with operators, such as + or ==, often also represent method calls, requiring copies for parameters and return values and perhaps making other copies internally. For example, in Listing 4-19 we add two Speed values.

```
```csharp
var start = Speed.FromMetersPerSecond(55);
var increase = Speed.FromMetersPerSecond(15);

var final = start + increase;
```
```

*Listing 4-19: Adding two Speed values*
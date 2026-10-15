maintain the integrity internally of an object. The point is that this approach quickly became a recognized best practice for designing types. And so the C# language designers took steps to facilitate this type of design by implementing some syntactic enhancements. This is how that it became possible to implement that pattern, beginning with C# version 3.

```
public int X { get; set; }
public int Y { get; set; }

public override string ToString() {
    return $"({X}, {Y})";
}
}
```

This version of the Point class leverages auto properties, which means we don't need to explicitly define private backing fields to hold the values we want to store. Instead, we can simply declare our publicly accessible properties and let the compiler handle that behind the scenes, nor do we need to implement the canonical body of the getter and setter for each property. The compiler will implement those too in the manner that you would expect, although without parameter validation. The result is definitely a lot cleaner than before, and you can always use the original syntax if this doesn't suit your specific needs. Much more recently, C# 9 codified support for a common pattern that involved the desire to define a property that has its value initially set by the caller when an instance of the type is initially constructed, but that could only be read by outside callers from that point on. A property that can be initialized once, but then only accessed in a manner subsequently by callers outside of the type itself, is implemented by using the init keyword instead of the set keyword to define the setter. Init properties like this remain read/writable from within the
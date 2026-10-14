
The compiler won’t allow any modifications via the read-only local reference variable. We’ve also made the destination field read-only in the Mail class. This means that we **must** use a read-only reference if we return a reference to the destination field. If we attempt to return a read-only field by reference without the `readonly ref` modifier, the compiler gives us this error:

> [CS8160] A readonly field cannot be returned by writable reference

We can assign one ref variable to another by using the same syntax as assigning a ref local to the result of a property. Note that a ref readonly variable can be assigned from a non-read-only reference. An automatic and implicit conversion occurs from a plain—or *writable*—ref return or a ref local to a ref readonly variable, but not in the other direction. A read-only reference can’t be assigned to a writable ref local. Doing so would break the immutability guarantees of a read-only reference.

## Keeping By-Reference Variables Within Scope

Methods can return values by reference too, and the syntax is the same as for properties. However, the lifetime of the variable returned by reference must be guaranteed to last at least as long as the reference’s lifetime. More formally, the scope of the variable being referenced must *include* the method or property that returns a reference to that variable.

One implication of this rule is that we can’t return a reference to a local variable, because the variable will go out of scope as soon as the method or property implementation returns. This is most clearly apparent for value types. The lifetime of a value ends when the scope ends, so its lifetime is *shorter* than that of the reference. The method in Listing 3-29 fails to compile because it’s attempting to return a reference to a local variable.

```
public ref Address Get()
{
    var val = new Address();
    return ref val;
}
```

*Listing 3-29: Trying to return a reference to a local variable*

If we could return a reference to the val variable, the code calling this method would get a reference to a value that no longer exists. The compiler prevents such a situation by refusing to compile the code, giving this error:

> [CS8168] Cannot return local 'val' by reference because it is not a ref local

This rule applies regardless of whether the value of the local variable is a reference or an instance of a struct. The *variable* still goes out of scope, even when the *instance* exists on the heap. By-reference variables and by-reference returns are references to variables, not instances, in exactly the same way as by-reference parameters.

## Instance Fields of Value Types

The compiler will prevent us from returning a variable by reference if it can’t guarantee that the variable will be valid for at least as long as any reference to it. A less obvious consequence of this rule is that a method or property of a value type can’t return a reference to one of that type’s instance fields. The code in Listing 3-30, for instance, won’t compile.

```
public readonly struct Color
{
    --snip--
    public ref readonly uint Rgb => ref rgbValue;

    private readonly uint rgbValue;
}
```

*Listing 3-30: Returning a struct field by reference*

The compiler gives us this error message:

> [CS8170] Struct members cannot return 'this' or other instance members by reference

This operation is prohibited because the compiler can’t easily determine that the Color instance will outlive any reference to a field within it. Listing 3-31 shows a pathological example to demonstrate why that might be a problem.

```
public ref readonly uint DefaultRgb()
{
    var source = new Color();

    ref readonly var rgb = ref source.Rgb;
    return ref rgb;
}
```

*Listing 3-31: Invalid code returning a reference to a struct’s field*

If the Color struct in Listing 3-30 could legally return one of its fields by reference, the DefaultRgb method in Listing 3-31 would be returning a reference to a field of an object that has gone out of scope. This is a similar problem to returning a reference to a local variable, but this time the problem is directly related to Color being a struct. When a Color variable goes out of scope, each of its fields goes out of scope too. The compiler forbids returning any instance field of a value type by reference to avoid even the possibility of this happening.

Member methods and properties of a value type are also prevented from returning this by reference. It’s disallowed for exactly the same reason as for instance fields: if it were permitted, we would be returning a reference to a local value—an instance of the type—that goes out of scope.

## References to References

When a reference variable goes out of scope, the instance it represented still exists on the heap until it is garbage collected. We can, therefore, safely return a reference to an instance field from a property or method of a class or a record. In fact, holding such a by-reference variable prevents the instance from being garbage collected. In Listing 3-32, we take a reference to an instance field of a local reference type object and return it.

```
public ref readonly Address GetAddress()
{
    var local = new Mail("G Lad Esq.",
        new ("62 West Wallaby Street", "Wigan", "Lancashire", "WG7 7FU"));

    ref readonly var address = ref local.Destination;
    return ref address;
}
```

Listing 3-32: Returning a reference to a field of a local object

The compiler accepts this code, and it’s safe to use this method, although we should certainly be cautious because this technique relies on a somewhat esoteric feature of the garbage collector. When GetAddress returns, the local variable goes out of scope, leaving no live reference variables directly to the Mail instance created inside the GetAddress method. Normally, that instance would then become eligible for garbage collection, making the by-reference return value a dangling reference. However, the returned by-reference variable is enough to prevent the garbage collector from destroying the Mail instance, so holding a by-reference variable to one of its fields remains valid.

Behind the scenes, a by-reference variable or parameter to a field within a class or record instance represents a managed pointer. Managed pointers are an implementation detail of the CLR, but the takeaway here is that they’re tracked by the garbage collector and considered object roots—simply put, references or managed pointers to objects known to be live when the garbage collector runs. Those objects, in turn, may contain references to other objects on the heap, so the chain of references forms a graph of objects currently in use at the time the garbage collector runs.

The garbage collector uses object roots to determine whether object instances can be collected: any instance it can’t reach from an object root by following the object graph is eligible for collection, and any object that is reachable survives. Storing a ref local variable is enough to keep the owning object from being garbage collected.

We can always safely return a by-reference parameter variable by reference because the variable aliased by the parameter must be in scope for the calling code. Strictly, the scope of the variable includes the method accepting the parameter by reference, as shown in Listing 3-33.

```
public ref Color RemoveRed(ref Color color)
{
    color = new Color(0, color.Green, color.Blue);
    return ref color;
}

var hasRed = new Color(0x77, 0xFF, 0x11);

ref var noRed = ref RemoveRed(ref hasRed);

Assert.That(noRed.Red, Is.EqualTo(0));
Assert.That(hasRed.Red, Is.EqualTo(0));
```

Listing 3-33: Returning a ref parameter by reference

The RemoveRed method's color parameter can be returned by reference because the reference can't outlive the variable underlying it, since the scope of the hasRed variable in the calling code includes RemoveRed. Listing 3-34 shows that the same is true of out parameters, even though they look like they're returning a reference to a local variable.

```
public ref Color CreateColor(out Color result)
{
    result = new Color();
    return ref result;
}

ref var created = ref CreateColor(out Color color);

Assert.That(created.Red, Is.EqualTo(0));
Assert.That(color.Red, Is.EqualTo(0));
```

Listing 3-34: Returning an out parameter by reference

The result parameter in the CreateColor method is a reference to a variable in the calling code, whose scope also includes the CreateColor method itself.

NOTE Returning out parameters by reference is prohibited as of C# v11.0, although returning ref parameters by reference is still permitted.

We can also return in parameters by reference, but they must be returned as ref readonly, because an in parameter is immutable. If we forget to make the returned reference readonly, the compiler gives us a predictable error:

```
[CS8333] Cannot return variable 'in Color' by writable reference because it is a readonly variable
```

Given that the variable used to populate the in parameter must already be part of the calling code and we can't modify it in any way, returning an

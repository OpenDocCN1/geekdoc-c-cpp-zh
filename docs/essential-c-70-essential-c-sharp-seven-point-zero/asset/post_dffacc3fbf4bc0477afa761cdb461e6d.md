
### Listing 9.7

```csharp
class Program
{
    static void Main()
    {
        // ...

        Angle angle = new Angle(25, 58, 23);
        // Example 1: Simple box operation
        object objectAngle = angle;  // Box
        Console.Write( ((Angle)objectAngle).Degrees);

        // Example 2: Unbox, modify unboxed value, and discard value
        ((IAngle)objectAngle).MoveTo(26, 58, 23);
        Console.Write(", " + ((Angle)objectAngle).Degrees);

        // Example 3: Box, modify boxed value, and discard reference to box
        ((IAngle)angle).MoveTo(26, 58, 23);
        Console.Write(", " + ((Angle)angle).Degrees);

        // Example 4: Modify boxed value directly
        ((IAngle)objectAngle).MoveTo(26, 58, 23);
        Console.WriteLine(", " + ((Angle)objectAngle).Degrees);

        // ...
    }
}
```

**Output 9.2**

```
25, 25, 25, 26
```

Listing 9.7 uses the `Angle` struct and `IAngle` interface. Note also that the `IAngle.MoveTo()` interface changes `Angle` to be mutable. This change brings out some of the idiosyncrasies of mutable value types and, in so doing, demonstrates the importance of the guideline to make structs immutable.

In Example 1 of Listing 9.7, after you initialize `angle`, you then box it into a variable called `objectAngle`. Next, Example 2 calls `MoveTo()` to change `Hours` to 26. However, as the output demonstrates, no change actually occurs the first time. The problem is that to call `MoveTo()`, the compiler unboxes `objectAngle` and (by definition) makes a copy of the value. Value types are copied by value—that is why they are called value types. Although the resultant value is successfully modified at execution time, this copy of the value is discarded and no change occurs on the heap location referenced by `objectAngle`.

Recall our analogy that suggested variables of value type are like pieces of paper with the value written on them. When you box a value, you make a photocopy of the paper and put the copy in a box. When you unbox the value, you make a photocopy of the paper in the box. Making an edit to this second copy does not change the copy that is in the box.

In Example 3, a similar problem occurs in reverse. Instead of calling `MoveTo()` directly, the value is cast to `IAngle`. The conversion to an interface type boxes the value, so the runtime copies the data in `angle` to the heap and provides a reference to that box. Next, the method call modifies the value in the referenced box. The value stored in variable `angle` remains unmodified.

In the last case, the cast to `IAngle` is a reference conversion, not a boxing conversion. The value has already been boxed by the conversion to `object` in this case, so no copy of the value occurs on this conversion. The call to `MoveTo()` updates the `Hours` value stored in the box, and the code behaves as desired.

As you can see from this example, mutable value types are quite confusing because it is often unclear when you are mutating a copy of the value rather than the storage location you actually intend to change. By avoiding mutable value types in the first place, you can eliminate this sort of confusion.

### Guidelines
- AVOID mutable value types.

## Advanced Topic

### How Boxing Can Be Avoided during Method Calls

Anytime a method is called on a value type, the value type receiving the call (represented by `this` in the body of the method) must be a variable, not a value, because the method might be trying to mutate the receiver. Clearly, it must be mutating the receiver's storage location, rather than mutating a copy of the receiver's value and then discarding it. Examples 2 and 4 of Listing 9.7 illustrate how this fact affects the performance of a method invocation on a boxed value type.

In Example 2, the unboxing conversion logically produces the boxed value, not a reference to the storage location on the heap that contains the boxed copy. Which storage location, then, is passed as the `this` to the mutating method call? It cannot be the storage location from the box on the heap, because the unboxing conversion produces a copy of that value, not a reference to that storage location.

When this situation arises—a variable of value type is required but only a value is available—one of two things happens: Either the C# compiler generates code that makes a new, temporary storage location and copies the value from the box into the new location, resulting in the temporary storage location becoming the needed variable, or the compiler produces an error and disallows the operation. In this case, the former strategy is used. The new temporary storage location is then the receiver of the call; after it is mutated, the temporary storage location is discarded.

This process—performing a type check of the boxed value, unboxing to produce the storage location of the boxed value, allocating a temporary variable, copying the value from the box to the temporary variable, and then calling the method with the location of the temporary storage—happens every time you use the unbox-and-then-call pattern, regardless of whether the method actually mutates the variable. Clearly, if it does not mutate the variable, some of this work could be avoided. Because the C# compiler does not know whether any particular method you call will try to mutate the receiver, it must err on the side of caution.

These expenses are all eliminated when calling an interface method on a boxed value type. In such a case, the expectation is that the receiver will be the storage location in the box; if the interface method mutates the storage location, it is the boxed location that should be mutated. Therefore, the expense of performing a type check, allocating new temporary storage, and making a copy is avoided. Instead, the runtime simply uses the storage location in the box as the receiver of the call to the struct’s method.

In Listing 9.8, we call the two-argument version of `ToString()` that is found on the `IFormattable` interface, which is implemented by the `int` value type. In this example, the receiver of the call is a boxed value type, but it is not unboxed to make the call to the interface method.

### Listing 9.8: Avoiding Unboxing and Copying

```csharp
int number;
object thing;
number = 42;

// Boxing
thing = number;
// No unboxing conversion
string text = ((IFormattable)thing).ToString(
      "X", null);
Console.WriteLine(text);
```

You might now wonder: Suppose that we had instead called the virtual `ToString()` method declared by `object` with an instance of a value type as the receiver. What happens then? Is the instance boxed, unboxed, or what? A number of different scenarios are possible depending on the details:

- If the receiver is unboxed and the struct overrides `ToString()`, the overridden method is called directly. There is no need for a virtual call because the method cannot be overridden further by a more derived class; all value types are automatically sealed.
- If the receiver is unboxed and the struct does not override `ToString()`, the base class implementation must be called, and it expects a reference to an `object` as its receiver. Therefore, the receiver is boxed.
- If the receiver is boxed and the struct overrides `ToString()`, the storage location in the box is passed to the overriding method without unboxing it.
- If the receiver is boxed and the struct does not override `ToString()`, the reference to the box is passed to the base class’s implementation of the method, which is expecting a reference.

## Enums

Compare the two code snippets shown in Listing 9.9.

### Listing 9.9: Comparing an Integer Switch to an Enum Switch

```csharp
int connectionState;
// ...
switch (connectionState)
{
    case 0:
        // ...
        break;
    case 1:
        // ...
        break;
    case 2:
        // ...
        break;
    case 3:
        // ...
        break;
}

ConnectionState connectionState;
// ...
switch (connectionState)
{
    case ConnectionState.Connected:
        // ...
        break;
    case ConnectionState.Connecting:
        // ...
        break;
    case ConnectionState.Disconnected:
        // ...
        break;
    case ConnectionState.Disconnecting:
        // ...
        break;
}
```

Obviously, the difference in terms of readability is tremendous—in the second snippet, the cases are self-documenting. However, the performance at runtime is identical. To achieve this outcome, the second snippet uses **enum values** in each case.

An enum is a value type that the developer can declare. The key characteristic of an enum is that it declares at compile time a set of possible constant values that can be referred to by name, thereby making the code easier to read. The syntax for a typical enum declaration is shown in Listing 9.10.

### Listing 9.10: Defining an Enum

```csharp
enum ConnectionState
{
    Disconnected,
    Connecting,
    Connected,
    Disconnecting
}
```

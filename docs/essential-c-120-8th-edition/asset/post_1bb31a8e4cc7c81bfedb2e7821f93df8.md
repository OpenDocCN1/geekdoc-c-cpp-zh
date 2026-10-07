
# Chapter 9: Introducing Structs and Records

Recall our analogy that suggested variables of value types are like pieces of paper with the value written on them. When you box a value, you make a photocopy of the paper and put the copy in a box. When you unbox the value, you make a photocopy of the paper in the box. Making an edit to this second copy does not change the copy that is in the box.

In Example 3, a similar problem occurs, but in reverse. Instead of calling MoveTo() directly, the value is cast to IAngle. The conversion to an interface boxes the value, so the runtime copies the data in angle to the heap and provides a reference to that box. Next, the method call modifies the value in the referenced box. The value stored in variable angle remains unmodified.

In the last case, the cast to IAngle is a reference conversion, not a boxing conversion. The value has already been boxed by object in this case, so no copy of the value occurs on this conversion. The call to MoveTo() updates the value stored in the box, and the code behaves as desired.

As you can see from this example, mutable value types are quite confusing because it is often unclear when you are mutating a copy of the value rather than the storage location you actually intend to change. By avoiding mutable value types in the first place, you can eliminate this sort of confusion.

> Guidelines
AVOID mutable value types.

# ADVANCED TOPIC avoided during Method Calls

### How Boxing Can Be Avoided during Method Calls
Anytime a method is called on a value type, the value type receiving the call (represented by this in the body of the method) must be a variable, not a value, because the method might be trying to mutate the receiver. Clearly, it must be mutating the receiver's storage location, rather than mutating a copy of the receiver's value and then discarding it. Examples 2 and 4 of Listing 9.11 illustrate how this fact affects the performance of a method invocation on a boxed value type.

In Example 2, the unboxing conversion logically produces the boxed value, not a reference to the storage location on the heap that contains the boxed copy. Which storage location, then, is passed via this to the mutating method call? It cannot be the storage location from the box on the heap, the unboxing conversion produces a copy of that value, not a reference to that storage location.

When this situation arises—a variable of value type is required but only a value is available—one of two things happens: the C# compiler generates code that makes a new, temporary storage location and copies the value from the box into the new location, resulting in the storage location becoming the needed variable, or the compiler produces errors and disallows the allocation. In this case, the former strategy is used. The new storage location is then the receiver of the call; after it is mutated, the boxed value is discarded.

This process—performing a type check of the boxed value, unboxing to produce the storage location of, allocating a temporary variable, copying the value from the box to the variable, and then calling the method with the location of the temporary storage—happens every time you use the unbox-and-then-call pattern, regardless of whether the method mutates the variable. Clearly, the C# compiler does not know whether any of this work would be avoided. Because the C# compiler does not know whether any particular method you call will try to mutate the receiver, it must err on the side of caution.

These expenses are all eliminated when calling an interface method on a boxed value type. In such a case, the expectation is that the receiver will be the storage location in the box; if the interface method mutates the storage location, it is the boxed location that should be mutated. Therefore, the expense of performing a type check, allocating new temporary storage, and making a copy is avoided. Instead, the runtime simply uses the storage location in the box as the receiver of the call to the struct's method.

In Listing 9.28, we call the two-argument version of ToString() that is found on the IFormattable interface, which is implemented by the int type. In this example, the receiver of the call is a boxed value type, but it is not unboxed to make the call to the interface method.

```
Listing 9.28: Avoiding Unboxing and Copying
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

Now suppose that we had replaced the virtual ToString() method declared by object with an instance of a value type as the receiver. What happens then? Is the instance boxed, unboxed, or something else? A number of different scenarios are possible depending on the details:

- If the receiver is unboxed and the struct overrides ToString(), the overridden method is called directly. There is no need for a virtual call because the method cannot be overridden further by a more derived class; all value types are automatically sealed.
- If the receiver is unboxed and the struct does not override ToString(), the base class implementation must be called, and it expects a reference to an object as its receiver. Therefore, the receiver is boxed.
- If the receiver is boxed and the struct overrides ToString(), the storage location in the box is passed to the overridden method without unboxing.
- If the receiver is boxed and the struct does not override ToString(), the reference to the box is passed to the base class's implementation of the method, which is expecting a reference.

# Enums

Compare the two code snippets shown in Listing 9.29. Obviously, the difference in terms of readability is tremendous—in the second snippet, the cases are self-documenting. However, the performance at runtime is identical. To achieve this outcome, the second snippet uses enum values.

# LISTING 9.29: Comparing an Integer Switch to an Enum Switch

```c
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
// ...
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

An enum is a value type that the developer can declare. The key characteristic of an enum is that it declares, at compile time, a set of possible values that can be referred to by name, thereby making the code easier to read. The syntax for a typical enum declaration is shown in Listing 9.30.

```
LISTING 9.30: Defining an Enum
enum ConnectionState {
    Disconnected,
    Connecting,
    Connected,
    Disconnecting
}
```

> NOTE
enum can be used as a more readable replacement for Boolean values as well. For example, a method call such as SetState(true) is less readable than SetState(DeviceState.On).

You use an enum value by prefixing it with the enum's name. To use the Connected value, for example, you would use the syntax ConnectionState.Connected. Do not make the enum type part of the value's name to avoid the redundancy of ConnectionState.ConnectionStateConnected and similar references. By convention, the enum name itself should be singular (unless the enum values are bit flags, as discussed shortly). That is, the nomenclature should be ConnectionState, not ConnectionStates.

> Guidelines
DO NOT use the enum type name as part of the values name.
DO use an enum type name that is singular unless the enum is a flag.

Enum values are actually implemented as nothing more than integer constants. By default, the first enum is given the value 0, and each subsequent entry increases by 1. Alternatively, you can assign explicit values to enum members, as shown in Listing 9.31.

In this code, Disconnected has a default value of 0 and Connecting has been explicitly assigned 10; consequently, Connected will be assigned 11.

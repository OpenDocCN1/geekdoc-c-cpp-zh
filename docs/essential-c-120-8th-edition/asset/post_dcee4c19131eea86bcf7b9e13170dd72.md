
# 508 Chapter 9: Introducing Structs and Records

LISTING 9.10: Cloning Records via the With Operator

```csharp
Angle angle = new(90, 0, 0, null);

// The with operator is the equivalent of
// Angle copy = new(degrees, minutes, seconds);
// Angle copy = angle with {};
Trace.Assert(angle == copy);
```

```csharp
// The with operator has object initializer type
// syntax for instantiating a modified copy.
Angle modifiedCopy = angle with { Degrees = 180 };
Trace.Assert(angle != modifiedCopy);
```

Cloning a record struct is a memory copy, the same as when creating a copy to an invoke method with pass by value. For this reason, you can't change the implementation for cloning a record struct.

For record classes, the process is slightly different. The C# compiler generates a hidden Clone() method (shown in Listing 9.5) that in turn invokes the copy constructor with a parameter for the source instance. You can also view that same code in Listing 9.11.

LISTING 9.11: Cloning Record Classes via the Clone Method

```csharp
// Actual name in IL is "<Clone>". However,
// you can't add a Clone method to a record.
public Coordinate Clone() => new(this);
```

```csharp
protected Coordinate(Coordinate original)
{
    Longitude = original.Longitude;
    Latitude = original.Latitude;
}
```

The clone method in turn calls the constructor. Note that in the case where the object initializer syntax is used, the assigned property cannot be read-only (either setter or an init-only setter is required). Also, the Clone() method uses a special non-C#-compliant name, making it accessible only via the with operator. If you want

+   4. A constructor that takes single parameter or the containing type. See Chapter 6.

to customize the clone behavior, however, you can provide your own implementation of the copy constructor.

# Record Constructors

Note that the record declaration of Listing 9.1 looks virtually identical to the constructor signature in Listing 9.3. Similarly, with the record class associated code in Listing 9.4 and its equivalent C#-generated equivalent in Listing 9.5, a record declaration and its positional parameters provide the structure for the C# compiler to generate a constructor with an equivalent-looking signature.

As with the properties themselves, one peculiarity with the record is that the positional parameters are, by convention, PascalCase, and, therefore, so are the parameters for the constructor. (Consequently, when initializing the properties, the generated constructor code uses this to distinguish the parameters from the properties.)

You can add additional constructors to the record’s definition. For example, you could provide a constructor that has strings rather than integers as parameters, as shown in Listing 9.12.

LISTING 9.12: Adding Additional Record Constructors

```csharp
public Angle(
    string degrees, string minutes, string seconds)
    : this(int.Parse(degrees),
      int.Parse(minutes),
      int.Parse(seconds))
{}
```

The implementation of an additional constructor uses the same syntax as any other constructor. The only additional constraint is that it must call the record-generated constructor or another constructor that calls the record-generated constructor. This ensures that the initialization of the positional parameter-generated properties are all initialized.

# Record Struct Initialization

Prior to C# 10.0, no default constructor could be defined. Regardless, if not explicitly instantiating a struct via the new operator’s call to the constructor, all data contained within the struct is implicitly initialized to data's default value. The default value is null for a field of reference type data, a zero value for a field of numeric type, and false for a field of Boolean type data, including fields backing an automatically implemented property. Similarly, since field and property initialization during declaration⁵ (as string Description { get; init; } = "") is injected into the constructor by the compiler, and it will also not execute without the new operator invocation.

It is important to be aware of this because, unlike with reference types, it is common for value types to be instantiated without the new operator. Assigning a value type to default or not initializing a value field on a class, for example, will not execute any constructor, neither will an uninitialized array item such as the one displayed in Listing 9.13.

# LISTING 9.13: Uninitialized Array Item

```csharp
Angle[] angles = new[2];
```

In both cases, regardless of what the default constructor initializes data members, they will end up with default values. For this reason, do not rely on either default constructors or member initialization at declaration time.

Prior to C# 11.0, every constructor in a struct must initialize all fields (and read-only, automatically implemented properties⁶) within the struct. Failure to initialize all data within the struct causes a compile-time error in C# 10.0 and earlier:

> CS0171: Field must be fully assigned before control is returned to the caller. Consider updating to language version '11.0' to auto-default the field.

Because of the struct's field initialization requirement, the succinctness of read-only field declaration, automatically implemented property support, and the guideline to avoid accessing fields from outside of its wrapping property, you should favor read-only, automatically implemented properties over fields within structs.

+   5. Enabled starting in C# 10.0
6. Initialization via a read-only, automatically implemented property is sufficient starting in C# 6.0, because the backing field is unknown and its initialization would not be possible otherwise.

# Guidelines

- DO ensure that the default value of a struct is valid; encapsulation cannot prevent obtaining the "all zero" struct.
- DO NOT rely on either default constructors or member initialization at declaration to run on a value type.

# ADVANCED TOPIC

# Using new with Value Types

Invoking the new operator with a reference type causes the runtime to create a new instance of the object on the garbage-collected heap, initialize all of its fields to their default values, and call the constructor, passing a reference to the instance as this. The result is the reference to the instance, which can then be copied to its final destination. In contrast, invoking the new operator with a value type causes the runtime to create a new instance of the object on the temporary storage pool, initialize all of its fields to their default values, and call the constructor (passing the temporary storage location as a ref variable through this), resulting in the value stored in the temporary storage location, which can then be copied to its final destination.

Unlike classes, structs do not support finalizers. Structs are copied by value; they do not have referential identity, as reference types do. Therefore, it is hard to know when it would be safe to execute the finalizer and free an unmanaged resource owned by the struct. The garbage collector knows when there are no more live references to an instance of reference type and can choose to run the finalizer for an instance of reference type at any time after there are no live references. Nevertheless, no part of the runtime tracks how many copies of a given value type exist at any moment.

# Chapter 9: Introducing Structs and Records

### Language Contrast: C++—struct Defines Type with Public Members

In C++, the difference between a type declared with struct and one declared with class is whether the default accessibility is public or private. The contrast is far greater in C#, where the difference is whether instances of the type are copied by value or by reference.

# Record Destructors

In addition to the properties and constructor, the C# compiler also generates a positional parameter--corresponding deconstructor, as seen in Listing 9.14:

LISTING 9.14: Record Destructor

```csharp
public void Deconstruct(
    out int Degrees, out int Minutes, out int Seconds)
{
    Degrees = this.Degrees;
    Minutes = this.Minutes;
    Seconds = this.Seconds;
}
```

This enables pattern matching like that used in Listing 9.2 (displayed again in Listing 9.15):

LISTING 9.15: Pattern Matching

```csharp
if (angle is (int, int, int, string) angleData)
{
    // ...
}
```

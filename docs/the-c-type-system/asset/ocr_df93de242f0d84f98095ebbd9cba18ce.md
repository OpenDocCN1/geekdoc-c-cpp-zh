In other words, the new expression is an abstraction that shields us from the implementation details of how memory is allocated and used.

Specifically, the memory for reference type instances is allocated dynamically. When a new instance of a class or record type is created, the memory is allocated on the heap at run time. Instances of struct and record struct types are allocated differently, depending on how the resulting instance is used. Consider this code, which initializes a variable with a new instance of a type named Thing:

```
var thing = new Thing();
```

This basic syntax for creating an object and assigning it to a variable is the same whether Thing is a class, struct, record, or record struct. As you’ll see over the coming sections, this code depends on Thing having an accessible constructor that can be invoked with no arguments, which isn’t necessarily the case when Thing is a reference type. For the time being, though, let’s assume that Thing instances can be created this way. If Thing is a class or a record, new causes memory to be allocated on the heap at run time and returns a reference to the new object, which is assigned to the thing variable.

If Thing is a struct or a record struct, the new instance is assigned to the thing variable. However, this code may or may not allocate memory for a new instance of Thing and may or may not call a constructor. The reason is that construction and initialization are separate processes. Part of the difference is related to whether a Thing is a value type or reference type.

# Default Initialization

Default initialization means that each of a type’s fields, including the backing fields for properties, is given a default value, which is defined in the language to mean one of the following:

+   - References are set to null.
+   - Built-in numeric value type variables are set to 0.
+   - All other value types are default-initialized.

Default-initialized reference type fields are a common cause of errors. For example, the simple MusicTrack struct in Listing 2-12 relies on us manually initializing an instance by setting its properties. If we neglect to set suitable values for the properties of a MusicTrack instance, we may be rewarded with an exception when we use the instance.

```
public struct MusicTrack
{
    public string Artist { get; set; }
    public string Name { get; set; }

    public override string ToString()
        => $"{Artist.ToUpper()}: {Name.ToUpper()}";
}
```
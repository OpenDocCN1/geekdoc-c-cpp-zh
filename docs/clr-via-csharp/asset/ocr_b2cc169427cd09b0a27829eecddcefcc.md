# ### How the CLR Controls the Layout of a Type’s Fields

To improve performance, the CLR is capable of arranging the fields of a type any way it chooses. For example, the CLR might reorder fields in memory so that object references are grouped together and data fields are properly aligned and packed. However, when you define a type, you can tell the CLR whether it must keep the type’s fields in the same order as the developer specified them or whether it can reorder them as it sees fit.

You tell the CLR what to do by applying the System.Runtime.InteropServices.StructLayoutAttribute attribute on the class or structure you’re defining. To this attribute’s constructor, you can pass LayoutKind.Auto to have the CLR arrange the fields, LayoutKind.Sequential to have the CLR preserve your field layout, or LayoutKind.Explicit to explicitly arrange the fields in memory by using offsets. If you don’t explicitly specify the StructLayoutAttribute on a type that you’re defining, your compiler selects whatever layout it determines is best.

You should be aware that Microsoft’s C# compiler selects LayoutKind.Auto for reference types (classes) and LayoutKind.Sequential for value types (structures). It is obvious that the C# compiler team believes that structures are commonly used when interoperating with unmanaged code, and for this to work, the fields must stay in the order defined by the programmer. However, if you’re creating a value type that has nothing to do with interoperability with unmanaged code, you probably want to override the C# compiler’s default. Here’s an example:

```
```csharp
using System;
using System.Runtime.InteropServices;

// Let the CLR arrange the fields to improve
// performance for this value type.
[StructLayout(LayoutKind.Auto)]
internal struct SomeValType {
    private readonly Byte m_b;
    private readonly Int16 m_x;
    ...
}
```
```

The StructLayoutAttribute also allows you to explicitly indicate the offset of each field by passing LayoutKind.Explicit to its constructor. Then you apply an instance of the System.Runtime.InteropServices.FieldOffsetAttribute attribute to each field passing to this attribute’s constructor an Int32 indicating the offset (in bytes) of the field’s first byte from the beginning of the instance. Explicit layout is typically used to simulate what would be a union in unmanaged C/C++ because you can have multiple fields starting at the same offset in memory. Here is an example:
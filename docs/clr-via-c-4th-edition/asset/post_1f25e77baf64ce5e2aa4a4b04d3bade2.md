
## How the CLR Controls the Layout of a Type's Fields

To improve performance, the CLR is capable of arranging the fields of a type any way it chooses. For example, the CLR might reorder fields in memory so that object references are grouped together and data fields are properly aligned and packed. However, when you define a type, you can tell the CLR whether it must keep the type's fields in the same order as the developer specified them or whether it can reorder them as it sees fit.

You tell the CLR what to do by applying the `System.Runtime.InteropServices.StructLayoutAttribute` attribute on the class or structure you're defining. To this attribute's constructor, you can pass `LayoutKind.Auto` to have the CLR arrange the fields, `LayoutKind.Sequential` to have the CLR preserve your field layout, or `LayoutKind.Explicit` to explicitly arrange the fields in memory by using offsets. If you don't explicitly specify the `StructLayoutAttribute` on a type that you're defining, your compiler selects whatever layout it determines is best.

You should be aware that Microsoft's C# compiler selects `LayoutKind.Auto` for reference types (classes) and `LayoutKind.Sequential` for value types (structures). It is obvious that the C# compiler team believes that structures are commonly used when interoperating with unmanaged code, and for this to work, the fields must stay in the order defined by the programmer. However, if you're creating a value type that has nothing to do with interoperability with unmanaged code, you could override the C# compiler's default. Here's an example.

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

The `StructLayoutAttribute` also allows you to explicitly indicate the offset of each field by passing `LayoutKind.Explicit` to its constructor. Then you apply an instance of the `System.Runtime.InteropServices.FieldOffsetAttribute` attribute to each field passing to this attribute's constructor an `Int32` indicating the offset (in bytes) of the field's first byte from the beginning of the instance. Explicit layout is typically used to simulate what would be a union in unmanaged C/C++ because you can have multiple fields starting at the same offset in memory.

Here is an example.

```csharp
using System;
using System.Runtime.InteropServices;

// The developer explicitly arranges the fields of this value type.
[StructLayout(LayoutKind.Explicit)]
internal struct SomeValType {
    [FieldOffset(0)]
    private readonly Byte m_b; // The m_b and m_x fields overlap each

    [FieldOffset(0)]
    private readonly Int16 m_x; // other in instances of this type
}
```

It should be noted that it is illegal to define a type in which a reference type and a value type overlap. It is possible to define a type in which multiple reference types overlap at the same starting offset; however, this is unverifiable. It is legal to define a type in which multiple value types overlap; however, all of the overlapping bytes must be accessible via public fields for the type to be verifiable.

## Boxing and Unboxing Value Types

Value types are lighter weight than reference types because they are not allocated as objects in the managed heap, not garbage collected, and not referred to by pointers. However, in many cases, you must get a reference to an instance of a value type. For example, let's say that you wanted to create an ArrayList object (a type defined in the System.Collections namespace) to hold a set of Point structures. The code might look like this.

```csharp
// Declare a value type.
struct Point {
    public Int32 x, y;
}

public sealed class Program {
    public static void Main() {
        ArrayList a = new ArrayList();
        Point p;                        // Allocate a Point (not in the heap).
        for (Int32 i = 0; i < 10; i++) {
            p.x = p.y = i;              // Initialize the members in the value type.
            a.Add(p);                   // Box the value type and add the
                                        // reference to the ArrayList.
        }
        ...
    }
}
```

With each iteration of the loop, a Point's value type fields are initialized. Then the Point is stored in the ArrayList. But let's think about this for a moment. What is actually being stored in the ArrayList? Is it the Point structure, the address of the Point structure, or something else entirely? To get the answer, you must look up ArrayList's Add method and see what type its parameter is defined as. In this case, the Add method is prototyped as follows.

```csharp
public virtual Int32 Add(Object value);
```

From this, you can plainly see that Add takes an Object as a parameter, indicating that Add requires a reference (or pointer) to an object on the managed heap as a parameter. But in the preceding code, I'm passing p, a Point, which is a value type. For this code to work, the Point value type must be converted into a true heap-managed object, and a reference to this object must be obtained.

It's possible to convert a value type to a reference type by using a mechanism called boxing. Internally, here's what happens when an instance of a value type is boxed:

- 1. Memory is allocated from the managed heap. The amount of memory allocated is the size required by the value type's fields plus the two additional overhead members (the type object pointer and the sync block index) required by all objects on the managed heap.
- 2. The value type's fields are copied to the newly allocated heap memory.
- 3. The address of the object is returned. This address is now a reference to an object; the value type is now a reference type.

The C# compiler automatically produces the IL code necessary to box a value type instance, but you still need to understand what's going on internally so that you're aware of code size and performance issues.

In the preceding code, the C# compiler detected that I was passing a value type to a method that requires a reference type, and it automatically emitted code to box the object. So at run time, the fields currently residing in the Point value type instance p are copied into the newly allocated Point object. The address of the boxed Point object (now a reference type) is returned and is then passed to the Add method. The Point object will remain in the heap until it is garbage collected. The Point value type variable (p) can be reused because the ArrayList never knows anything about it. Note that the lifetime of the boxed value type extends beyond the lifetime of the unboxed value type.

> **Note** It should be noted that the FCL now includes a new set of generic collection classes that make the non-generic collection classes obsolete. For example, you should use the System.Collections.Generic.List<T> class instead of the System.Collections.ArrayList class. The generic collection classes offer many improvements over the non-generic equivalents. For example, the API has been cleaned up and improved, and the performance of the collection classes has been greatly improved as well. But one of the biggest improvements is that the generic collection classes allow you to work with collections of value types without requiring that items in the collection be boxed/unboxed. This in itself greatly improves performance because far fewer objects will be created on the managed heap, thereby reducing the number of garbage collections required by your application. Furthermore, you will get compile-time type safety, and your source code will be cleaner due to fewer casts. This will all be explained in further detail in Chapter 12, "Generics."

I mentioned earlier that an unboxing operation is frequently followed immediately by a field copy. Let's take a look at some C# code demonstrating that unbox and copy operations work together.

```csharp
    public static void Main() {
        Point p;
        p.x = p.y = 1;
        Object o = p;   // Boxes p; o refers to the boxed instance

        p = (Point) o;  // Unboxes o AND copies fields from boxed
                        // instance to stack variable
    }
```

On the last line, the C# compiler emits an IL instruction to unbox o (get the address of the fields in the boxed instance) and another IL instruction to copy the fields from the heap to the stack-based variable p.

Now look at this code.

```csharp
    public static void Main() {
        Point p;
        p.x = p.y = 1;
        Object o = p;   // Boxes p; o refers to the boxed instance

        // Change Point's x field to 2
        p = (Point) o;  // Unboxes o AND copies fields from boxed
                        // instance to stack variable
        p.x = 2;        // Changes the state of the stack variable
        o = p;          // Boxes p; o refers to a new boxed instance
    }
```

The code at the bottom of this fragment is intended only to change Point's x field from 1 to 2. To do this, an unbox operation must be performed, followed by a field copy, followed by changing the field (on the stack), followed by a boxing operation (which creates a whole new boxed instance in the managed heap). Hopefully, you see the impact that boxing and unboxing/copying operations have on your application's performance.

Some languages, such as C++/CLI, allow you to unbox a boxed value type without copying the fields. Unboxing returns the address of the unboxed portion of a boxed object (ignoring the object's type object pointer and sync block index overhead). You can now use this pointer to manipulate the unboxed instance's fields (which happen to be in a boxed object on the heap). For example, the previous code would be much more efficient if written in C++/CLI, because you could change the value of Point's x field within the already boxed Point instance. This would avoid both allocating a new object on the heap and copying all of the fields twice!

> **Important** If you're the least bit concerned about your application's performance, you must be aware of when the compiler produces the code that performs these operations. Unfortunately, many compilers implicitly emit code to box objects, so it is not obvious when you write code that boxing is occurring. If I am concerned about the performance of a particular algorithm, I always use a tool such as ILDasm.exe to view the IL code for my methods and see where the box IL instructions are.


```
}
```

The code at the bottom of this fragment is intended only to change Point's x field from 1 to 2. To do this, an unbox operation must be performed, followed by a field copy, followed by changing the field (on the stack), followed by a boxing operation (which creates a whole new boxed instance in the managed heap). Hopefully, you see the impact that boxing and unboxing/copying operations have on your application's performance.

Some languages, such as C++/CLI, allow you to unbox a boxed value type without copying the fields. Unboxing returns the address of the unboxed portion of a boxed object (ignoring the object's type object pointer and sync block index overhead). You can now use this pointer to manipulate the unboxed instance's fields (which happen to be in a boxed object on the heap). For example, the previous code would be much more efficient if written in C++/CLI, because you could change the value of Point's x field within the already boxed Point instance. This would avoid both allocating a new object on the heap and copying all of the fields twice!

**Important** If you're the least bit concerned about your application's performance, you must be aware of when the compiler produces the code that performs these operations. Unfortunately, many compilers implicitly emit code to box objects, and so it is not obvious when you write code that boxing is occurring. If I am concerned about the performance of a particular algorithm, I always use a tool such as ILDasm.exe to view the IL code for my methods and see where the box IL instructions are.

Let's look at a few more examples that demonstrate boxing and unboxing:

```csharp
public static void Main() {
    Int32 v = 5;            // Create an unboxed value type variable.
    Object o = v;           // o refers to a boxed Int32 containing 5.
    v = 123;                // Changes the unboxed value to 123

    Console.WriteLine(v + ", " + (Int32) o);    // Displays "123, 5"
}
```

In this code, can you guess how many boxing operations occur? You might be surprised to discover that the answer is three! Let's analyze the code carefully to really understand what's going on. To help you understand, I've included the IL code generated for the Main method shown in the preceding code. I've commented the code so that you can easily see the individual operations.

```cil
.method public hidebysig static void Main() cil managed
{
    .entrypoint
    // Code size       45 (0x2d)
    .maxstack  3
    .locals init ([0]int32 v,
             [1] object o)
    // Load 5 into v.
    IL_0000:  ldc.i4.5
    IL_0001:  stloc.0
    // Box v and store the reference pointer in o.
    IL_0002:  ldloc.0
    IL_0003:  box        [mscorlib]System.Int32
    IL_0008:  stloc.1

// Load 123 into v.
IL_0009:  ldc.i4.s   123
IL_000b:  stloc.0

// Box v and leave the pointer on the stack for Concat.
IL_000c:  ldloc.0
IL_000d:  box        [mscorlib]System.Int32

// Load the string on the stack for Concat.
IL_0012:  ldstr      ", "

// Unbox o: Get the pointer to the Int32's field on the stack.
IL_0017:  ldloc.1
IL_0018:  unbox.any  [mscorlib]System.Int32

// Box the Int32 and leave the pointer on the stack for Concat.
IL_001d:  box        [mscorlib]System.Int32

// Call Concat.
IL_0022:  call       string [mscorlib]System.String::Concat(object,
                                                          object,
                                                          object)

// The string returned from Concat is passed to WriteLine.
IL_0027:  call       void [mscorlib]System.Console::WriteLine(string)

// Return from Main terminating this application.
IL_002c:  ret
} // end of method App:Main
```

First, an Int32 unboxed value type instance (v) is created on the stack and initialized to 5. Then a variable (o) typed as Object is created, and is initialized to point to v. But because reference type variables must always point to objects in the heap, C# generated the proper IL code to box and store the address of the boxed copy of v in o. Now the value 123 is placed into the unboxed value type instance v; this has no effect on the boxed Int32 value, which keeps its value of 5.

Next is the call to the WriteLine method. WriteLine wants a String object passed to it, but there is no string object. Instead, these three items are available: an unboxed Int32 value type instance (v), a String (which is a reference type), and a reference to a boxed Int32 value type instance (o) that is being cast to an unboxed Int32. These must somehow be combined to create a String.

To create a String, the C# compiler generates code that calls String's static Concat method. There are several overloaded versions of the Concat method, all of which perform identically—the only difference is in the number of parameters. Because a String is being created from the concatenation of three items, the compiler chooses the following version of the Concat method:

```il
IL_0012:  ldstr      ", "
// Load the address of the boxed Int32 on the stack for Concat.
IL_0017:  ldloca.s 1

// Call Concat.
IL_001a:  call       string [mscorlib]System.String::Concat(object,
                                                         object,
                                                         object)

// The string returned from Concat is passed to WriteLine.
IL_001d:  call       void [mscorlib]System.Console::WriteLine(string)

// Return from Main terminating this application.
IL_0022:  ret
} // end of method App::Main
```

A quick comparison of the IL for these two versions of the Main method shows that the version without the (Int32) cast is 10 bytes smaller than the version with the cast. The extra unbox/box steps in the first version are obviously generating more code. An even bigger concern, however, is that the extra boxing step allocates an additional object from the managed heap that must be garbage collected in the future. Certainly, both versions give identical results, and the difference in speed isn't noticeable, but extra, unnecessary boxing operations occurring in a loop cause the performance and memory usage of your application to be seriously degraded.

You can improve the previous code even more by calling WriteLine like this:

```csharp
Console.WriteLine(v.ToString() + ", " + o);   // Displays "123, 5"
```

Now ToString is called on the unboxed value type instance v, and a String is returned. String objects are already reference types and can simply be passed to the Concat method without requiring any boxing.

Let's look at yet another example that demonstrates boxing and unboxing:

```csharp
public static void Main() {
    Int32 v = 5;                // Create an unboxed value type variable.
    Object o = v;                // o refers to the boxed version of v.

    v = 123;                     // Changes the unboxed value type to 123
    Console.WriteLine(v);        // Displays "123"

    v = (Int32) o;               // Unboxes and copies o into v
    Console.WriteLine(v);        // Displays "5"
}
```

How many boxing operations do you count in this code? The answer is one. The reason that there is only one boxing operation is that the System.Console class defines a WriteLine method that accepts an Int32 as a parameter:

```csharp
public static void WriteLine(Int32 value);
```

In the two calls to `WriteLine` above, the variable v, an Int32 unboxed value type instance, is passed by value. Now it may be that `WriteLine` will box this Int32 internally, but you have no control over that. The important thing is that you should do the best you could and have eliminated the boxing from your own code.

If you take a close look at the FCL, you'll notice many overloaded methods that differ based on their value type parameters. For example, the `System.Console` type offers several overloaded versions of the `WriteLine` method:

```csharp
public static void WriteLine(Boolean);
public static void WriteLine(Char);
public static void WriteLine(Char[]);
public static void WriteLine(Int32);
public static void WriteLine(UInt32);
public static void WriteLine(Int64);
public static void WriteLine(UInt64);
public static void WriteLine(Single);
public static void WriteLine(Double);
public static void WriteLine(Decimal);
public static void WriteLine(Object);
public static void WriteLine(String);
```

You’ll also find a similar set of overloaded methods for `System.Console`’s `Write` method, `System.IO.BinaryWriter`’s `Write` method, `System.IO.TextWriter`’s `Write` and `WriteLine` methods, `System.Runtime.Serialization.SerializationInfo`’s `AddValue` method, `System.Text.StringBuilder`’s `Append` and `Insert` methods, and so on. Most of these methods offer overloaded versions for the sole purpose of reducing the number of boxing operations for the common value types.

If you define your own value type, these FCL classes will not have overloads of these methods that accept your value type. Furthermore, there are a bunch of value types already defined in the FCL for which overloads of these methods do not exist. If you call a method that does not have an overload for the specific value type that you are passing to it, you will always end up calling the overload that takes an `Object`. Passing a value type instance as an `Object` will cause boxing to occur, which will adversely affect performance. If you are defining your own class, you can define the methods in the class to be generic (possibly constraining the type parameters to be value types). Generics give you a way to define a method that can take any kind of value type without having to box it. Generics are discussed in Chapter 12.

One last point about boxing: if you know that the code that you’re writing is going to cause the compiler to box a single value type repeatedly, your code will be smaller and faster if you manually box the value type. Here’s an example:

```csharp
using System;

public sealed class Program {
    public static void Main() {
        Int32 v = 5;    // Create an unboxed value type variable.
```

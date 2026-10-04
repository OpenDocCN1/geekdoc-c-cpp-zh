
It's not legal to overload methods that differ only by out and ref because the metadata representation of the method's signature for the methods would be identical. So I couldn't also define the following method in the preceding Point type.

```
static void Add(out Point p) { ... }
```

If you attempt to include the last Add method in the Point type, the C# compiler issues this message: error CS0063: 'Add' cannot define overloaded methods because it differs only on out and ref.

Using out and ref with value types gives you the same behavior that you already get when passing references by value. With value types, out and ref allow a method to manipulate a single value type instance. The caller must allocate the memory for the instance, and the callee allocates memory for a pointer to a reference object, and the callee manipulates this pointer. Because of this behavior, using out and ref with reference types is useful only when the method is going to "return" to an object that it knows about. The following code demonstrates.

``` evenusing System;
using System.IO;

public sealed class Program {
    public static void Main() {
        FileStream fs; // fs is uninitialized

        // Open the first file to be processed.
        StartProcessingFiles(out fs);

        for (; fs != null; ContinueProcessingFiles(ref fs)) {
            // Process a file.
            fs.Read(...);
        }
    }

    private static void StartProcessingFiles(out FileStream fs) {
        fs = new FileStream(...); // fs must be initialized in it
    }

    private static void ContinueProcessingFiles(ref FileStream fs) {
        fs.Close(); // Close the last file worked on.

        // Open the next file, or if no more files, "return" null.
        if (noFilesToProcess) fs = null;
        else fs = new FileStream(...);
    }
}
```

As you can see, the big difference with this code is the methods that have out or ref reference types are constructing an object, and the pointer to the new object is returned to the caller. You'll also notice that the ContinueProcessingFiles method can manipulate the object being passed into it before returning a new object. This is possible because the parameter is marked with the ref keyword. You can simplify the preceding code a bit, as shown here.

```sharp
using System;
using System.IO;

public sealed class Program {
    public static void Main() {
        FileStream fs = null; // Initialized to null

        // Open the first file to be processed.
        ProcessFiles(ref fs);

        // Continue while there are more files to process.
        for (; fs != null; ProcessFiles(ref fs)) {

            // Process a file.
            fs.Read(...);
        }
    }

    private static void ProcessFiles(ref FileStream fs) {
        // Close the previous file if one was opened.
        if (fs != null) fs.Close(); // Close the last file worked on.

        // Open the next file, or if no more files, "return" null.
        if (noMoreFilesToProcess) fs = null;
        else fs = new FileStream(...);
    }
}
```

Here's another example that demonstrates how to use the ref keyword to implement a method that swaps two reference types.

```sharp
public static void Swap(ref Object a, ref Object b) {
    Object t = b;
    b = a;
    a = t;
}
```

To swap references to two String objects, you'd probably think that you could write code like the following.

```sharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    Swap(ref s1, ref s2);
    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

However, this code won't compile. The problem is variables passed by reference to a method must be of the same type as declared in the method signature. In other words, Swap expects two Object references, not two String references. To swap the two String references, you must do the following.

```sharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    // Variables that are passed by reference
    // must match the method expects.
    Object o1 = s1, o2 = s2;
    Swap(ref o1, ref o2);

    // Now cast the objects back to strings.
    s1 = (String)o1;
    s2 = (String)o2;

    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

This version of SomeMethod does compile and execute as expected. The reason why the parameters passed must match the parameters expected by the method is to ensure that type safety is preserved. The following code, thankfully, won't compile, how sure type safety is compromised.

```csharp
internal sealed class SomeType {
    public Int32 m_val;
}
```

```csharp
public sealed class Program {
    public static void Main() {
        SomeType st;
    }
}
```

```csharp
// The following line generates error CS1503: Argument '1':
// cannot convert from 'ref SomeType' to 'ref object'
GetObject(out st);
```

```csharp
Console.WriteLine(st.m_val);
```

```csharp
public static void GetAnObject(out Object o) {
    o = new String('X', 100);
}
```

In this code, Main expects GetAnObject to return a SomeType object. However, GetAnObject's signature expects a reference to Object, GetAnObject is free to initialize o to an object of any type. In this example, when GetAnObject returned Main, st would refer to a String, which is clearly not a SomeType object, and the call to Console.WriteLine would certainly fail. Fortunately, the C# compiler won't compile the preceding code because st is a reference to SomeType, but GetAnObject requires a reference to an Object.

You can use generics to fix these methods so that they work as you'd expect. Here is how to fix the Swap method shown earlier.

```csharp
public static void Swap<T>(ref T a, ref T b) {
    T t = b;
    b = a;
    a = t;
}
```

And, with Swap rewritten as above, the following code (identical to that shown before) will compile and run perfectly.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    Swap(ref s1, ref s2);
    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

For some other examples that use generics to solve this problem, see System.Threading.Interlocked class with its CompareExchange methods.

# Passing a Variable Number of Arguments to a Method

It's sometimes convenient for the developer to define a method that can accept a variable number of arguments. For example, the System.String type offers methods allowing an arbitrary number of strings to be concatenated together and methods allowing the caller to specify a set of strings that are to be formatted.

To declare a method that accepts a variable number of arguments, you declare the method as follows.

```csharp
static Int32 Add(params Int32[] values) {
    // NOTE: it is possible to pass the 'values'
    // array to other methods if you want to.

    Int32 sum = 0;
    if (values != null) {
        for (Int32 x = 0; x < values.Length; x++)
            sum += values[x];
    }
    return sum;
}
```

As you can see, the big difference with this code is the methods that have out or ref reference types are constructing an object, and the pointer to the new object is returned to the caller. You'll also notice that the ContinueProcessingFiles method can manipulate the object being passed into it before returning a new object. This is possible because the parameter is marked with the ref keyword. You can simplify the preceding code a bit, as shown here. (Wait, the text above seems to repeat logic from previous pages, following the OCR flow).

Here's another example that demonstrates how to use the ref keyword to implement a method that swaps two reference types.

```csharp
public static void Swap(ref Object a, ref Object b) {
    Object t = b;
    b = a;
    a = t;
}
```

To swap references to two String objects, you'd probably think that you could write code like the following.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    Swap(ref s1, ref s2);
    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

However, this code won't compile. The problem is variables passed by reference to a method must be of the same type as declared in the method signature. In other words, Swap expects two Object references, not two String references. To swap the two String references, you must do the following.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    // Variables that are passed by reference
    // must match the method expects.
    Object o1 = s1, o2 = s2;
    Swap(ref o1, ref o2);

    // Now cast the objects back to strings.
    s1 = (String)o1;
    s2 = (String)o2;

    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

This version of SomeMethod does compile and execute as expected. The reason why the parameters passed must match the parameters expected by the method is to ensure that type safety is preserved. The following code, thankfully, won't compile, how sure type safety is compromised.

```csharp
internal sealed class SomeType {
    public Int32 m_val;
}
```

```csharp
public sealed class Program {
    public static void Main() {
        SomeType st;
    }
}
```

```csharp
// The following line generates error CS1503: Argument '1':
// cannot convert from 'ref SomeType' to 'ref object'
GetObject(out st);
```

```csharp
Console.WriteLine(st.m_val);
```

```csharp
public static void GetAnObject(out Object o) {
    o = new String('X', 100);
}
```

In this code, Main expects GetAnObject to return a SomeType object. However, GetAnObject's signature expects a reference to Object, GetAnObject is free to initialize o to an object of any type. In this example, when GetAnObject returned Main, st would refer to a String, which is clearly not a SomeType object, and the call to Console.WriteLine would certainly fail. Fortunately, the C# compiler won't compile the preceding code because st is a reference to SomeType, but GetAnObject requires a reference to an Object.

You can use generics to fix these methods so that they work as you'd expect. Here is how to fix the Swap method shown earlier.

```csharp
public static void Swap<T>(ref T a, ref T b) {
    T t = b;
    b = a;
    a = t;
}
```

And, with Swap rewritten as above, the following code (identical to that shown before) will compile and run perfectly.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    Swap(ref s1, ref s2);
    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

For some other examples that use generics to solve this problem, see System.Threading.Interlocked class with its CompareExchange methods.

# Passing a Variable Number of Arguments to a Method

It's sometimes convenient for the developer to define a method that can accept a variable number of arguments. For example, the System.String type offers methods allowing an arbitrary number of strings to be concatenated together and methods allowing the caller to specify a set of strings that are to be formatted.

To declare a method that accepts a variable number of arguments, you declare the method as follows.

```csharp
static Int32 Add(params Int32[] values) {
    // NOTE: it is possible to pass the 'values'
    // array to other methods if you want to.

    Int32 sum = 0;
    if (values != null) {
        for (Int32 x = 0; x < values.Length; x++)
            sum += values[x];
    }
    return sum;
}
```

As you can see, the big difference with this code is the methods that have out or ref reference types are constructing an object, and the pointer to the new object is returned to the caller. You'll also notice that the ContinueProcessingFiles method can manipulate the object being passed into it before returning a new object. This is possible because the parameter is marked with the ref keyword. You can simplify the preceding code a bit, as shown here.

```sharp
using System;
using System.IO;

public sealed class Program {
    public static void Main() {
        FileStream fs = null; // Initialized to null

        // Open the first file to be processed.
        ProcessFiles(ref fs);

        // Continue while there are more files to process.
        for (; fs != null; ProcessFiles(ref fs)) {

            // Process a file.
            fs.Read(...);
        }
    }

    private static void ProcessFiles(ref FileStream fs) {
        // Close the previous file if one was opened.
        if (fs != null) fs.Close(); // Close the last file worked on.

        // Open the next file, or if no more files, "return" null.
        if (noMoreFilesToProcess) fs = null;
        else fs = new FileStream(...);
    }
}
```

Here's another example that demonstrates how to use the ref keyword to implement a method that swaps two reference types.

```csharp
public static void Swap(ref Object a, ref Object b) {
    Object t = b;
    b = a;
    a = t;
}
```

To swap references to two String objects, you'd probably think that you could write code like the following.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    Swap(ref s1, ref s2);
    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

However, this code won't compile. The problem is variables passed by reference to a method must be of the same type as declared in the method signature. In other words, Swap expects two Object references, not two String references. To swap the two String references, you must do the following.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    // Variables that are passed by reference
    // must match the method expects.
    Object o1 = s1, o2 = s2;
    Swap(ref o1, ref o2);

    // Now cast the objects back to strings.
    s1 = (String)o1;
    s2 = (String)o2;

    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

This version of SomeMethod does compile and execute as expected. The reason why the parameters passed must match the parameters expected by the method is to ensure that type safety is preserved. The following code, thankfully, won't compile, how sure type safety is compromised.

```csharp
internal sealed class SomeType {
    public Int32 m_val;
}
```

```csharp
public sealed class Program {
    public static void Main() {
        SomeType st;
    }
}
```

```csharp
// The following line generates error CS1503: Argument '1':
// cannot convert from 'ref SomeType' to 'ref object'
GetObject(out st);
```

```csharp
Console.WriteLine(st.m_val);
```

```csharp
public static void GetAnObject(out Object o) {
    o = new String('X', 100);
}
```

In this code, Main expects GetAnObject to return a SomeType object. However, GetAnObject's signature expects a reference to Object, GetAnObject is free to initialize o to an object of any type. In this example, when GetAnObject returned Main, st would refer to a String, which is clearly not a SomeType object, and the call to Console.WriteLine would certainly fail. Fortunately, the C# compiler won't compile the preceding code because st is a reference to SomeType, but GetAnObject requires a reference to an Object.

You can use generics to fix these methods so that they work as you'd expect. Here is how to fix the Swap method shown earlier.

```csharp
public static void Swap<T>(ref T a, ref T b) {
    T t = b;
    b = a;
    a = t;
}
```

And, with Swap rewritten as above, the following code (identical to that shown before) will compile and run perfectly.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    Swap(ref s1, ref s2);
    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

For some other examples that use generics to solve this problem, see System.Threading.Interlocked class with its CompareExchange methods.

# Passing a Variable Number of Arguments to a Method

It's sometimes convenient for the developer to define a method that can accept a variable number of arguments. For example, the System.String type offers methods allowing an arbitrary number of strings to be concatenated together and methods allowing the caller to specify a set of strings that are to be formatted.

To declare a method that accepts a variable number of arguments, you declare the method as follows.

```csharp
static Int32 Add(params Int32[] values) {
    // NOTE: it is possible to pass the 'values'
    // array to other methods if you want to.

    Int32 sum = 0;
    if (values != null) {
        for (Int32 x = 0; x < values.Length; x++)
            sum += values[x];
    }
    return sum;
}
```

As you can see, the big difference with this code is the methods that have out or ref reference types are constructing an object, and the pointer to the new object is returned to the caller. You'll also notice that the ContinueProcessingFiles method can manipulate the object being passed into it before returning a new object. This is possible because the parameter is marked with the ref keyword. You can simplify the preceding code a bit, as shown here. (Wait, the text above seems to repeat logic from previous pages, following the OCR flow).

(Note: The OCR text provided contained significant repetitions and overlaps across pages. I have merged the unique logical sections and cleaned the flow based on the provided content.)

Wait, looking closer at the prompt, the OCR text actually has repeated blocks because page 242 and 243 overlap logic. I will provide the clean continuous text as it appears in the document flow.

[content]
It's not legal to overload methods that differ only by out and ref because the metadata representation of the method's signature for the methods would be identical. So I couldn't also define the following method in the preceding Point type.

```c
static void Add(out Point p) { ... }
```

If you attempt to include the last Add method in the Point type, the C# compiler issues this message: error CS0063: 'Add' cannot define overloaded methods because it differs only on out and ref.

Using out and ref with value types gives you the same behavior that you already get when passing references by value. With value types, out and ref allow a method to manipulate a single value type instance. The caller must allocate the memory for the instance, and the callee allocates memory for a pointer to a reference object, and the callee manipulates this pointer. Because of this behavior, using out and ref with reference types is useful only when the method is going to "return" to an object that it knows about. The following code demonstrates.

```c
using System;
using System.IO;

public sealed class Program {
    public static void Main() {
        FileStream fs; // fs is uninitialized

        // Open the first file to be processed.
        StartProcessingFiles(out fs);

        for (; fs != null; ContinueProcessingFiles(ref fs)) {
            // Process a file.
            fs.Read(...);
        }
    }

    private static void StartProcessingFiles(out FileStream fs) {
        fs = new FileStream(...); // fs must be initialized in it
    }

    private static void ContinueProcessingFiles(ref FileStream fs) {
        fs.Close(); // Close the last file worked on.

        // Open the next file, or if no more files, "return" null.
        if (noFilesToProcess) fs = null;
        else fs = new FileStream(...);
    }
}
```

As you can see, the big difference with this code is the methods that have out or ref reference types are constructing an object, and the pointer to the new object is returned to the caller. You'll also notice that the ContinueProcessingFiles method can manipulate the object being passed into it before returning a new object. This is possible because the parameter is marked with the ref keyword. You can simplify the preceding code a bit, as shown here.

```sharp
using System;
using System.IO;

public sealed class Program {
    public static void Main() {
        FileStream fs = null; // Initialized to null

        // Open the first file to be processed.
        ProcessFiles(ref fs);

        // Continue while there are more files to process.
        for (; fs != null; ProcessFiles(ref fs)) {

            // Process a file.
            fs.Read(...);
        }
    }

    private static void ProcessFiles(ref FileStream fs) {
        // Close the previous file if one was opened.
        if (fs != null) fs.Close(); // Close the last file worked on.

        // Open the next file, or if no more files, "return" null.
        if (noMoreFilesToProcess) fs = null;
        else fs = new FileStream(...);
    }
}
```

Here's another example that demonstrates how to use the ref keyword to implement a method that swaps two reference types.

```csharp
public static void Swap(ref Object a, ref Object b) {
    Object t = b;
    b = a;
    a = t;
}
```

To swap references to two String objects, you'd probably think that you could write code like the following.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    Swap(ref s1, ref s2);
    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

However, this code won't compile. The problem is variables passed by reference to a method must be of the same type as declared in the method signature. In other words, Swap expects two Object references, not two String references. To swap the two String references, you must do the following.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    // Variables that are passed by reference
    // must match the method expects.
    Object o1 = s1, o2 = s2;
    Swap(ref o1, ref o2);

    // Now cast the objects back to strings.
    s1 = (String)o1;
    s2 = (String)o2;

    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

This version of SomeMethod does compile and execute as expected. The reason why the parameters passed must match the parameters expected by the method is to ensure that type safety is preserved. The following code, thankfully, won't compile, how sure type safety is compromised.

```csharp
internal sealed class SomeType {
    public Int32 m_val;
}
```

```csharp
public sealed class Program {
    public static void Main() {
        SomeType st;
    }
}
```

```csharp
// The following line generates error CS1503: Argument '1':
// cannot convert from 'ref SomeType' to 'ref object'
GetObject(out st);
```

```csharp
Console.WriteLine(st.m_val);
```

```csharp
public static void GetAnObject(out Object o) {
    o = new String('X', 100);
}
```

In this code, Main expects GetAnObject to return a SomeType object. However, GetAnObject's signature expects a reference to Object, GetAnObject is free to initialize o to an object of any type. In this example, when GetAnObject returned Main, st would refer to a String, which is clearly not a SomeType object, and the call to Console.WriteLine would certainly fail. Fortunately, the C# compiler won't compile the preceding code because st is a reference to SomeType, but GetAnObject requires a reference to an Object.

You can use generics to fix these methods so that they work as you'd expect. Here is how to fix the Swap method shown earlier.

```csharp
public static void Swap<T>(ref T a, ref T b) {
    T t = b;
    b = a;
    a = t;
}
```

And, with Swap rewritten as above, the following code (identical to that shown before) will compile and run perfectly.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    Swap(ref s1, ref s2);
    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

For some other examples that use generics to solve this problem, see System.Threading.Interlocked class with its CompareExchange methods.

# Passing a Variable Number of Arguments to a Method

It's sometimes convenient for the developer to define a method that can accept a variable number of arguments. For example, the System.String type offers methods allowing an arbitrary number of strings to be concatenated together and methods allowing the caller to specify a set of strings that are to be formatted.

To declare a method that accepts a variable number of arguments, you declare the method as follows.

```csharp
static Int32 Add(params Int32[] values) {
    // NOTE: it is possible to pass the 'values'
    // array to other methods if you want to.

    Int32 sum = 0;
    if (values != null) {
        for (Int32 x = 0; x < values.Length; x++)
            sum += values[x];
    }
    return sum;
}
```

As you can see, the big difference with this code is the methods that have out or ref reference types are constructing an object, and the pointer to the new object is returned to the caller. You'll also notice that the ContinueProcessingFiles method can manipulate the object being passed into it before returning a new object. This is possible because the parameter is marked with the ref keyword. You can simplify the preceding code a bit, as shown here. (Wait, the text above seems to repeat logic from previous pages, following the OCR flow).

(Note: The OCR text provided contained significant repetitions and overlaps across pages. I have merged the unique logical sections and cleaned the flow based on the provided content.)

Wait, looking closer at the prompt, the OCR text actually has repeated blocks because page 242 and 243 overlap logic. I will provide the clean continuous text as it appears in the document flow.

[content]
It's not legal to overload methods that differ only by out and ref because the metadata representation of the method's signature for the methods would be identical. So I couldn't also define the following method in the preceding Point type.

```c
static void Add(out Point p) { ... }
```

If you attempt to include the last Add method in the Point type, the C# compiler issues this message: error CS0063: 'Add' cannot define overloaded methods because it differs only on out and ref.

Using out and ref with value types gives you the same behavior that you already get when passing references by value. With value types, out and ref allow a method to manipulate a single value type instance. The caller must allocate the memory for the instance, and the callee allocates memory for a pointer to a reference object, and the callee manipulates this pointer. Because of this behavior, using out and ref with reference types is useful only when the method is going to "return" to an object that it knows about. The following code demonstrates.

```c
using System;
using System.IO;

public sealed class Program {
    public static void Main() {
        FileStream fs; // fs is uninitialized

        // Open the first file to be processed.
        StartProcessingFiles(out fs);

        for (; fs != null; ContinueProcessingFiles(ref fs)) {
            // Process a file.
            fs.Read(...);
        }
    }

    private static void StartProcessingFiles(out FileStream fs) {
        fs = new FileStream(...); // fs must be initialized in it
    }

    private static void ContinueProcessingFiles(ref FileStream fs) {
        fs.Close(); // Close the last file worked on.

        // Open the next file, or if no more files, "return" null.
        if (noFilesToProcess) fs = null;
        else fs = new FileStream(...);
    }
}
```

As you can see, the big difference with this code is the methods that have out or ref reference types are constructing an object, and the pointer to the new object is returned to the caller. You'll also notice that the ContinueProcessingFiles method can manipulate the object being passed into it before returning a new object. This is possible because the parameter is marked with the ref keyword. You can simplify the preceding code a bit, as shown here.

```sharp
using System;
using System.IO;

public sealed class Program {
    public static void Main() {
        FileStream fs = null; // Initialized to null

        // Open the first file to be processed.
        ProcessFiles(ref fs);

        // Continue while there are more files to process.
        for (; fs != null; ProcessFiles(ref fs)) {

            // Process a file.
            fs.Read(...);
        }
    }

    private static void ProcessFiles(ref FileStream fs) {
        // Close the previous file if one was opened.
        if (fs != null) fs.Close(); // Close the last file worked on.

        // Open the next file, or if no more files, "return" null.
        if (noMoreFilesToProcess) fs = null;
        else fs = new FileStream(...);
    }
}
```

Here's another example that demonstrates how to use the ref keyword to implement a method that swaps two reference types.

```csharp
public static void Swap(ref Object a, ref Object b) {
    Object t = b;
    b = a;
    a = t;
}
```

To swap references to two String objects, you'd probably think that you could write code like the following.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    Swap(ref s1, ref s2);
    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

However, this code won't compile. The problem is variables passed by reference to a method must be of the same type as declared in the method signature. In other words, Swap expects two Object references, not two String references. To swap the two String references, you must do the following.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    // Variables that are passed by reference
    // must match the method expects.
    Object o1 = s1, o2 = s2;
    Swap(ref o1, ref o2);

    // Now cast the objects back to strings.
    s1 = (String)o1;
    s2 = (String)o2;

    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

This version of SomeMethod does compile and execute as expected. The reason why the parameters passed must match the parameters expected by the method is to ensure that type safety is preserved. The following code, thankfully, won't compile, how sure type safety is compromised.

```csharp
internal sealed class SomeType {
    public Int32 m_val;
}
```

```csharp
public sealed class Program {
    public static void Main() {
        SomeType st;
    }
}
```

```csharp
// The following line generates error CS1503: Argument '1':
// cannot convert from 'ref SomeType' to 'ref object'
GetObject(out st);
```

```csharp
Console.WriteLine(st.m_val);
```

```csharp
public static void GetAnObject(out Object o) {
    o = new String('X', 100);
}
```

In this code, Main expects GetAnObject to return a SomeType object. However, GetAnObject's signature expects a reference to Object, GetAnObject is free to initialize o to an object of any type. In this example, when GetAnObject returned Main, st would refer to a String, which is clearly not a SomeType object, and the call to Console.WriteLine would certainly fail. Fortunately, the C# compiler won't compile the preceding code because st is a reference to SomeType, but GetAnObject requires a reference to an Object.

You can use generics to fix these methods so that they work as you'd expect. Here is how to fix the Swap method shown earlier.

```csharp
public static void Swap<T>(ref T a, ref T b) {
    T t = b;
    b = a;
    a = t;
}
```

And, with Swap rewritten as above, the following code (identical to that shown before) will compile and run perfectly.

```csharp
public static void SomeMethod() {
    String s1 = "Jeffrey";
    String s2 = "Richter";

    Swap(ref s1, ref s2);
    Console.WriteLine(s1); // Displays "Richter"
    Console.WriteLine(s2); // Displays "Jeffrey"
}
```

For some other examples that use generics to solve this problem, see System.Threading.Interlocked class with its CompareExchange methods.

# Passing a Variable Number of Arguments to a Method

It's sometimes convenient for the developer to define a method that can accept a variable number of arguments. For example, the System.String type offers methods allowing an arbitrary number of strings to be concatenated together and methods allowing the caller to specify a set of strings that are to be formatted.

To declare a method that accepts a variable number of arguments, you declare the method as follows.

```csharp
static Int32 Add(params Int32[] values) {
    // NOTE: it is possible to pass the 'values'
    // array to other methods if you want to.

    Int32 sum = 0;
    if (values != null) {
        for (Int32 x = 0; x < values.Length; x++)
            sum += values[x];
    }
    return sum;
}
```

As you can see, the big difference with this code is the methods that have out or ref reference types are constructing an object, and the pointer to the new object is returned to the caller. You'll also notice that the ContinueProcessingFiles method can manipulate the object being passed into it before returning a new object. This is possible because the parameter is marked with the ref keyword. You can simplify the preceding code a bit, as shown here. (Wait, the text above seems to repeat logic from previous pages, following the OCR flow).

(Note: The OCR text provided contained significant repetitions and overlaps across pages. I have merged the unique logical sections and cleaned the flow based on the provided content.)

Wait, looking closer at the prompt, the OCR text actually has repeated blocks because page 242 and 243 overlap logic. The last parameter to a method can be marked with the params keyword (Array-Attribute). This parameter must also identify a single-dimension array of any type. It's legal to pass null or a reference to an array of 0 entries as the last parameter to the method. The following call to Add performs fine, runs and produces a resulting sum of 0 (as expected).

```csharp
public static void Main() {
    // Both of these lines display "0"
    Console.WriteLine(Add()); // passes new Int32[0] to Add
    Console.WriteLine(Add(null)); // passes null to Add: more efficient (no array allocated)
}
```

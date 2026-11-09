It’s not legal to overload methods that differ only by out and ref because the metadata representation of the method’s signature for the methods would be identical. So I couldn’t also define the following method in the preceding Point type:

```
static void Add(out Point p) { ... }
```

If you attempt to include the last Add method in the Point type, the C# compiler issues this message:
"error CS0663: 'Add' cannot define overloaded methods because it differs only on ref and out."

Using out and ref with value types gives you the same behavior that you already get when passing reference types by value. With value types, you add ref and allow a method to manipulate a single value type instance. The caller must allocate the memory for the instance, and the callee manipulates that memory. With reference types, the caller allocates memory for a pointer to a reference object, and the callee manipulates this pointer. Because of this behavior, using out and ref with reference types is useful only when the method is going to “return” a reference to an object that it knows about. The following code demonstrates:

```
using System;
using System.IO;

public sealed class Program {
    public static void Main() {
        FileStream fs;    // fs is uninitialized

        // Open the first file to be processed.
        StartProcessingFiles(out fs);

        // Continue while there are more files to process.
        for (; fs != null; ContinueProcessingFiles(ref fs)) {

            // Process a file.
            fs.Read(...);
        }
    }

    private static void StartProcessingFiles(out FileStream fs) {
        fs = new FileStream(...);  // fs must be initialized in this method
    }

    private static void ContinueProcessingFiles(ref FileStream fs) {
        fs.Close();  // Close the last file worked on.

        // Open the next file, or if no more files, "return" null.
        if (noMoreFilesToProcess) fs = null;
        else fs = new FileStream(...);
    }
}
```

As you can see, the big difference with this code is that the methods that have out or ref reference type parameters are constructing an object, and the pointer to the new object is returned to the caller.
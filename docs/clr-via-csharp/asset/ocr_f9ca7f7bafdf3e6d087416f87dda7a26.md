As you can see, the code is pretty verbose; it would be nice if there were some shorthand way to refer to the **FileStream** and **StringBuilder** types to reduce typing. Fortunately, many compilers do offer mechanisms to reduce programmer typing. The C# compiler provides this mechanism via the **using** directive. The following code is identical to the previous example:

```
using System.IO;    // Try prepending "System.IO."
using System.Text;  // Try prepending "System.Text."

public sealed class Program {
    public static void Main() {
        FileStream fw = new FileStream(...);
        StringBuilder sb = new StringBuilder();
    }
}
```

To the compiler, a namespace is simply an easy way of making a type’s name longer and more likely to be unique by preceding the name with some symbols separated by dots. So the compiler interprets the reference to **FileStream** in this example to mean **System.IO.FileStream**. Similarly, the compiler interprets the reference to **StringBuilder** to mean **System.Text.StringBuilder**.

Using the C# **using** directive is entirely optional; you’re always welcome to type out the fully qualified name of a type if you prefer. The C# **using** directive instructs the compiler to try prepending different prefixes to a type name until a match is found.

> **Important** The CLR doesn’t know anything about namespaces. When you access a type, the CLR needs to know the full name of the type (which can be a really long name containing periods) and which assembly contains the definition of the type so that the runtime can load the proper assembly, find the type, and manipulate it.

In the previous code example, the compiler needs to ensure that every type referenced exists and that my code is using that type in the correct way: calling methods that exist, passing the right number of arguments to these methods, ensuring that the arguments are the right type, using the method’s return value correctly, and so on. If the compiler can’t find a type with the specified name in the source files or in any referenced assemblies, it prepends **System.IO.** to the type name and checks if the generated name matches an existing type. If the compiler still can’t find a match, it prepends **System.Text.** to the type’s name. The two **using** directives shown earlier allow me to simply type **FileStream** and **StringBuilder** in my code—the compiler automatically expands the references to **System.IO.FileStream** and **System.Text.StringBuilder**. I’m sure you can easily imagine how much typing this saves, as well as how much cleaner your code is to read.

When checking for a type’s definition, the compiler must be told which assemblies to examine by using the **/reference** compiler switch as discussed in Chapter 2, “Building, Packaging, Deploying, and Administering Applications and Types,” and Chapter 3, “Shared Assemblies
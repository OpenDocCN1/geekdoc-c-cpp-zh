which produces an executable assembly named hello.exe. The output produced by this application when it is run is

```
Hello, world
```

The “Hello, World” program starts with a using directive that references the System namespace. Namespaces provide a hierarchical means of organizing C# programs and libraries. Namespaces contain types and other namespaces—for example, the System namespace contains a number of types, such as the Console class referenced in the program, and a number of other namespaces, such as IO and Collections. A using directive that references a given namespace enables unqualified use of the types that are members of that namespace. Because of the using directive, the program can use Console.WriteLine as shorthand for System.Console.WriteLine.

The Hello class declared by the “Hello, World” program has a single member, the method named Main. The Main method is declared with the static modifier. While instance methods can reference a particular enclosing object instance using the keyword this, static methods operate without reference to a particular object. By convention, a static method named Main serves as the entry point of a program.

The output of the program is produced by the writeLine method of the Console class in the System namespace. This class is provided by the .NET Framework class libraries, which, by default, are automatically referenced by the Microsoft C# compiler. Note that C# itself does not have a separate runtime library. Instead, the .NET Framework is the runtime library of C#.

# 1.2 Program structure

The key organizational concepts in C# are programs, namespaces, types, members, and assemblies. C# programs consist of one or more source files. Programs declare types, which contain members and can be organized into namespaces. Classes and interfaces are examples of types. Fields, methods, properties, and events are examples of members. When C# programs are compiled, they are physically packaged into assemblies. Assemblies typically have the file extension .exe or .dll, depending on whether they implement applications or libraries.

The example

```
using System;
namespace Acme.Collections
{
    public class Stack
    {
        Entry top;
        public void Push(object data) {
            top = new Entry(top, data);
        }

        public object Pop() {
            if (top == null) throw new InvalidOperationException();
            object result = top.data;
            top = top.next;
            return result;
        }
    class Entry
    {
        public Entry next;
        public object data;
    }
```
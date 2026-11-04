
type name MyClass was known in advance and used in a typeof statement to obtain a Type object upon which all of the reflection methods either directly or indirectly operated. Although this might be useful in a number of circumstances, the full power of reflection is found when the types available to a program are determined dynamically by analyzing the contents of other assemblies.

As you know from Chapter 16, an assembly carries with it type information about the classes, structures, and so on, that it contains. The Reflection API allows you to load an assembly, discover information about it, and create instances of any of its publicly available types. Using this mechanism, a program can search its environment, utilizing functionality that might be available without having to explicitly define that functionality at compile time. This is an extremely potent, and exciting, concept. For example, you can imagine a program that acts as a "type browser," displaying the types available on a system. Another application could be a design tool that lets you visually "wire together" a program that is composed of the various types supported by the system. Since all information about a type is discoverable, there is no inherent limitation to the ways reflection can be applied.

To obtain information about an assembly, you will first create an Assembly object. The Assembly class does not define a public constructor. Instead, an Assembly object is obtained by calling one of its methods. The one we will use is LoadFrom(), which loads an assembly given its filename. The form we will use is shown here:

```
static Assembly LoadFrom(string filename)
```

Here, filename specifies the filename of the assembly.

Once you have obtained an Assembly object, you can discover the types that it defines by calling GetTypes() on it. Here is its general form:

```
Type[] GetTypes()
```

It returns an array of the types contained in the assembly.

To demonstrate the discovery of types in an assembly, you will need two files. The first will contain a set of classes that will be discovered by the second. To begin, create a file called MyClasses.cs that contains the following:

```
// A file that contains three classes. Call this file MyClasses.cs.

using System;

class MyClass {
    int x;
    int y;

    public MyClass(int i) {
        Console.WriteLine("Constructing MyClass(int). ");
        x = y = i;
        Show();
    }

    public MyClass(int i, int j) {
        Console.WriteLine("Constructing MyClass(int, int). ");
        x = i;
        y = j;
        Show();
    }

    public int Sum() {
        return x*y;
    }

    public bool IsBetween(int i) {
        if((x < i) && (i < y)) return true;
        else return false;
    }

    public void Set(int a, int b) {
        Console.Write("Inside Set(int, int). ");
        x = a;
        y = b;
        Show();
    }

    // Overload Set.
    public void Set(double a, double b) {
        Console.Write("Inside Set(double, double). ");
        x = (int) a;
        y = (int) b;
        Show();
    }

    public void Show() {
        Console.WriteLine("Values are x: {0}, y: {1}", x, y);
    }
}

class AnotherClass {
    string msg;

    public AnotherClass(string str) {
        msg = str;
    }

    public void Show() {
        Console.WriteLine(msg);
    }
}

class Demo {
    static void Main() {
        Console.WriteLine("This is a placeholder.");
    }
}
```

This file contains MyClass, which we have been using in the previous examples. It also adds a second class called AnotherClass and a third class called Demo. Thus, the assembly

produced by this program will contain three classes. Next, compile this file so the file MyClasses.exe is produced. This is the assembly that will be interrogated.

The program that will discover information about MyClasses.exe is shown here. Enter it at this time.

```
/* Locate an assembly, determine types, and create
an object using reflection. */

using System;
using System.Reflection;

class ReflectAssemblyDemo {
    static void Main() {
        int val;

        // Load the MyClasses.exe assembly.
        Assembly asm = Assembly.LoadFrom("MyClasses.exe");

        // Discover what types MyClasses.exe contains.
        Type[] alltypes = asm.GetTypes();
        foreach(Type temp in alltypes)
            Console.WriteLine("Found: " + temp.Name);

        Console.WriteLine();

        // Use the first type, which is MyClass in this case.
        Type t = alltypes[0]; // use first class found
        Console.WriteLine("Using: " + t.Name);

        // Obtain constructor info.
        ConstructorInfo[] ci = t.GetConstructors();

        Console.WriteLine("Available constructors: ");
        foreach(ConstructorInfo c in ci) {
            // Display return type and name.
            Console.Write("  " + t.Name + "(");

            // Display parameters.
            ParameterInfo[] pi = c.GetParameters();

            for(int i=0; i < pi.Length; i++) {
                Console.Write(pi[i].ParameterType.Name +
                    " " + pi[i].Name);
                if(i+1 < pi.Length) Console.Write(", ");
            }
            Console.WriteLine(")");
        }
        Console.WriteLine();

        // Find matching constructor.
        int x;

        for(x=0; x < ci.Length; x++) {
            ParameterInfo[] pi = ci[x].GetParameters();
            if (pi.Length == 2) break;
        }
        if (x == ci.Length) {
            Console.WriteLine("No matching constructor found.");
            return;
        }
        else
            Console.WriteLine("Two-parameter constructor found.\n");

        // Construct the object.
        object[] consargs = new object[2];
        consargs[0] = 10;
        consargs[1] = 20;
        object reflectOb = ci[x].Invoke(consargs);

        Console.WriteLine("\nInvoking methods on reflectOb.");
        Console.WriteLine();
        MethodInfo[] mi = t.GetMethods();

        // Invoke each method.
        foreach (MethodInfo m in mi) {
            // Get the parameters.
            ParameterInfo[] pi = m.GetParameters();

            if (m.Name.CompareTo("Set")==0 && pi[0].ParameterType == typeof(int)) {
                // This is Set(int, int).
                object[] args = new object[2];
                args[0] = 9;
                args[1] = 18;
                m.Invoke(reflectOb, args);
            }
            else if (m.Name.CompareTo("Set")==0 && pi[0].ParameterType == typeof(double)) {
                // This is Set(double, double).
                object[] args = new object[2];
                args[0] = 1.12;
                args[1] = 23.4;
                m.Invoke(reflectOb, args);
            }
            else if (m.Name.CompareTo("Sum")==0) {
                val = (int) m.Invoke(reflectOb, null);
                Console.WriteLine("sum is " + val);
            }
            else if (m.Name.CompareTo("IsBetween")==0) {
                object[] args = new object[1];
                args[0] = 14;
                if ((bool) m.Invoke(reflectOb, args))
                    Console.WriteLine("14 is between x and y");
            }
            else if (m.Name.CompareTo("Show")==0) {
                m.Invoke(reflectOb, null);
            }
        }
    }
}
```

The output from the program is shown here:

```
Found: MyClass
Found: AnotherClass
Found: Demo

Using: MyClass
Available constructors:
    MyClass(Int32 i)
    MyClass(Int32 i, Int32 j)

Two-parameter constructor found.

Constructing MyClass(int, int).
Values are x: 10, y: 20

Invoking methods on reflectOb.

sum is 30
14 is between x and y
Inside Set(int, int). Values are x: 9, y: 18
Inside Set(double, double). Values are x: 1, y: 23
Values are x: 1, y: 23
```

As the output shows, all three classes contained within MyClasses.exe were found. The first one, which in this case was MyClass, was then used to instantiate an object and execute methods.

The types in MyClasses.exe are discovered using this sequence of code, which is near the start of Main():

```
// Load the MyClasses.exe assembly.
Assembly asm = Assembly.LoadFrom("MyClasses.exe");

// Discover what types MyClasses.exe contains.
Type[] alltypes = asm.GetTypes();
foreach(Type temp in alltypes)
    Console.WriteLine("Found: " + temp.Name);
```

You can use such a sequence whenever you need to dynamically load and interrogate an assembly.

```
csc /t:library MyClasses.cs
```

then the output file would be MyClasses.dll. One advantage to putting code into a DLL is that no Main() method is required. All exe files require an entry point, such as Main(), that

defines where execution begins. This is why the Demo class contained a placeholder Main() method. Such a method is not required by a DLL. If you try making MyClass into a DLL, you will need to change the call to LoadFrom() as shown here:

```
Assembly asm = Assembly.LoadFrom("MyClasses.dll");
```

## Fully Automating Type Discovery

Before we leave the topic of reflection, one last example will be instructive. Even though the preceding program was able to fully use MyClass without explicitly specifying MyClass in the program, it still relied upon prior knowledge of the contents of MyClass. For example, the program knew the names of its methods, such as Set and Sum. However, using reflection it is possible to utilize a type about which you have no prior knowledge. To do this, you must discover all information necessary to construct an object and to generate method calls. Such an approach would be useful to a visual design tool, for example, because it could utilize the types available on the system.

To see how the full dynamic discovery of a type can be accomplished, consider the following example, which loads the MyClasses.exe assembly, constructs a MyClass object, and then calls all of the methods declared by MyClass, all without assuming any prior knowledge:

```
// Utilize MyClass without assuming any prior knowledge.

using System;
using System.Reflection;

class ReflectAssemblyDemo {
    static void Main() {
        int val;
        Assembly asm = Assembly.LoadFrom("MyClasses.exe");

        Type[] alltypes = asm.GetTypes();

        Type t = alltypes[0]; // use first class found

        Console.WriteLine("Using: " + t.Name);

        ConstructorInfo[] ci = t.GetConstructors();

        // Use first constructor found.
        ParameterInfo[] cpi = ci[0].GetParameters();
        object reflectOb;

        if(cpi.Length > 0) {
            object[] consargs = new object[cpi.Length];

            // Initialize args.
            for(int n=0; n < cpi.Length; n++)
                consargs[n] = 10 + n * 20;

            // Construct the object.
            reflectOb = ci[0].Invoke(consargs);
        } else

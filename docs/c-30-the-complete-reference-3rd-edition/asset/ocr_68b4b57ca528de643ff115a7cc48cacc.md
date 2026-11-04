defines where execution begins. This is why the Demo class contained a placeholder Main() method. Such a method is not required by a DLL. If you try making MyClass into a DLL, you will need to change the call to LoadFrom() as shown here:

```
Assembly asm = Assembly.LoadFrom("MyClasses.dll");
```

# Fully Automating Type Discovery

Before we leave the topic of reflection, one last example will be instructive. Even though the preceding program was able to fully use MyClass without explicitly specifying MyClass in the program, it still relied upon prior knowledge of the contents of MyClass. For example, the program knew the names of its methods, such as Set and Sum. However, using reflection it is possible to utilize a type about which you have no prior knowledge. To do this, you must discover all information necessary to construct an object and to generate method calls. Such an approach would be useful to a visual design tool, for example, because it could utilize the types available on the system.

To see how the full dynamic discovery of a type can be accomplished, consider the following example, which loads the MyClasses.exe assembly, constructs a MyClass object, and then calls all of the methods declared by MyClass, all without assuming any prior knowledge:

```
// Utilize MyClass without assuming any prior knowledge.

using System;
using System.Reflection;

class ReflectAssembleDemo {
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
```
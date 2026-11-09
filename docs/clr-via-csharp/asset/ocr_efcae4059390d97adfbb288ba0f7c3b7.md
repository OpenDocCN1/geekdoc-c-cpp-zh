The **Employee** class shown below defines three different kinds of methods:

```
    internal class Employee {
        // A nonvirtual instance method
        public      Int32    GetYearsEmployed() { ... }

        // A virtual method (virtual implies instance)
        public virtual String GetProgressReport() { ... }

        // A static method
        public static  Employee Lookup(String name) { ... }
    }
```

When the compiler compiles this code, the compiler emits three entries in the resulting assembly's method definition table. Each entry has flags set indicating if the method is instance, virtual, or static.

When code is written to call any of these methods, the compiler emitting the calling code examines the method definition's flags to determine how to emit the proper IL code so that the call is made correctly. The CLR offers two IL instructions for calling a method:

+   - The `call` IL instruction can be used to call static, instance, and virtual methods. When the `call` instruction is used to call a static method, you must specify the type that defines the method that the CLR should call. When the `call` instruction is used to call an instance or virtual method, you must specify a variable that refers to an object. The `call` instruction assumes that this variable is not `null`. In other words, the type of the variable itself indicates which type defines the method that the CLR should call. If the variable's type doesn't define the method, base types are checked for a matching method. The `call` instruction is frequently used to call a virtual method nonvirtually.
+   - The `callvirt` IL instruction can be used to call instance and virtual methods, not static methods. When the `callvirt` instruction is used to call an instance or virtual method, you must specify a variable that refers to an object. When the `callvirt` IL instruction is used to call a nonvirtual instance method, the type of the variable indicates which type defines the method that the CLR should call. When the `callvirt` instruction is used to call a virtual instance method, the CLR discovers the actual type of the object being used to make the call and then calls the method polymorphically. In order to determine the type, the variable being used to make the call must not be `null`. In other words, when compiling this call, the JIT compiler generates code that verifies that the variable's value is not `null`. If it is `null`, the `callvirt` instruction causes the CLR to throw a `NullReferenceException`. This additional check means that the `callvirt` IL instruction executes slightly more slowly than the `call` instruction. Note that this `null` check is performed even when the `callvirt` instruction is used to call a nonvirtual instance method.
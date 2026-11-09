+   2. It allocates memory for the object by allocating the number of bytes required for the specified type from the managed heap; all of these bytes are then set to zero (0).
+   3. It initializes the object's type object pointer and sync block index members.
+   4. The type's instance constructor is called, passing it any arguments (the string "ConstructorParam1" in the preceding example) specified in the call to new. Most compilers automatically emit code in a constructor to call a base class's constructor. Each constructor is responsible for initializing the instance fields defined by the type whose constructor is being called. Eventually, System.Object's constructor is called, and this constructor method does nothing but return.

After new has performed all of these operations, it returns a reference (or pointer) to the newly created object. In the preceding code example, this reference is saved in the variable e, which is of type Employee.

By the way, the new operator has no complementary delete operator; that is, there is no way to explicitly free the memory allocated for an object. The CLR uses a garbage-collected environment (described in Chapter 21) that automatically detects when objects are no longer being used or accessed and frees the object's memory automatically.

# ## Casting Between Types

One of the most important features of the CLR is type safety. At run time, the CLR always knows what type an object is. You can always discover an object's exact type by calling the GetType method. Because this method is nonvirtual, it is impossible for a type to spoof another type. For example, the Employee type can't override the GetType method and have it return a type of SuperHero.

Developers frequently find it necessary to cast an object to various types. The CLR allows you to cast an object to its type or to any of its base types. Your choice of programming language dictates how to expose casting operations to the developer. For example, C# doesn't require any special syntax to cast an object to any of its base types, because casts to base types are considered safe implicit conversions. However, C# does require the developer to explicitly cast an object to any of its derived types because such a cast could fail at run time. The following code demonstrates casting to base and derived types.

```
    // This type is implicitly derived from System.Object.
    internal class Employee {
        ...
    }

    public sealed class Program {
        public static void Main() {
            // No cast needed since new returns an Employee object
            // and Object is a base type of Employee.
            Object o = new Employee();
```
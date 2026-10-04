Now, after the method has been JIT-compiled, the thread starts to execute it and eventually get to the code that calls the constructor. In fact, it is possible that multiple threads will be executing the same method concurrently. The CLR wants to ensure that a type's constructor executes only once per AppDomain. To guarantee this, when a type constructor acquires a mutual exclusive thread synchronization lock. If multiple threads attempt to simultaneously call a static constructor, only one will acquire the lock and the other threads will block. The first thread will execute the code in the static constructor. After the first thread leaves the constructor, the waiting threads will wake up and see that the constructor's code has already been executed. These threads will not execute the code again; they will simply return from the constructor. In addition, if any of these methods ever get called again, the CLR knows that the type constructor has already executed and will ensure that the constructor is not called again.

> Note Because the CLR guarantees that a type constructor executes only once per AppDomain and is thread-safe, a type constructor is a great place to initialize any singleton objects required the type.

Within a single thread, there is a potential problem that can occur if two type constructors reference each other. For example, ClassA has a type constructor containing code that references ClassB, and ClassB has a type constructor containing code that references ClassA. In this situation, the CLR still guarantees that each type constructor executes only once; however, it cannot guarantee that ClassA's type constructor has run before executing ClassB's type constructor. You should certainly try to avoid writing code that sets up this scenario. In fact, because the CLR is responsible for calling type constructors, you should always avoid writing any code that requires type constructors to be called in a specific order.

Finally, if a type constructor throws an unhandled exception, the CLR considers the type to be unusable. Attempting to access any fields or methods of the type will cause a System.TypeInitializationException to be thrown.

The code in a type constructor has access only to a type's static fields, and its usual purpose is to initialize those fields. As it does with instance, C# offers a simple syntax that allows you to initialize a type's static fields.

```
internal sealed class SomeType {
    private static Int32 s_x = 5;
}
```

> Note Although C# doesn't allow a value type to use inline field initialization syntax for instance fields, it does allow you to use it for static fields. In other words, if you change SomeType above from a class to a struct, the code will compile and work as expected.
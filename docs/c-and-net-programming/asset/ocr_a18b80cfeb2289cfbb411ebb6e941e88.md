assigned to FS is early bound. Early Binding is also called static binding or compile time binding.

While performing Early Binding the compiler can ensure at compile time that the function will exist and be callable at runtime. Moreover the compiler guarantees that the function takes the exact number of arguments and that they are of the right type and can checks that the return value is of the correct type.

# Late binding (Dynamic binding)

By contrast, in late binding functions, methods, variables and properties are detected and checked only at the run-time. It implies that the compiler does not know what kind of object or actual type of an object or which methods or properties an object contains until run time. The biggest advantages of late binding is that the Objects of this type can hold references to any object, but lack many of the advantages of early-bound objects

```
object objFS = null;
objFS = CreateObject('Scripting.FileSystemObject');
```

Above code does not require a reference to be set beforehand, the instance creation and type determination will just happen at runtime. It is important to note that the late binding can only be used to access type members that are declared as Public. Accessing members declared as Friend or Protected Friend resulted in a run-time error.

While perform late binding there is a possibility of the target function may not exist. Also the target function may not accept the arguments passed to it, and may have a return value of the wrong type.

# Method Overloading (Early binding) and Method Overriding (Late Binding)

Method Overloading happens at compile time (Early Binding) while Overriding happens at runtime (Late Binding). In method overloading, method call to its definition has happens at compile time (Static Binding) while in method overriding, method call to its definition happens at runtime (Dynamic Binding).

# Q.9 What are sealed classes ?

Ans. : A sealed class, in C#, is a class that cannot be inherited by any class but can be instantiated.

The design intent of a sealed class is to indicate that the class is specialized and there is no need to extend it to provide any additional functionality through inheritance to override its behavior. A sealed class is often used to encapsulate a logic that needs to be used across the program but without any alteration to it.
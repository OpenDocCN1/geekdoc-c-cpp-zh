# # Primary Constraints

A type parameter can specify zero primary constraints or one primary constraint. A primary constraint can be a reference type that identifies a class that is not sealed. You cannot specify one of the following special reference types: **System.Object**, **System.Array**, **System.Delegate**, **System.MulticastDelegate**, **System.ValueType**, **System.Enum**, or **System.Void**.

When specifying a reference type constraint, you are promising the compiler that a specified type argument will either be of the same type or of a type derived from the constraint type. For example, see the following generic class:

```
    internal sealed class PrimaryConstraintOfStream<T> where T : Stream {
        public void M(T stream) {
            stream.Close(); // OK
        }
    }
```

In this class definition, the type parameter T has a primary constraint of **Stream** (defined in the **System.IO** namespace). This tells the compiler that code using **PrimaryConstraintOfStream** must specify a type argument of **Stream** or a type derived from **Stream** (such as **FileStream**). If a type parameter doesn't specify a primary constraint, **System.Object** is assumed. However, the C# compiler issues an error message **"error CS0702: Constraint cannot be special class 'object'"** if you explicitly specify **System.Object** in your source code.

There are two special primary constraints: **class** and **struct**. The **class** constraint promises the compiler that a specified type argument will be a reference type. Any class type, interface type, delegate type, or array type satisfies this constraint. For example, see the following generic class:

```
    internal sealed class PrimaryConstraintOfClass<T> where T : class {
        public void M() {
            T temp = null; // Allowed because T must be a reference type
        }
    }
```

In this example, setting **temp** to **null** is legal because T is known to be a reference type, and all reference type variables can be set to **null**. If T were unconstrained, the code above would not compile because T could be a value type, and value type variables cannot be set to **null**.

The **struct** constraint promises the compiler that a specified type argument will be a value type. Any value type, including enumerations, satisfies this constraint. However, the compiler and the CLR treat any **System.Nullable<T>** value type as a special type, and nullable types do not satisfy this constraint. The reason is because the **Nullable<T>** type constrains its type parameter to **struct**, and the CLR wants to prohibit a recursive type such
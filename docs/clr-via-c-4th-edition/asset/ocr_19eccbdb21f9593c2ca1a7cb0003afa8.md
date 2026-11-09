Attempting to compile the preceding code causes the compiler to issue the following message: error CS0460: Constraints for override and explicit interface implementation methods are inherited from the base method, so they cannot be specified directly. If we remove the two where lines from the Derived class's M<T3, T4> method, the code will compile just fine. Notice that you can change the names of the type parameters (as in the example: from T1 to T3 and T2 to T4); however, you cannot change (or even specify) constraints.

Now let's talk about the different kinds of constraints the compiler/CLR allows you to apply to a type parameter. A type parameter can be constrained by using a primary constraint, a secondary constraint, and/or a constructor constraint. I'll talk about these three kinds of constraints in the next three sections.

# ## Primary Constraints

A type parameter can specify zero primary constraints or one primary constraint. A primary constraint can be a reference type that identifies a class that is not sealed. You cannot specify one of the following special reference types: System.Object, System.Array, System.Delegate, System.MulticastDelegate, System.ValueType, System.Enum, or System.Void.

When specifying a reference type constraint, you are promising the compiler that a specified type argument will either be of the same type or of a type derived from the constraint type. For example, see the following generic class.

```
    internal sealed class PrimaryConstraintOfStream<T> where T : Stream {
        public void M(T stream) {
            stream.Close();// OK
        }
    }
```

In this class definition, the type parameter T has a primary constraint of Stream (defined in the System.IO namespace). This tells the compiler that code using PrimaryConstraintOfStream must specify a type argument of Stream or a type derived from Stream (such as FileStream). If a type parameter doesn't specify a primary constraint, System.Object is assumed. However, the C# compiler issues an error message (error CS0702: Constraint cannot be special class 'object') if you explicitly specify System.Object in your source code.

There are two special primary constraints: class and struct. The class constraint promises the compiler that a specified type argument will be a reference type. Any class type, interface type, delegate type, or array type satisfies this constraint. For example, see the following generic class.

```
    internal sealed class PrimaryConstraintOfClass<T> where T : class {
        public void M() {
            T temp = null;// Allowed because T must be a reference type
        }
    }
```
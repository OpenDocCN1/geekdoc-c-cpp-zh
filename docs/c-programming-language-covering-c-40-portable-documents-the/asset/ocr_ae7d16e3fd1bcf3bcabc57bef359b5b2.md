# 1. Introduction

```
a.Add(2);
List<int> b = new List<int>();
b.Add(1);
b.Add(2);
Console.WriteLine(a == b);    // Outputs "True"
b.Add(3);
Console.WriteLine(a == b);    // Outputs "False"
} }
```

The first Console.WriteLine outputs True because the two lists contain the same number of objects with the same values in the same order. Had List<T> not defined operator ==, the first Console.WriteLine would have output False because a and b reference different List<int> instances.

# 1.6.7.6 Destructors

A destructor is a member that implements the actions required to destruct an instance of a class. Destructors cannot have parameters, they cannot have accessibility modifiers, and they cannot be invoked explicitly. The destructor for an instance is invoked automatically during garbage collection.

The garbage collector is allowed wide latitude in deciding when to collect objects and run destructors. Specifically, the timing of destructor invocations is not deterministic, and destructors may be executed on any thread. For these and other reasons, classes should implement destructors only when no other solutions are feasible.

> VLADIMIR RESHETNIKOV Destructors are sometimes called "finalizers." This name also appears in the garbage collector API—for example, GC.WaitForPendingFinalizers.

The using statement provides a better approach to object destruction.

# 1.7 Structs

Like classes, structs are data structures that can contain data members and function members, but unlike classes, structs are value types and do not require heap allocation. A variable of a struct type directly stores the data of the struct, whereas a variable of a class type stores a reference to a dynamically allocated object. Struct types do not support user-specified inheritance, and all struct types implicitly inherit from type object.
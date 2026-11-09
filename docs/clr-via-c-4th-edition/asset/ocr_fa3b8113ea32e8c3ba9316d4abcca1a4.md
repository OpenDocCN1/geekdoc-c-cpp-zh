```
```csharp
// Using ICloneable, I can call any method declared by the
// ICloneable interface (or any method defined by Object) only.

// The comparable variable refers to the same String object
IComparable comparable = s;
// Using comparable, I can call any method declared by the
// IComparable interface (or any method defined by Object) only.

// The enumerable variable refers to the same String object
// At run time, you can cast a variable from one interface to another as
// long as the object's type implements both interfaces.
IEnumerable enumerable = (IEnumerable) comparable;
// Using enumerable, I can call any method declared by the
// IEnumerable interface (or any method defined by Object) only.
```
```

In this code, all of the variables refer to the same “Jeffrey” String object that is in the managed heap, and therefore, any method that I call while using any of these variables applies to the one “Jeffrey” String object. However, the type of the variable indicates the action that I can perform on the object. The s variable is of type String, and therefore, I can use s to call any members defined by the String type (such as the Length property). I can also use the variable s to call any methods inherited from Object (such as GetType).

The cloneable variable is of the ICloneable interface type, and therefore, using the cloneable variable, I can call the Clone method defined by this interface. In addition, I can call any method defined by Object (such as GetType) because the CLR knows that all types derive from Object. However, using the cloneable variable, I cannot call public methods defined by String itself or any methods defined by any other interface that String implements. Similarly, using the comparable variable, I can call CompareTo or any method defined by Object, but no other methods are callable using this variable.

> > **Important** Like a reference type, a value type can implement zero or more interfaces. However, when you cast an instance of a value type to an interface type, the value type instance must be boxed. This is because an interface variable is a reference that must point to an object on the heap so that the CLR can examine the object's type object pointer to determine the exact type of the object. Then, when calling an interface method with a boxed value type, the CLR will follow the object's type object pointer to find the type object's method table in order to call the proper method.

# ## Implicit and Explicit Interface Method Implementations
(What’s Happening Behind the Scenes)

When a type is loaded into the CLR, a method table is created and initialized for the type (as discussed in Chapter 1, “The CLR’s Execution Model”). This method table contains one entry for every new method introduced by the type as well as entries for any virtual methods inherited by the type.
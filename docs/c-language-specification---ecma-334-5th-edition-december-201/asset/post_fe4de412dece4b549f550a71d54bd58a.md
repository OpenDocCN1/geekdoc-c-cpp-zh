
An operator ++ or operator -- implementation can be invoked using either postfix or prefix notation.
It is not possible to have separate operator implementations for the two notations.

## 12.7.11 The new operator

### 12.7.11.1 General

The new operator is used to create new instances of types.

There are three forms of new expressions:

- Object creation expressions and anonymous object creation expressions are used to create new instances of class types and value types.
- Array creation expressions are used to create new instances of array types.
- Delegate creation expressions are used to obtain instances of delegate types.

The new operator implies creation of an instance of a type, but does not necessarily imply allocation of memory. In particular, instances of value types require no additional memory beyond the variables in which they reside, and no allocations occur when new is used to create instances of value types.

> [Note: Delegate creation expressions do not always create new instances. When the expression is processed in the same way as a method group conversion (§11.8) or an anonymous function conversion (§11.7) this may result in an existing delegate instance being reused. end note]

### 12.7.11.2 Object creation expressions

An object-creation-expression is used to create a new instance of a class-type or a value-type.

```
object-creation-expression:
  new type ( argument-list_opt ) object-or-collection-initializer_opt
  new type object-or-collection-initializer

object-or-collection-initializer:
  object-initializer
  collection-initializer
```

The type of an object-creation-expression shall be a class-type, a value-type, or a type-parameter. The type cannot be an abstract or static class-type.

- If no value type constraint or constructor constraint (§15.2.5) has been specified for T, a binding-time error occurs.
- The result of the object-creation-expression is a value of the run-time type that the type parameter has been bound to, namely the result of invoking the default constructor of that type. The run-time type may be a reference type or a value type.

- Otherwise, if T is a class-type or a struct-type:
  - If T is an abstract or static class-type, a compile-time error occurs.
  - The instance constructor to invoke is determined using the overload resolution rules of §12.6.4. The set of candidate instance constructors consists of all accessible instance constructors declared in T, which are applicable with respect to A (§12.6.4.2). If the set of candidate instance constructors is empty, or if a single best instance constructor cannot be identified, a binding-time error occurs.
  - The result of the object-creation-expression is a value of type T, namely the value produced by invoking the instance constructor determined in the step above.
  - Otherwise, the object-creation-expression is invalid, and a binding-time error occurs.

Even if the object-creation-expression is dynamically bound, the compile-time type is still T.

The run-time processing of an object-creation-expression of the form new T(A), where T is class-type or a struct-type and A is an optional argument-list, consists of the following steps:

- If T is a class-type:
  - A new instance of class T is allocated. If there is not enough memory available to allocate the new instance, a System.OutOfMemoryException is thrown and no further steps are executed.
  - All fields of the new instance are initialized to their default values (§10.3).
  - The instance constructor is invoked according to the rules of function member invocation (§12.6.6). A reference to the newly allocated instance is automatically passed to the instance constructor and the instance can be accessed from within that constructor as this.

- If T is a struct-type:
  - An instance of type T is created by allocating a temporary local variable. Since an instance constructor of a struct-type is required to definitely assign a value to each field of the instance being created, no initialization of the temporary variable is necessary.
  - The instance constructor is invoked according to the rules of function member invocation (§12.6.6). A reference to the newly allocated instance is automatically passed to the instance constructor and the instance can be accessed from within that constructor as this.

### 12.7.11.3 Object initializers

An object initializer specifies values for zero or more fields or properties of an object.

```
object-initializer:
    { member-initializer-list_opt }
    { member-initializer-list , }

member-initializer-list:
    member-initializer
    member-initializer-list , member-initializer

member-initializer:
    identifier = initializer-value

initializer-value:
    expression
    object-or-collection-initializer
```

An object initializer consists of a sequence of member initializers, enclosed by { and } tokens and separated by commas. Each member initializer shall name an accessible field or property of the object being initialized, followed by an equals sign and an expression or an object initializer or collection initializer. It is an error for an object initializer to include more than one member initializer for the same field or property. It is not possible for the object initializer to refer to the newly created object it is initializing.

A member initializer that specifies an expression after the equals sign is processed in the same way as an assignment (§12.18.2) to the field or property.

A member initializer that specifies an object initializer after the equals sign is a nested object initializer, i.e., an initialization of an embedded object. Instead of assigning a new value to the field or property, the assignments in the nested object initializer are treated as assignments to members of the field or property. Nested object initializers cannot be applied to properties with a value type, or to read-only fields with a value type.

A member initializer that specifies a collection initializer after the equals sign is an initialization of an embedded collection. Instead of assigning a new collection to the field or property, the elements given in the initializer are added to the collection referenced by the field or property. The field or property shall be of a collection type that satisfies the requirements specified in §12.7.11.4.

[Example: The following class represents a point with two coordinates:

```
public class Point
{
    int x, y;
    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

An instance of Point can be created and initialized as follows:

```
Point a = new Point { X = 0, Y = 1 };
```

which has the same effect as

```
Point __a = new Point();
__a.X = 0;
__a.Y = 1;
Point a = __a;
```

where __a is an otherwise invisible and inaccessible temporary variable. The following class represents a rectangle created from two points:

```
public class Rectangle
{
    Point p1, p2;
    public Point P1 { get { return p1; } set { p1 = value; } }
    public Point P2 { get { return p2; } set { p2 = value; } }
}
```

An instance of Rectangle can be created and initialized as follows:

```
Rectangle r = new Rectangle {
    P1 = new Point { X = 0, Y = 1 },
    P2 = new Point { X = 2, Y = 3 }
};
```

which has the same effect as

```
Rectangle __r = new Rectangle();
Point __p1 = new Point();
__p1.X = 0;
__p1.Y = 1;
__r.P1 = __p1;
Point __p2 = new Point();
__p2.X = 2;
__p2.Y = 3;
__r.P2 = __p2;
Rectangle r = __r;
```

where __r, __p1 and __p2 are temporary variables that are otherwise invisible and inaccessible.

If Rectangle's constructor allocates the two embedded Point instances

```
public class Rectangle
{
    Point p1 = new Point();
    Point p2 = new Point();
    public Point P1 { get { return p1; } }
    public Point P2 { get { return p2; } }
}
```

the following construct can be used to initialize the embedded Point instances instead of assigning new instances:

```
Rectangle r = new Rectangle {
    P1 = { X = 0, Y = 1 },
    P2 = { X = 2, Y = 3 }
};
```

which has the same effect as

```
Rectangle __r = new Rectangle();
__r.P1.X = 0;
__r.P1.Y = 1;
__r.P2.X = 2;
__r.P2.Y = 3;
Rectangle r = __r;
```

end example]

### 12.7.11.4 Collection initializers

A collection initializer specifies the elements of a collection.

```
collection-initializer:
    { element-initializer-list }
    { element-initializer-list , }

element-initializer-list:
    element-initializer
    element-initializer-list , element-initializer

element-initializer:
    non-assignment-expression
    { expression-list }

expression-list:
    expression
    expression-list , expression
```

A collection initializer consists of a sequence of element initializers, enclosed by { and } tokens and separated by commas. Each element initializer specifies an element to be added to the collection object being initialized, and consists of a list of expressions enclosed by { and } tokens and separated by commas. A single-expression element initializer can be written without braces, but cannot then be an assignment

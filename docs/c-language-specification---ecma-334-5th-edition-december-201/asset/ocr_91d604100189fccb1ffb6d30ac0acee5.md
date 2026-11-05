+   - Assignment to a variable of a struct type creates a copy of the value being assigned (§16.4.4).
+   - The default value of a struct is the value produced by setting all fields to their default value (§16.4.5).
+   - Boxing and unboxing operations are used to convert between a struct type and certain reference types (§16.4.6).
+   - The meaning of this is different within struct members (§16.4.7).
+   - Instance field declarations for a struct are not permitted to include variable initializers (§16.4.8).
+   - A struct is not permitted to declare a parameterless instance constructor (§16.4.9).
+   - A struct is not permitted to declare a finalizer.

# 16.4.2 Value semantics

Structs are value types (§9.3) and are said to have value semantics. Classes, on the other hand, are reference types (§9.2) and are said to have reference semantics.

A variable of a struct type directly contains the data of the struct, whereas a variable of a class type contains a reference to an object that contains the data. When a struct B contains an instance field of type A and A is a struct type, it is a compile-time error for A to depend on B or a type constructed from B. A struct X directly depends on a struct Y if X contains an instance field of type Y. Given this definition, the complete set of structs upon which a struct depends is the transitive closure of the directly depends on relationship.

```
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```

is an error because Node contains an instance field of its own type. Another example

```
struct A { B b; }
struct B { C c; }
struct C { A a; }
```

is an error because each of the types A, B, and C depend on each other. end example

With classes, it is possible for two variables to reference the same object, and thus possible for operations on one variable to affect the object referenced by the other variable. With structs, the variables each have their own copy of the data (except in the case of ref and out parameter variables), and it is not possible for operations on one to affect the other. Furthermore, except when explicitly nullable (§9.3.11), it is not possible for values of a struct type to be null. [Note: If a struct contains a field of reference type then the contents of the object referenced can be altered by other operations. However the value of the field itself, i.e., which object it references, cannot be changed through a mutation of a different struct value. end note]

```
struct Point
{
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

the code fragment

Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);
```
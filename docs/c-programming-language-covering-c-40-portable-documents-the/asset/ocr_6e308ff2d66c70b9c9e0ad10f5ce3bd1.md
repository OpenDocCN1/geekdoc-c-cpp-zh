A variable of a struct type directly contains the data of the struct, whereas a variable of a class type contains a reference to the data, the latter known as an object. When a struct B contains an instance field of type A and A is a struct type, it is a compile-time error for A to depend on B. A struct X directly depends on a struct Y if X contains an instance field of type Y. Given this definition, the complete set of structs upon which a struct depends is the transitive closure of the directly depends on relationship. For example,

```
struct Node
{
    int data;
    Node next; // Error: Node directly depends on itself
}
```

is an error because Node contains an instance field of its own type. Another example

```
struct A { B b; }
struct B { C c; }
struct C { A a; }
```

is an error because each of the types A, B, and C depend on each other.

With classes, it is possible for two variables to reference the same object, and thus possible for operations on one variable to affect the object referenced by the other variable. With structs, each of the variables has its own copy of the data (except in the case of ref and out parameter variables), and it is not possible for operations on one to affect the others. Furthermore, because structs are not reference types, it is not possible for values of a struct type to be null.

Given the declaration

```
struct Point
{
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

the code fragment

```
Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);
```
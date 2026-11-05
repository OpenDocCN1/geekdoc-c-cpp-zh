# C# LANGUAGE SPECIFICATION

The static constructor for a closed class type executes at most once in a given application domain. The execution of a static constructor is triggered by the first of the following events to occur within an application domain:

+   - An instance of the class type is created.
+   - Any of the static members of the class type are referenced.

If a class contains the Main method (§3.1) in which execution begins, the static constructor for that class executes before the Main method is called.

To initialize a new closed class type, first a new set of static fields (§10.5.1) for that particular closed type is created. Each of the static fields is initialized to its default value (§5.2). Next, the static field initializers (§10.4.5.1) are executed for those static fields. Finally, the static constructor is executed.

The example

```
```csharp
using System;
class Test
{
    static void Main() {
        A.F();
        B.F();
    }
}
class A
{
    static A() {
        Console.WriteLine("Init A");
    }
    public static void F() {
        Console.WriteLine("A.F");
    }
}
class B
{
    static B() {
        Console.WriteLine("Init B");
    }
    public static void F() {
        Console.WriteLine("B.F");
    }
}
```
```

must produce the output:

```
```
Init A
A.F
Init B
B.F
```
```

because the execution of A's static constructor is triggered by the call to A.F, and the execution of B's static constructor is triggered by the call to B.F.

It is possible to construct circular dependencies that allow static fields with variable initializers to be observed in their default value state.

The example

```
```csharp
using System;
```
```
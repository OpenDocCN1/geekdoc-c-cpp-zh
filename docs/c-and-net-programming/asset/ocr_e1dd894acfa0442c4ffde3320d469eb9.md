```
```csharp
{
    Console.WriteLine("Batsman Constructor.");
}

public static void Main()
{
    Batsman bat = new Batsman();

    bat.print();
}
}
```
```

# Output

```
```text
Player Constructor.
Batsman Constructor.
I am a Player.
```
```

# 7.  Polymorphism

+   1. Polymorphism means one name, many forms. The word *Polymorphism* means having many forms. Many forms of a single object is called Polymorphism.
+   2. Generally, polymorphism can be achieved when there is a hierarchy of classes and they are related by inheritance.
+   3. One function is made to behave in different forms based on its invoking object and parameters to it.
+   4. There are two types of polymorphism -

# Compile time polymorphism :

+   i) In this polymorphism, compiler identifies which polymorphism form it has to take and evaluate at compile time only hence, is called as *compile time polymorphism* or *early binding*.
+   ii) Early binding is achieved by *Method Overloading* and *Operator Overloading*. The *Method Overloading* means more than one method having same name but different signatures (or parameters) in the same or different class.
+   iii) Advantage of early binding is that execution becomes fast because everything about the method is known to compiler during compilation process itself.
+   iv) The main disadvantage is it lacks flexibility of runtime decision.

# Runtime polymorphism :

+   i) In this polymorphism, compiler identifies which polymorphism form it has to take and evaluate at runtime is called as *runtime polymorphism* or *late binding*.
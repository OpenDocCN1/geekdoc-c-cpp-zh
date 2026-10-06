
# Classes 43

## Example 52 Method Name Overloading and Signatures
This class declares four overloaded methods M whose signatures are M(int) and M(bool) and M(int, double) and M(double, double). Some of the overloaded methods are static, others are instance methods. The overloaded methods have different types, as shown here. 92 explains the method calls.

It would be legal to declare an additional method with signature M(double, int), but then the method call M(10, 20) would become ambiguous and illegal. Namely, there is no best signature among M(double, double) and M(int, double) or M(double, int); see section 12.17.1.

```csharp
public class Overloading {
    double M(int i) { return i; }
    bool M(bool b) { return b; }
    static double M(int x, double y) { return x + y + 1; }
    static double M(double x, double y) { return x + y + 3; }
}
```

```csharp
public static void main(String[] args) {
    Console.WriteLine(M(10, 20));      // Print 31
    Console.WriteLine(M(10, 20.0));    // Print 31
    Console.WriteLine(M(10.0, 20));    // Print 33
    Console.WriteLine(M(10.0, 20.0));  // Print 33
}
```

## Example 53 Method Overriding

In the vessel hierarchy (example 45), the classes Tank and Barrel override the method ToString inherited from the universal base class Object, and class Cube overrides inherited from class Tank.

## Example 54 Parameter Arrays and Overloading

This example declares three overloads of the method Max, including one with a parameter array (params). When the params overload is called, the first argument will be bound to parameter xr of Max, and all remaining arguments will be stored in a new array, bound to the parameter xr. Example 95 shows several ways to these methods. Example 149 demonstrates a parameter array in an indexer.

```csharp
public static int Max(int a, double b) {
    return a > b ? a : (int)b;
}

public static int Max(int a, int b, int c) {
    a = a > b ? a : b;
    return a > c ? a : c;
}

public static int Max(int xo, params int[] xr) {
    foreach (int i in xr) {
        if (i > xo)
            xo = i;
    }
    return xo;
}
```

# 10.8 Method Modifiers static new virtual override sealed abstract

The modifiers are used in method declarations (section 10.7), property declarations (section 10.15), and indexer declarations (section 10.16). See also section 10.3 for member access modifiers. The following-modifiers are legal (in classes C, structs S, or interfaces I):

| Method Modifier | Meaning for This Method | Allowable Base Class Method | In |
| --- | --- | --- | --- |
| static | Static method | No method, private | CS- |
| new static | Static method; hide base | Any method | CS- |
| new | Non-virtual instance method | No method, private | CSI |
| virtual | Virtual method | No method, private | C- |
| override | Virtual; override base | virtual/override/abstract | CS- |
| sealed override | Virtual; prevent further overriding | abstract | C- |
| new virtual | Virtual; hide base | Any method | C-- |
| abstract | Virtual and abstract; no body | No method, private | C-- |
| abstract override | Virtual and abstract; override base | abstract | C-- |
| new abstract | Virtual and abstract; hide base | Any method | C-- |

When a method's accessibility (section 10.3) is not explicitly specified, it defaults to private, which is not permitted for methods that are abstract, virtual, or override. There are several kinds of methods:

- *A static method is a method M (in a class or type C) that is declared. Then M is associated with the class itself; it can be called without any object of class C. The method may be called as C.M(...) or inside methods, constructors, field initializers, initializer blocks and nested classes in C, simply as M(...). A static method cannot use the current object reference this and can only refer to static members of the enclosing class.
- *An instance method is a method M (in a class or type C) that is not declared. Then every call to M is associated with an instance of class C or a subclass. The method may be called as O.M(...), where O is an object of class C or a subclass. Instance methods and constructors of C, it may be called as M(...), which has the same meaning as M(...). An instance method can refer to all members of class C, static or not. There are two kinds of instance methods:
    - *A non-virtual instance method is one not declared virtual or override. In a call O.M(...) to such a method, the compile-time type of O determines which method is called (section 12.17.5).
    - *An instance method is one declared virtual or override. In a call O.M(...) to such a method, the compile-time type of O and the run-time type of the object determine which method is called (section 12.17.5). Only classes have virtual instance methods; structs types (section 14). A sealed method cannot be overridden in subclasses. The combination sealed virtual is illegal; that would just mean.
- *An abstract method is a method M (in a class C) declared abstract. Then class C must be abstract, so cannot be instantiated. The declaration of an abstract method has no method body:

abstract method-modifiers retype M(format-list);

# Classes 45

**Example 55 Inheritance, Hiding, and Overriding**
The class A declares static method M1, non-virtual instance method M2, virtual method M3, and abstract method M4. Class B overrides M4 and inherits the other classes. Class C hides the static M1 by a static method M1 and hides M2 by a new non-virtual M2, and overrides the virtual M3. Abstract class D hides non-virtual method M2 and virtual method M3 and overrides M4 by an abstract method. Class E overrides M2 and M4 with virtual methods. Classes methods are shown in example 97.

```csharp
abstract class A {
    public static void M1() { Console.Write("A.M1"); }
    public virtual void M2() { Console.Write("A.M2"); }
    public virtual void M3() { Console.Write("A.M3"); }
    public abstract void M4();
}
class B : A {
    public override void M4() { Console.Write("B.M4"); }
}
class C : B {
    public static new void M1() { Console.Write("C.M1"); }
    public new void M2() { Console.Write("C.M2"); }
    public override void M3() { Console.Write("C.M3"); }
}
abstract class D : C {
    public new abstract void M2();
    public new virtual void M3() { Console.Write("D.M3"); }
    public abstract override void M4();
}
class E : D {
    public sealed override void M2() { Console.Write("E.M2"); }
    public override void M3() { Console.Write("E.M3"); }
    public override void M4() { Console.Write("E.M4"); }
}
```

**Example 56 Static Initializers and Static Constructor**
The initializer of static field creates an array and binds it to ps. The static constructor fills it with random numbers. This is useful for generating a sequence of 1.0.

```csharp
class InitializerExample {
    static double[] ps = new double[6];
    static readonly rnd = new Random();
    static InitializerExample() { // Static constructor
        double sum = 0;
        for (int i=0; i<ps.Length; i++) { // Fills ps with random numbers
            ps[i] = rnd.NextDouble(); // Random number 0 <= x < 1
            sum += ps[i];
        }
    }
    // ... scales so that last element is 1.0
    for (int i=0; i<ps.Length; i++) { // Scales so that last element is 1.0
        ps[i] /= sum;
    }
}
```

# 10.9 Extension Methods (C# 3.0)
An extension method is a non-virtual instance method declared outside the type to which it belongs. An extension method must be declared in static class using this:

```csharp
static class CExtensions {
    access-modifier retype M(this C variable-name, formal-list)
    method-body
}
```
Note this keyword before the first parameter, whose type determines the class (or interface or delegate type) to which it belongs. The instance method syntax is to pretend that the extension method had been declared in type C like:

```csharp
access-modifier retype M(formal-list)
method-body
```
An extension method can access only public or internal members of the type on which it is defined. An extension method defined on a class or interface is very similar to a non-virtual instance method. However, in call s.M() to an extension method defined on a struct, the instance s will be copied when passed to M, whereas a real instance method defined in the struct would be called on itself. Unlike normal methods, the receiver o may be null. This is just syntactic sugar for the static method call CExtensions.M(o, ...).

The scope of an extension method is the nearest namespace in which it is defined and any scope that imports namespace via a using declaration.section 29.1.

When resolving a method call in namespace syntax o.M(), real instance methods are preferred over extension methods, extension methods available in inner namespace declarations are preferred over extension methods, methods declared directly in a namespace are preferred over extension methods imported by a using directive.

IEnumerable<T> from System.Collections.Generic has extension methods (section 28.5), declared in static class System.Linq.Enumerable. For those extension methods to be usable in a source file, it must contain the using declaration System.Linq.

There is no concept of "extension property" or "extension indexer".

# 10.10 Optional or Default-Value Method Parameters (C# 4.0)
In the formal-list of a method declaration (section 10.7), constructor declaration (section 10.11), or indexer declaration (section 10.16), a parameter may be optional by giving a default value for it:

```csharp
type parametername = constant
```

In calls, the argument corresponding to an optional parameter may be left out (section 12.17.7), which is convenient for rarely used arguments and can reduce the temptation to introduce a large number of overloads. The default value must be a compile-time constant. A ref parameter, an out parameter or a parameter array cannot have a default value. An optional parameter must follow all required parameters.


the `Shape` class defines the abstract notion of a geometrical shape object that can paint itself. The `Paint` method is abstract because there is no meaningful default implementation. The `Ellipse` and `Box` classes are concrete `Shape` implementations. Because these classes are non-abstract, they are required to override the `Paint` method and provide an actual implementation.

It is a compile-time error for a *base-access* (§7.6.8) to reference an abstract method. In the example

```csharp
abstract class A
{
    public abstract void F();
}

class B: A
{
    public override void F() {
        base.F();        // Error, base.F is abstract
    }
}
```

a compile-time error is reported for the `base.F()` invocation because it references an abstract method.

An abstract method declaration is permitted to override a virtual method. This allows an abstract class to force re-implementation of the method in derived classes, and makes the original implementation of the method unavailable. In the example

```csharp
using System;

class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }
}

abstract class B: A
{
    public abstract override void F();
}

class C: B
{
    public override void F() {
        Console.WriteLine("C.F");
    }
}
```

class A declares a virtual method, class B overrides this method with an abstract method, and class C overrides the abstract method to provide its own implementation.

## 10.6.7 External methods

When a method declaration includes an `extern` modifier, that method is said to be an *external method*. External methods are implemented externally, typically using a language other than C#. Because an external method declaration provides no actual implementation, the *method-body* of an external method simply consists of a semicolon. An external method may not be generic.

The `extern` modifier is typically used in conjunction with a `DllImport` attribute (§17.5.1), allowing external methods to be implemented by DLLs (Dynamic Link Libraries). The execution environment may support other mechanisms whereby implementations of external methods can be provided.

When an external method includes a `DllImport` attribute, the method declaration must also include a `static` modifier. This example demonstrates the use of the `extern` modifier and the `DllImport` attribute:

```csharp
using System.Text;
using System.Security.Permissions;
using System.Runtime.InteropServices;
class Path
{
    [DllImport("kernel32", SetLastError=true)]
    static extern bool CreateDirectory(string name, SecurityAttribute sa);
    [DllImport("kernel32", SetLastError=true)]
    static extern bool RemoveDirectory(string name);
    [DllImport("kernel32", SetLastError=true)]
    static extern int GetCurrentDirectory(int bufsize, StringBuilder buf);
    [DllImport("kernel32", SetLastError=true)]
    static extern bool SetCurrentDirectory(string name);
}
```

## 10.6.8 Partial methods

When a method declaration includes a partial modifier, that method is said to be a partial method. Partial methods can only be declared as members of partial types (§10.2), and are subject to a number of restrictions. Partial methods are further described in §10.2.7.

## 10.6.9 Extension methods

When the first parameter of a method includes the this modifier, that method is said to be an extension method. Extension methods can only be declared in non-generic, non-nested static classes. The first parameter of an extension method can have no modifiers other than this, and the parameter type cannot be a pointer type.

The following is an example of a static class that declares two extension methods:

```csharp
public static class Extensions
{
    public static int ToInt32(this string s) {
        return Int32.Parse(s);
    }
    public static T[] Slice<T>(this T[] source, int index, int count) {
        if (index < 0 || count < 0 || source.Length - index < count)
            throw new ArgumentException();
        T[] result = new T[count];
        Array.Copy(source, index, result, 0, count);
        return result;
    }
}
```

An extension method is a regular static method. In addition, where its enclosing static class is in scope, an extension method can be invoked using instance method invocation syntax (§7.6.5.2), using the receiver expression as the first argument.

The following program uses the extension methods declared above:

```csharp
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in strings.Slice(1, 2)) {
            Console.WriteLine(s.ToInt32());
        }
    }
}
```

The Slice method is available on the string[], and the ToInt32 method is available on string, because they have been declared as extension methods. The meaning of the program is the same as the following, using ordinary static method calls:

```csharp
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in Extensions.Slice(strings, 1, 2)) {
            Console.WriteLine(Extensions.ToInt32(s));
        }
    }
}
```

## 10.6.10 Method body

The *method-body* of a method declaration consists of either a *block* or a semicolon.

Abstract and external method declarations do not provide a method implementation, so their method bodies simply consist of a semicolon. For any other method, the method body is a block (§8.2) that contains the statements to execute when that method is invoked.

When the return type of a method is void, return statements (§8.9.4) in that method's body are not permitted to specify an expression. If execution of the method body of a void method completes normally (that is, control flows off the end of the method body), that method simply returns to its caller.

When the return type of a method is not void, each return statement in that method's body must specify an expression that is implicitly convertible to the return type. The endpoint of the method body of a value-returning method must not be reachable. In other words, in a value-returning method, control is not permitted to flow off the end of the method body.

In the example

```csharp
class A
{
    public int F() {}       // Error, return value required
    public int G() {
        return 1;
    }
    public int H(bool b) {
        if (b) {
            return 1;
        }
        else {
            return 0;
        }
    }
}
```

the value-returning F method results in a compile-time error because control can flow off the end of the method body. The G and H methods are correct because all possible execution paths end in a return statement that specifies a return value.

## 10.6.11 Method overloading

The method overload resolution rules are described in §7.5.2.

## 10.7 Properties

A *property* is a member that provides access to a characteristic of an object or a class. Examples of properties include the length of a string, the size of a font, the caption of a window, the name of a customer, and so on. Properties are a natural extension of fields—both are named members with associated types, and the syntax for

accessing fields and properties is the same. However, unlike fields, properties do not denote storage locations. Instead, properties have accessors that specify the statements to be executed when their values are read or written. Properties thus provide a mechanism for associating actions with the reading and writing of an object's attributes; furthermore, they permit such attributes to be computed.

Properties are declared using property-declarations:

```
property-declaration:
    attributesopt property-modifiersopt type member-name { accessor-declarations }
property-modifiers:
    property-modifier
    property-modifiers property-modifier
property-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern
member-name:
    identifier
    interface-type . identifier
```

A property-declaration may include a set of attributes (§17) and a valid combination of the four access modifiers (§10.3.5), the new (§10.3.4), static (§10.6.2), virtual (§10.6.3), override (§10.6.4), sealed (§10.6.5), abstract (§10.6.6), and extern (§10.6.7) modifiers.

Property declarations are subject to the same rules as method declarations (§10.6) with regard to valid combinations of modifiers.

The type of a property declaration specifies the type of the property introduced by the declaration, and the member-name specifies the name of the property. Unless the property is an explicit interface member implementation, the member-name is simply an identifier. For an explicit interface member implementation (§13.4.1), the member-name consists of an interface-type followed by a '.' and an identifier.

The type of a property must be at least as accessible as the property itself (§3.5.4). The accessor-declarations, which must be enclosed in '{' and '}' tokens, declare the accessors (§10.7.2) of the property. The accessors specify the executable statements associated with reading and writing the property. Even though the syntax for accessing a property is the same as that for a field, a property is not classified as a variable. Thus, it is not possible to pass a property as a ref or out argument. When a property declaration includes an extern modifier, the property is said to be an external property. Because an external property declaration provides no actual implementation, each of its accessor-declarations consists of a semicolon.

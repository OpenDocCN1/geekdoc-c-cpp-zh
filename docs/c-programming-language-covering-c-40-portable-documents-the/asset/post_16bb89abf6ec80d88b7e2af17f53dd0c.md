
> **JON SKEET** While I follow Eric's reasoning for the most part, this design permits an unfortunate situation to occur. If a derived class introduces a new overload of a base class method and overrides the base class method, then clearly that derived class is aware of the base class method—and yet that override is still not considered when selecting the method, until the algorithm reaches the base class. For example, consider the following methods in a derived class, with a base class declaring the obvious virtual method:

```
public void Foo(object x) { ... }
public override void Foo(int y) { ... }
```

A call to Foo(10) on an expression of the derived type will pick the first method—contrary to the expectations of every non-Microsoft developer I've ever presented this design to.

## 7.6.5.2 Extension Method Invocations

In a method invocation (§7.5.5.1) of one of the forms

- `expr . identifier ( )`
- `expr . identifier ( args )`
- `expr . identifier < typeargs > ( )`
- `expr . identifier < typeargs > ( args )`

if the normal processing of the invocation finds no applicable methods, an attempt is made to process the construct as an extension method invocation. If expr or any of the args has compile-time type dynamic, extension methods will not apply.

> **VLADIMIR RESHETNIKOV** The last rule does not apply to ref/out arguments of type dynamic.

The objective is to find the best type-name C, so that the corresponding static method invocation can take place:

- `C . identifier ( expr )`
- `C . identifier ( expr , args )`
- `C . identifier < typeargs > ( expr )`
- `C . identifier < typeargs > ( expr , args )`

An extension method C₁.M₁ is eligible if:

- C₁ is a nongeneric, non-nested class.
- The name of M₁ is identifier.
- M₁ is accessible and applicable when applied to the arguments as a static method as shown above.
- An implicit identity, reference, or boxing conversion exists from expr to the type of the first parameter of M₁.

> ERIC LIPPERT  This rule ensures that making a method that extends double does not also extend int. It also ensures that no extension methods are defined on anonymous functions or method groups.

The search for C proceeds as follows:

- Starting with the closest enclosing namespace declaration, continuing with each enclosing namespace declaration, and with the containing compilation unit, successive attempts are made to find a candidate set of extension methods:
- If the given namespace or compilation unit directly contains nongeneric type declarations C₁ with eligible extension methods M₁, then the set of those extension methods is the candidate set.
- If namespaces imported by using namespace directives in the given namespace or compilation unit directly contain nongeneric type declarations C₁ with eligible extension methods M₁, then the set of those extension methods is the candidate set.
- If no candidate set is found in any enclosing namespace declaration or compilation unit, a compile-time error occurs.
- Otherwise, overload resolution is applied to the candidate set as described in (§7.5.3). If no single best method is found, a compile-time error occurs.
- C is the type within which the best method is declared as an extension method.

Using C as a target, the method call is then processed as a static method invocation (§7.5.4).

> BILL WAGNER  This processing is somewhat complicated, and it reinforces the recommendation that you should not create duplicate extension methods in different namespaces.

> **PETER SESTOFT** It is tempting to think of an extension method as just a funny sort of nonvirtual instance method that is called only when no suitable ordinary instance method is available. Unfortunately, an extension method SetX(this S s) on a struct type S is not quite the same as an instance method on S, because the call s.SetX() will be transformed to the call SetX(s) that passes struct s by value, hence copying it. Any side effect will happen on the copy, not on the original struct s—yet another reason never to have mutable fields in struct types.

> **JON SKEET** One of the issues with extension methods is just how easy it is to accidentally import more than you expect or want. I would prefer this process to be more explicit, such as with a new type of using directive:

```csharp
using static System.Linq.Enumerable;
```

This would allow class libraries to expose extension methods without adding to IntelliSense confusion for users who didn't want to use them. Additionally, it would provide a note to code maintainers warning them that they should expect to see certain extension methods used within this compilation unit.

The preceding rules mean that instance methods take precedence over extension methods, that extension methods available in inner namespace declarations take precedence over extension methods available in outer namespace declarations, and that extension methods declared directly in a namespace take precedence over extension methods imported into that same namespace with a using namespace directive. For example:

```csharp
public static class E
{
    public static void F(this object obj, int i) { }
    public static void F(this object obj, string s) { }
}

class A { }

class B
{
    public void F(int i) { }
}

class C
{
    public void F(object obj) { }
}
```

```csharp
class X
{
    static void Test(A a, B b, C c) {
        a.F(1);        // E.F(object, int)
        a.F("hello");  // E.F(object, string)
        b.F(1);        // B.F(int)
        b.F("hello");  // E.F(object, string)
        c.F(1);        // C.F(object)
        c.F("hello");  // C.F(object)
    }
}
```

In the example, B’s method takes precedence over the first extension method, and C’s method takes precedence over both extension methods.

```csharp
public static class C
{
    public static void F(this int i) {
        Console.WriteLine("C.F({0})", i);
    }
    public static void G(this int i) {
        Console.WriteLine("C.G({0})", i);
    }
    public static void H(this int i) {
        Console.WriteLine("C.H({0})", i);
    }
}

namespace N1
{
    public static class D
    {
        public static void F(this int i) {
            Console.WriteLine("D.F({0})", i);
        }
        public static void G(this int i) {
            Console.WriteLine("D.G({0})", i);
        }
    }
}

namespace N2
{
    using N1;
    public static class E
    {
        public static void F(this int i) {
            Console.WriteLine("E.F({0})", i);
        }
    }
}
```

```csharp
class Test
{
    static void Main(string[] args)
    {
        1.F();
        2.G();
        3.H();
    }
}
```

The output of this example is

- E.F(1)
- D.G(2)
- C.H(3)

D.G takes precedence over C.G, and E.F takes precedence over both D.F and C.F.

> **JOSEPH ALBAHARI** One reason for instance methods having higher precedence than extension methods is to ensure that the introduction of extension methods into a program or framework doesn't break existing code.

> **ERIC LIPPERT** The way C# looks for extension methods gives rise to a variation on the “brittle derived class” problem mentioned earlier. If you rely on invocation processing to choose an extension method, but someone introduces an identically named instance method upon the class, then the extension method will no longer be called upon recompilation.

This behavior is not really a problem—it’s usually exactly what you want. The method on the class has far more information about the internal structure of the class than the static extension method does, so it should be given precedence.

The Microsoft C# compiler does not give a warning that an extension method exists that would be an alternative to the instance method chosen. If the compiler gave such a warning, there would be no easy way to “fix” the warning other than by putting a #pragma directive around it to turn the warning off.

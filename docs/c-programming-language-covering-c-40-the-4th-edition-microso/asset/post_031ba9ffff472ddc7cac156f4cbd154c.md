
> **PETER SESTOFT** It is tempting to think of an extension method as just a funny sort of nonvirtual instance method that is called only when no suitable ordinary instance method is available. Unfortunately, an extension method SetX(this S s) on a struct type S is not quite the same as an instance method on S, because the call s.SetX() will be transformed to the call SetX(s) that passes struct s by value, hence copying it. Any side effect will happen on the copy, not on the original struct s—yet another reason never to have mutable fields in struct types.

> **JON SKEET** One of the issues with extension methods is just how easy it is to accidentally import more than you expect or want. I would prefer this process to be more explicit, such as with a new type of using directive:
> 
> `using static System.Linq.Enumerable;`
> 
> This would allow class libraries to expose extension methods without adding to IntelliSense confusion for users who didn’t want to use them. Additionally, it would provide a note to code maintainers warning them that they should expect to see certain extension methods used within this compilation unit.

The preceding rules mean that instance methods take precedence over extension methods, that extension methods available in inner namespace declarations take precedence over extension methods available in outer namespace declarations, and that extension methods declared directly in a namespace take precedence over extension methods imported into that same namespace with a using namespace directive. For example:

```
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

```
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

```
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
```

```
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
```

```
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

```
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

E.F(1)
D.G(2)
C.H(3)

D.G takes precedence over C.G, and E.F takes precedence over both D.F and C.F.

> **JOSEPH ALBAHARI** One reason for instance methods having higher precedence than extension methods is to ensure that the introduction of extension methods into a program or framework doesn't break existing code.

> **ERIC LIPPERT** The way C# looks for extension methods gives rise to a variation on the “brittle derived class” problem mentioned earlier. If you rely on invocation processing to choose an extension method, but someone introduces an identically named instance method upon the class, then the extension method will no longer be called upon recompilation.
> 
> This behavior is not really a problem—it’s usually exactly what you want. The method on the class has far more information about the internal structure of the class than the static extension method does, so it should be given precedence.
> 
> The Microsoft C# compiler does not give a warning that an extension method exists that would be an alternative to the instance method chosen. If the compiler gave such a warning, there would be no easy way to “fix” the warning other than by putting a #pragma directive around it to turn the warning off.

> > JON SKEET I think in this case a warning would actually be the most appropriate course of action, so as to alert developers to the possibility that a method with the same name but a different meaning would now be called with no changes (beyond recompilation) of client code. In many cases—where the whole codebase relying on an extension method can be recompiled, so binary compatibility is not required—the method could be removed entirely or renamed. In other cases it could be converted into a non-extension method, allowing binary compatibility with old code. It feels wrong to completely ignore this change in the results of member lookup.

### 7.6.5.3 Delegate Invocations

For a delegate invocation, the *primary-expression* of the *invocation-expression* must be a value of a *delegate-type*. Furthermore, considering the *delegate-type* to be a function member with the same parameter list as the *delegate-type*, the *delegate-type* must be applicable (§7.5.3.1) with respect to the *argument-list* of the *invocation-expression*.

The runtime processing of a delegate invocation of the form D(A), where D is a *primary-expression* of a *delegate-type* and A is an optional *argument-list*, consists of the following steps:

- D is evaluated. If this evaluation causes an exception, no further steps are executed.
- The value of D is checked to be valid. If the value of D is null, a System.NullReferenceException is thrown and no further steps are executed.
- Otherwise, D is a reference to a delegate instance. Function member invocations (§7.5.4) are performed on each of the callable entities in the invocation list of the delegate. For callable entities consisting of an instance and instance method, the instance for the invocation is the instance contained in the callable entity.

### 7.6.6 Element Access

An *element-access* consists of a *primary-no-array-creation-expression*, followed by a “[” token, followed by an *argument-list*, followed by a “]” token. The *argument-list* consists of one or more *arguments*, separated by commas.

```
element-access:
    primary-no-array-creation-expression   [   argument-list   ]
```

The *argument-list* of an *element-access* is not allowed to contain ref or out arguments.

An element-access is dynamically bound (§7.2.2) if at least one of the following holds:

- The primary-no-array-creation-expression has compile-time type dynamic.
- At least one expression of the argument-list has compile-time type dynamic and the primary-no-array-creation-expression does not have an array type.

In this case the compiler classifies the element-access as a value of type dynamic. The rules below to determine the meaning of the element-access are then applied at runtime, using the runtime type instead of the compile-time type of those of the primary-no-array-creation-expression and argument-list expressions that have the compile-time type dynamic. If the primary-no-array-creation-expression does not have compile-time type dynamic, then the element access undergoes a limited compile time check as described in §7.5.4.

If the primary-no-array-creation-expression of an element-access is a value of an array-type, the element-access is an array access (§7.6.6.1). Otherwise, the primary-no-array-creation-expression must be a variable or value of a class, struct, or interface type that has one or more indexer members, in which case the element-access is an indexer access (§7.6.6.2).

## 7.6.6.1 Array Access

For an array access, the primary-no-array-creation-expression of the element-access must be a value of an array-type. Furthermore, the argument-list of an array access is not allowed to contain named arguments. The number of expressions in the argument-list must be the same as the rank of the array-type, and each expression must be of type int, uint, long, or ulong, or must be implicitly convertible to one or more of these types.

The result of evaluating an array access is a variable of the element type of the array—namely, the array element selected by the value(s) of the expression(s) in the argument-list.

> JON SKEET The fact that the result is a variable is important here: It means you can use array elements as ref or out arguments in method calls. In the face of array covariance, the actual type of the storage location is validated before the method is called.

The runtime processing of an array access of the form P[A], where P is a primary-no-array-creation-expression of an array-type and A is an argument-list, consists of the following steps:

- P is evaluated. If this evaluation causes an exception, no further steps are executed.
- The index expressions of the argument-list are evaluated in order, from left to right. Following evaluation of each index expression, an implicit conversion (§6.1) to one of the following types is performed: int, uint, long, ulong. The first type in this list for which

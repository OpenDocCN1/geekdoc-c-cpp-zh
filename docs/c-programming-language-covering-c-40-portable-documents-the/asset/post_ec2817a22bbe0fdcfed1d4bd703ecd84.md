
## 17.4.2 The Conditional Attribute

The attribute Conditional enables the definition of conditional methods and conditional attribute classes.

```
namespace System.Diagnostics
{
    [AttributeUsage(AttributeTargets.Method | AttributeTargets.Class,
        AllowMultiple = true)]
    public class ConditionalAttribute: Attribute
    {
        public ConditionalAttribute(string conditionString) {...}
        public string ConditionString { get {...} }
    }
}
```

### 17.4.2.1 Conditional Methods

A method decorated with the Conditional attribute is a conditional method. The Conditional attribute indicates a condition by testing a conditional compilation symbol. Calls to a conditional method are either included or omitted depending on whether this symbol is defined at the point of the call. If the symbol is defined, the call is included; otherwise, the call is omitted (including evaluation of the receiver and parameters of the call).

A conditional method is subject to the following restrictions:

- The conditional method must be a method in a class-declaration or struct-declaration. A compile-time error occurs if the Conditional attribute is specified on a method in an interface declaration.
- The conditional method must have a return type of void.
- The conditional method must not be marked with the override modifier. A conditional method may be marked with the virtual modifier, however. Overrides of such a method are implicitly conditional, and must not be explicitly marked with a Conditional attribute.
- The conditional method must not be an implementation of an interface method. Otherwise, a compile-time error occurs.

In addition, a compile-time error occurs if a conditional method is used in a delegate-creation-expression. The example

```
#define DEBUG
using System;
using System.Diagnostics;
class Class1
{ [Conditional("DEBUG")] public static void M() { Console.WriteLine("Executed Class1.M"); } }
class Class2 { public static void Test() { Class1.M(); } }
```

declares Class1.M as a conditional method. Class2's Test method calls this method. Since the conditional compilation symbol DEBUG is defined, if Class2.Test is called, it will call M. If the symbol DEBUG had not been defined, then Class2.Test would not call Class1.M.

It is important to note that the inclusion or exclusion of a call to a conditional method is controlled by the conditional compilation symbols at the point of the call. In the example

File class1.cs:

```
using System.Diagnostics; class Class1 { [Conditional("DEBUG")] public static void F() { Console.WriteLine("Executed Class1.F"); } }
```

File class2.cs:

```
#define DEBUG class Class2 { public static void G() { Class1.F(); // F is called } }
```

File class3.cs:

```
#undef DEBUG class Class3 { public static void H() { Class1.F(); // F is not called } }
```

the classes Class2 and Class3 each contain calls to the conditional method Class1.F, which is conditional based on whether DEBUG is defined. Since this symbol is defined in the context of Class2 but not Class3, the call to F in Class2 is included, while the call to F in Class3 is omitted.

The use of conditional methods in an inheritance chain can be confusing. Calls made to a conditional method through base, of the form base.M, are subject to the normal conditional method call rules. In the example

File class1.cs:

```
using System;
using System.Diagnostics;

class Class1
{
    [Conditional("DEBUG")]
    public virtual void M() {
        Console.WriteLine("Class1.M executed");
    }
}
```

File class2.cs:

```
using System;
class Class2: Class1
{
    public override void M() {
        Console.WriteLine("Class2.M executed");
        base.M();    // base.M is not called!
    }
}
```

File class3.cs:

```
#define DEBUG
using System;
class Class3
{
    public static void Test() {
        Class2 c = new Class2();
        c.M();    // M is called
    }
}
```

Class2 includes a call to the M defined in its base class. This call is omitted because the base method is conditional based on the presence of the symbol DEBUG, which is undefined. Thus the method writes to the console "Class2.M executed" only. Judicious use of pp-declarations can eliminate such problems.

### 17.4.2.2 Conditional Attribute Classes

An attribute class (§17.1) decorated with one or more Conditional attributes is a conditional attribute class. A conditional attribute class is thus associated with the conditional compilation symbols declared in its Conditional attributes. The example

```
using System;
using System.Diagnostics;
[Conditional("ALPHA")]
[Conditional("BETA")]
public class TestAttribute : Attribute {}
```

declares TestAttribute as a conditional attribute class associated with the conditional compilations symbols ALPHA and BETA.

Attribute specifications (§17.2) of a conditional attribute are included if one or more of its associated conditional compilation symbols are defined at the point of specification; otherwise, the attribute specification is omitted.

It is important to note that the inclusion or exclusion of an attribute specification of a conditional attribute class is controlled by the conditional compilation symbols at the point of the specification. In the example

File test.cs:

```
using System;
using System.Diagnostics;
[Conditional("DEBUG")]
public class TestAttribute : Attribute {}
```

File class1.cs:

```
#define DEBUG
[Test]
class Class1 {}    // TestAttribute is specified
```

File class2.cs:

```
#undef DEBUG
[Test]
class Class2 {}    // TestAttribute is not specified
```

the classes Class1 and Class2 are each decorated with attribute Test, which is conditional based on whether DEBUG is defined. Since this symbol is defined in the context of Class1 but not Class2, the specification of the Test attribute on Class1 is included, while the specification of the Test attribute on Class2 is omitted.

> ERIC LIPPERT The conditional attribute clearly has a strong connection to conditional compilation symbols—but it is important to remember that they are very different. A common error is to write something like this:
> 
> #if DEBUG
> int counter;
> #endif
> [Conditional("DEBUG")] void DoIt(int x) { ... }
> ...
> DoIt(this.counter);
> 
> The definition of the field counter is removed from the program entirely if the DEBUG symbol is not defined. How does the compiler know to remove the call to DoIt? Because DoIt(int) is conditional and DEBUG is not defined. But how does the compiler know that DoIt(int) is being called, as opposed to some other overload? Because this counter is declared as an int—oh, wait, that field definition has been removed. There is no such field, so compilation will fail in the non-debug build.

## 17.4.3 The Obsolete Attribute

The attribute Obsolete is used to mark types and members of types that should no longer be used.

```csharp
namespace System
{
    [AttributeUsage(
        AttributeTargets.Class |
        AttributeTargets.Struct |
        AttributeTargets.Enum |
        AttributeTargets.Interface |
        AttributeTargets.Delegate |
        AttributeTargets.Method |
        AttributeTargets.Constructor |
        AttributeTargets.Property |
        AttributeTargets.Field |
        AttributeTargets.Event,
        Inherited = false)
    ]
    public class ObsoleteAttribute : Attribute
    {
        public ObsoleteAttribute() {...}
        public ObsoleteAttribute(string message) {...}
        public ObsoleteAttribute(string message, bool error) {...}
        public string Message { get {...} }
        public bool IsError { get {...} }
    }
}
```

If a program uses a type or member that is decorated with the Obsolete attribute, the compiler issues a warning or an error. Specifically, the compiler issues a warning if no error parameter is provided, or if the error parameter is provided and has the value false. The compiler issues an error if the error parameter is specified and has the value true.

In the example

```
[Obsolete("This class is obsolete; use class B instead")]
class A
{
    public void F() { }
}
class B
{
    public void F() { }
}
class Test
{
    static void Main()
    {
        A a = new A();    // Warning
        a.F();
    }
}
```

the class A is decorated with the Obsolete attribute. Each use of A in Main results in a warning that includes the specified message, "This class is obsolete; use class B instead."

> JON SKEET There's an important lesson in this example: When you make something obsolete, always give guidance as to the new, preferred way of achieving a similar effect. Ideally, provide some indication (potentially in the documentation instead of the attribute message) of why the "old" code is being declared obsolete as well. It's extremely annoying when code that has worked for a long time suddenly starts spouting warnings with no good explanation.

> MAREK SAFAR The compiler does not automatically obsolete overrides of virtual methods. Therefore, when a virtual method is marked as Obsolete, every method that overrides it has to be manually decorated with the Obsolete attribute as well.

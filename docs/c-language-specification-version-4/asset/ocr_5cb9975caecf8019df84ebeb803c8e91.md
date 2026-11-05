+   - A static function member (method, property, event, operator, or constructor) does not operate on a specific instance, and it is a compile-time error to refer to this in such a function member.

When a field, method, property, event, indexer, constructor, or destructor declaration does not include a static modifier, it declares an instance member. (An instance member is sometimes called a non-static member.) Instance members have the following characteristics:

+   - When an instance member M is referenced in a member-access (§7.6.4) of the form E.M, E must denote an instance of a type containing M. It is a binding-time error for E to denote a type.
+   - Every instance of a class contains a separate set of all instance fields of the class.
+   - An instance function member (method, property, indexer, instance constructor, or destructor) operates on a given instance of the class, and this instance can be accessed as this (§7.6.7).

The following example illustrates the rules for accessing static and instance members:

```
class Test
{
    int x;
    static int y;
    void F() {
        x = 1;      // Ok, same as this.x = 1
        y = 1;      // Ok, same as Test.y = 1
    }
    static void G() {
        x = 1;      // Error, cannot access this.x
        y = 1;      // Ok, same as Test.y = 1
    }
    static void Main() {
        Test t = new Test();
        t.x = 1;    // Ok
        t.y = 1;    // Error, cannot access static member through instance
        Test.x = 1; // Error, cannot access instance member through type
        Test.y = 1; // Ok
    }
}
```

The F method shows that in an instance function member, a simple-name (§7.6.2) can be used to access both instance members and static members. The G method shows that in a static function member, it is a compile-time error to access an instance member through a simple-name. The Main method shows that in a member-access (§7.6.4), instance members must be accessed through instances, and static members must be accessed through types.

# 10.3.8 Nested types

A type declared within a class or struct declaration is called a nested type. A type that is declared within a compilation unit or namespace is called a non-nested type.

In the example

```
using System;
class A
{
    class B
    {
        static void F() {
            Console.WriteLine("A.B.F");
        }
    }
}
```

```
public IComparable<string> Prop { get {...} set {...} }
public int H(double d) {...}
```

The type of the member a in the generic class declaration Gen is “two-dimensional array of T”, so the type of the member a in the constructed type above is “two-dimensional array of single-dimensional array of int”, or int[,][].

*end example*

Within instance function members, the type of this is the instance type (§14.3.2) of the containing declaration.

All members of a generic class can use type parameters from any enclosing class, either directly or as part of a constructed type. When a particular closed constructed type (§8.4.3) is used at run-time, each use of a type parameter is replaced with the type argument supplied to the constructed type.

Example:

```
class C<V>
{
    public V f1;
    public C<V> f2 = null;

    public C(V x)
    {
        this.f1 = x;
        this.f2 = this;
    }
}

class Application
{
    static void Main()
    {
        C<int> x1 = new C<int>(1);          // Prints 1
        Console.WriteLine(x1.f1);

        C<double> x2 = new C<double>(3.1415);  // Prints 3.1415
        Console.WriteLine(x2.f1);
    }
}
```

*end example*

## 14.3.4 Inheritance

A class inherits the members of its direct base class. Inheritance means that a class implicitly contains all members of its direct base class, except for the instance constructors, finalizers, and static constructors of the base class. Some important aspects of inheritance are:

- Inheritance is transitive. If C is derived from B, and B is derived from A, then C inherits the members declared in B as well as the members declared in A.
- A derived class extends its direct base class. A derived class can add new members to those it inherits, but it cannot remove the definition of an inherited member.
- Instance constructors, finalizers, and static constructors are not inherited, but all other members are, regardless of their declared accessibility (§7.5). However, depending on their declared accessibility, inherited members might not be accessible in a derived class.
- A derived class can hide (§7.7.2.3) inherited members by declaring new members with the same name or signature. However, hiding an inherited member does not remove that member—it merely makes that member inaccessible directly through the derived class.
- An instance of a class contains a set of all instance fields declared in the class and its base classes, and an implicit conversion (§10.2.8) exists from a derived class type to any of its base class types. Thus, a reference to an instance of some derived class can be treated as a reference to an instance of any of its base classes.
- A class can declare virtual methods, properties, indexers, and events, and derived classes can override the implementation of these function members. This enables classes to exhibit polymorphic behavior wherein the actions performed by a function member invocation vary depending on the run-time type of the instance through which that function member is invoked.

The inherited members of a constructed class type are the members of the immediate base class type (§14.2.4.2), which is found by substituting the type arguments of the constructed type for each occurrence of the corresponding type parameters in the base_class_specification. These members, in turn, are transformed by substituting, for each type_parameter in the member declaration, the corresponding type_argument of the base_class_specification.

Example:

```
class B<U>
{
    public U F(long index) {...}
}
```

```
class D<T> : B<T[]>
{
    public T G(string s) {...}
}
```

In the code above, the constructed type D<int> has a non-inherited member public int G(string s) obtained by substituting the type argument int for the type parameter T. D<int> also has an inherited member from the class declaration B. This inherited member is determined by first determining the base class type B<int[]> of D<int> by substituting int for T in the base class specification B<T[]>. Then, as a type argument to B, int[] is substituted for U in public U F(long index), yielding the inherited member public int[] F(long index).
end example

## 14.3.5 The new modifier

A class_member_declaration is permitted to declare a member with the same name or signature as an inherited member. When this occurs, the derived class member is said to hide the base class member. See §7.7.2.3 for a precise specification of when a member hides an inherited member.

An inherited member M is considered to be available if M is accessible and there is no other inherited accessible member N that already hides M. Implicitly hiding an inherited member is not considered an error, but it does cause the compiler to issue a warning unless the declaration of the derived class member includes a new modifier to explicitly indicate that the derived member is intended to hide the
base member. If one or more parts of a partial declaration (§14.2.7) of a nested type include the new modifier, no warning is issued if the nested type hides an available inherited member.

If a new modifier is included in a declaration that doesn't hide an available inherited member, a warning to that effect is issued.

## 14.3.6 Access modifiers

A class_member_declaration can have any one of the five possible kinds of declared accessibility (§7.5.2): public, protected internal, protected, internal, or private. Except for the protected internal combination, it is a compile-time error to specify more than one access modifier. When a class_member_declaration does not include any access modifiers, private is assumed.

## 14.3.7 Constituent types

Types that are used in the declaration of a member are called the constituent types of that member. Possible constituent types are the type of a constant, field, property, event, or indexer, the return type of a method or operator, and the parameter types of a method, indexer, operator, or instance constructor. The constituent types of a member shall be at least as accessible as that member itself (§7.5.5).

## 14.3.8 Static and instance members

Members of a class are either static members or instance members.

Note: Generally speaking, it is useful to think of static members as belonging to classes and instance members as belonging to objects (instances of classes). end note

When a field, method, property, event, operator, or constructor declaration includes a static modifier, it declares a static member. In addition, a constant or type declaration implicitly declares a static member. Static members have the following characteristics:

- When a static member M is referenced in a member_access (§11.7.6) of the form E.M, E shall denote a type that has a member M. It is a compile-time error for E to denote an instance.
- A static field in a non-generic class identifies exactly one storage location. No matter how many instances of a non-generic class are created, there is only ever one copy of a static field. Each distinct closed constructed type (§8.4.3) has its own set of static fields, regardless of the number of instances of the closed constructed type.
- A static function member (method, property, event, operator, or constructor) does not operate on a specific instance, and it is a compile-time error to refer to this in such a function member.

When a field, method, property, event, indexer, constructor, or finalizer declaration does not include a static modifier, it declares an instance member. (An instance member is sometimes called a non-static member.) Instance members have the following characteristics:

- When an instance member M is referenced in a member_access (§11.7.6) of the form E.M, E shall denote an instance of a type that has a member M. It is a binding-time error for E to denote a type.
- Every instance of a class contains a separate set of all instance fields of the class.
- An instance function member (method, property, indexer, instance constructor, or finalizer) operates on a given instance of the class, and this instance can be accessed as this (§11.7.12).

Example: The following example illustrates the rules for accessing static and instance members:

```
class Test
{
```

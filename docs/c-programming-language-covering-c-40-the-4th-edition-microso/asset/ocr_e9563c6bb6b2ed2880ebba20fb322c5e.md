+   - Inheritance is transitive. If C is derived from B, and B is derived from A, then C inherits the members declared in B as well as the members declared in A.
+   - A derived class extends its direct base class. A derived class can add new members to those it inherits, but it cannot remove the definition of an inherited member.
+   - Instance constructors, destructors, and static constructors are not inherited, but all other members are, regardless of their declared accessibility (§3.5). However, depending on their declared accessibility, inherited members might not be accessible in a derived class.

> **JON SKEET** Occasionally, developers ask why instance constructors aren’t inherited. My view is that only the particular class knows which information it needs to create a valid instance. For example, if instance constructors were inherited, all classes would have to have a parameterless constructor (because object does). What would it mean to create a new FileStream without specifying a filename or handle?

+   - A derived class can hide (§3.7.1.2) inherited members by declaring new members with the same name or signature. Note, however, that hiding an inherited member does not remove that member—it merely makes that member inaccessible directly through the derived class.
+   - An instance of a class contains a set of all instance fields declared in the class and its base classes, and an implicit conversion (§6.1.6) exists from a derived class type to any of its base class types. Thus a reference to an instance of some derived class can be treated as a reference to an instance of any of its base classes.
+   - A class can declare virtual methods, properties, and indexers, and derived classes can override the implementation of these function members. This enables classes to exhibit polymorphic behavior wherein the actions performed by a function member invocation varies depending on the runtime type of the instance through which that function member is invoked.

The inherited members of a constructed class type are the members of the immediate base class type (§10.1.4.1), which is found by substituting the type arguments of the constructed type for each occurrence of the corresponding type parameters in the base-class-specification. These members, in turn, are transformed by substituting, for each type-parameter in the member declaration, the corresponding type-argument of the base-class-specification.

```
```csharp
class B<U>
{
    public U F(long index) {...}
}

class D<T>: B<T[]>
{
    public T G(string s) {...}
}
```
```
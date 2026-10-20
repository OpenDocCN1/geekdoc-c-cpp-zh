
```
if (Object.ReferenceEquals(left, null) ||
Object.ReferenceEquals(right, null))
return false;
return left.Equals(right);
```

This example code introduces a method I have not discussed yet: namely, the instance Equals() method. I’ll explain that in detail, but I’m not ready to end my discussion of the static Equals() just yet. For right now, I want you to understand that static Equals() uses the instance Equals() method of the left argument to determine whether two objects are equal.

As with ReferenceEquals(), you’ll never overload or redefine your own version of the static Object.Equals() method because it already does exactly what it needs to do: determines whether two objects are the same when you don’t know the runtime type. Because the static Equals() method delegates to the left argument’s instance Equals(), it uses the rules for that type.

Now you understand why you never need to redefine the static ReferenceEquals() and static Equals() methods. It’s time to discuss the methods you will override. But first, let’s briefly discuss the mathematical properties of an equality relation. You need to make sure that your definition and implementation are consistent with other programmers’ expectations. This means that you need to keep in mind the mathematical properties of equality: Equality is reflexive, symmetric, and transitive. The reflexive property means that any object is equal to itself. No matter what type is involved, a == a is always true. The symmetric property means that order does not matter: If a == b is true, b == a is also true. If a == b is false, b == a is also false. The last property is that if a == b and b == c are both true, then a == c must also be true. That’s the transitive property.

Now it’s time to discuss the instance Object.Equals() function, including when and how you override it. You create your own instance version of Equals() when the default behavior is inconsistent with your type. The Object.Equals() method uses object identity to determine whether two variables are equal. The default Object.Equals() function behaves exactly the same as Object.ReferenceEquals(). But wait—value types are different. System.ValueType does override Object.Equals(). Remember that ValueType is the base class for all value types that you create (using the struct keyword). Two variables of a value type are equal if they are the same type and they have the same contents. ValueType.Equals() implements that behavior. Unfortunately, ValueType.Equals() does not have an efficient

implementation. ValueType.Equals() is the base class for all value types. To provide the correct behavior, it must compare all the member variables in any derived type, without knowing the runtime type of the object. In C#, that means using reflection. As you’ll see in Item 43, there are many disadvantages to reflection, especially when performance is a goal. Equality is one of those fundamental constructs that gets called frequently in programs, so performance is a worthy goal. Under almost all circumstances, you can write a much faster override of Equals() for any value type. The recommendation for value types is simple: Always create an override of ValueType.Equals() whenever you create a value type.

You should override the instance Equals() function only when you want to change the defined semantics for a reference type. A number of classes in the .NET Framework Class Library use value semantics instead of reference semantics for equality. Two string objects are equal if they contain the same contents. Two DataRowView objects are equal if they refer to the same DataRow. The point is that if your type should follow value semantics (comparing contents) instead of reference semantics (comparing object identity), you should write your own override of instance Object.Equals().

Now that you know when to write your own override of Object.Equals(), you must understand how you should implement it. The equality relationship for value types has many implications for boxing and is discussed in Item 45. For reference types, your instance method needs to follow predefined behavior to avoid strange surprises for users of your class. Whenever you override Equals(), you’ll want to implement IEquatable<T> for that type. I’ll explain why a little further into this item. Here is the standard pattern for overriding System.Object.Equals. The highlight shows the changes to implement IEquatable<T>.

```
public class Foo : IEquatable<Foo>
{
    public override bool Equals(object right)
    {
        // check null:
        // this pointer is never null in C# methods.
        if (object.ReferenceEquals(right, null))
            return false;

        if (object.ReferenceEquals(this, right))
            return true;

        // Discussed below.
        if (this.GetType() != right.GetType())
            return false;

        // Compare this type's contents here:
        return this.Equals(right as Foo);
    }

    #region IEquatable<Foo> Members
    public bool Equals(Foo other)
    {
        // elided.
        return true;
    }
    #endregion
}
```

First, Equals() should never throw exceptions—it doesn’t make much sense. Two variables are or are not equal; there’s not much room for other failures. Just return false for all failure conditions, such as null references or the wrong argument types. Now, let’s go through this method in detail so you understand why each check is there and why some checks can be left out. The first check determines whether the right-side object is null. There is no check on this reference. In C#, this is never null. The CLR throws an exception before calling any instance method through a null reference. The next check determines whether the two object references are the same, testing object identity. It’s a very efficient test, and equal object identity guarantees equal contents.

The next check determines whether the two objects being compared are the same type. The exact form is important. First, notice that it does not assume that this is of type Foo; it calls this.GetType(). The actual type might be a class derived from Foo. Second, the code checks the exact type of objects being compared. It is not enough to ensure that you can convert the right-side parameter to the current type. That test can cause two subtle bugs. Consider the following example involving a small inheritance hierarchy:

```
public class B : IEquatable<B>
{
    public override bool Equals(object right)
    {
        // check null:
```
```csharp
if (object.ReferenceEquals(right, null))
    return false;

// Check reference equality:
if (object.ReferenceEquals(this, right))
    return true;

// Problems here, discussed below.
B rightAsB = right as B;
if (rightAsB == null)
    return false;

return this.Equals(rightAsB);
}

#region IEquatable<B> Members

public bool Equals(B other)
{
    // elided
    return true;
}

#endregion
}

public class D : B, IEquatable<D>
{
    // etc.
    public override bool Equals(object right)
    {
        // check null:
        if (object.ReferenceEquals(right, null))
            return false;

        if (object.ReferenceEquals(this, right))
            return true;

        // Problems here.
        D rightAsD = right as D;
```

```
if (rightAsD == null)
    return false;

if (base.Equals(rightAsD) == false)
    return false;

return this.Equals(rightAsD);
}

#region IEquatable<D> Members
public bool Equals(D other)
{
    // elided.
    return true; // or false, based on test
}
#endregion
}

//Test:
B baseObject = new B();
D derivedObject = new D();

// Comparison 1.
if (baseObject.Equals(derivedObject))
    Console.WriteLine("Equals");
else
    Console.WriteLine("Not Equal");

// Comparison 2.
if (derivedObject.Equals(baseObject))
    Console.WriteLine("Equals");
else
    Console.WriteLine("Not Equal");
```

Under any possible circumstances, you would expect to see either Equals or Not Equal printed twice. Because of some errors, this is not the case with the previous code. The second comparison will never return true. The base object, of type B, can never be converted into a D. However, the first comparison might evaluate to true. The derived object, of type D, can be implicitly converted to a type B. If the B members of the right-side argu-


Eventually, people consume the information in your types. People understand text output, so you want to provide it in the simplest fashion possible: Override ToString() in all your types. Make the ToString() output short and reasonable.

## Item 6: Understand the Relationships Among the Many Different Concepts of Equality

When you create your own types (either classes or structs), you define what equality means for that type. C# provides four different functions that determine whether two different objects are “equal”:

```
public static bool ReferenceEquals
    (object left, object right);
public static bool Equals
    (object left, object right);
public virtual bool Equals(object right);
public static bool operator ==(MyClass left, MyClass right);
```

The language enables you to create your own versions of all four of these methods. But just because you can doesn’t mean that you should. You should never redefine the first two static functions. You’ll often create your own instance Equals() method to define the semantics of your own type, and you’ll occasionally override operator==(), typically for performance reasons in value types. Furthermore, there are relationships among these four functions, so when you change one, you can affect the behavior of the others. Yes, needing four functions to test equality is complicated. But don’t worry—you can simplify it.

Of course, those four methods are not the only options for equality. Types that override Equals() should implement IEquatable<T>. Types that implement value semantics should implement the IStructuralEquality interface. That means six different ways to express equality.

Like so many of the complicated elements in C#, this one follows from the fact that C# enables you to create both value types and reference types. Two variables of a reference type are equal if they refer to the same object, referred to as object identity. Two variables of a value type are equal if they are the same type and they contain the same contents. That’s why equality tests need so many different methods.

Let's start with the two functions you should never change. Object.ReferenceEquals() returns true if two variables refer to the same object—that is, the two variables have the same object identity. Whether the types being compared are reference types or value types, this method always tests object identity, not object contents. Yes, that means that ReferenceEquals() always returns false when you use it to test equality of value types. Even when you compare a value type to itself, ReferenceEquals() returns false. This is due to boxing, which is covered in Item 45.

```
int i = 5;
int j = 5;
if (Object.ReferenceEquals(i, j))
    Console.WriteLine("Never happens.");
else
    Console.WriteLine("Always happens.");

if (Object.ReferenceEquals(i, i))
    Console.WriteLine("Never happens.");
else
    Console.WriteLine("Always happens.");
```

You'll never redefine Object.ReferenceEquals() because it does exactly what it is supposed to do: tests the object identity of two different variables.

The second function you'll never redefine is static Object.Equals(). This method tests whether two variables are equal when you don't know the runtime type of the two arguments. Remember that System.Object is the ultimate base class for everything in C#. Anytime you compare two variables, they are instances of System.Object. Value types and reference types are instances of System.Object. So how does this method test the equality of two variables, without knowing their type, when equality changes its meaning depending on the type? The answer is simple: This method delegates that responsibility to one of the types in question. The static Object.Equals() method is implemented something like this:

```
public static new bool Equals(object left, object right)
{
    // Check object identity
    if (Object.ReferenceEquals(left, right) )
        return true;
    // both null references handled above
    if (Object.ReferenceEquals(left, null) ||
        Object.ReferenceEquals(right, null))
        return false;

    return left.Equals(right);
}
```

This example code introduces a method I have not discussed yet: namely, the instance Equals() method. I'll explain that in detail, but I'm not ready to end my discussion of the static Equals() just yet. For right now, I want you to understand that static Equals() uses the instance Equals() method of the left argument to determine whether two objects are equal.

As with ReferenceEquals(), you'll never overload or redefine your own version of the static Object.Equals() method because it already does exactly what it needs to do: determines whether two objects are the same when you don't know the runtime type. Because the static Equals() method delegates to the left argument's instance Equals(), it uses the rules for that type.

Now you understand why you never need to redefine the static ReferenceEquals() and static Equals() methods. It's time to discuss the methods you will override. But first, let's briefly discuss the mathematical properties of an equality relation. You need to make sure that your definition and implementation are consistent with other programmers' expectations. This means that you need to keep in mind the mathematical properties of equality: Equality is reflexive, symmetric, and transitive. The reflexive property means that any object is equal to itself. No matter what type is involved, a == a is always true. The symmetric property means that order does not matter: If a == b is true, b == a is also true. If a == b is false, b == a is also false. The last property is that if a == b and b == c are both true, then a == c must also be true. That's the transitive property.

Now it's time to discuss the instance Object.Equals() function, including when and how you override it. You create your own instance version of Equals() when the default behavior is inconsistent with your type. The Object.Equals() method uses object identity to determine whether two variables are equal. The default Object.Equals() function behaves exactly the same as Object.ReferenceEquals(). But wait—value types are different. System.ValueType does override Object.Equals(). Remember that ValueType is the base class for all value types that you create (using the struct keyword). Two variables of a value type are equal if they are the same type and they have the same contents. ValueType.Equals() implements that behavior. Unfortunately, ValueType.Equals() does not have an efficient implementation. ValueType.Equals() is the base class for all value types. To provide the correct behavior, it must compare all the member variables in any derived type, without knowing the runtime type of the object. In C#, that means using reflection. As you'll see in Item 43, there are many disadvantages to reflection, especially when performance is a goal. Equality is one of those fundamental constructs that gets called frequently in programs, so performance is a worthy goal. Under almost all circumstances, you can write a much faster override of Equals() for any value type. The recommendation for value types is simple: Always create an override of ValueType.Equals() whenever you create a value type.

You should override the instance Equals() function only when you want to change the defined semantics for a reference type. A number of classes in the .NET Framework Class Library use value semantics instead of reference semantics for equality. Two string objects are equal if they contain the same contents. Two DataRowView objects are equal if they refer to the same DataRow. The point is that if your type should follow value semantics (comparing contents) instead of reference semantics (comparing object identity), you should write your own override of instance Object.Equals().

Now that you know when to write your own override of Object.Equals(), you must understand how you should implement it. The equality relationship for value types has many implications for boxing and is discussed in Item 45. For reference types, your instance method needs to follow pre-defined behavior to avoid strange surprises for users of your class. Whenever you override Equals(), you'll want to implement IEquatable<T> for that type. I'll explain why a little further into this item. Here is the standard pattern for overriding System.Object.Equals. The highlight shows the changes to implement IEquatable<T>.

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
    }
}
```

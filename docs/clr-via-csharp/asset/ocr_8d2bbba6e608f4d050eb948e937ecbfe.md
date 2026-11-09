A number of developers reviewed the chapters of this book. After reading through some of my code samples (such as the preceding one), these reviewers would tell me that they’ve sworn off value types. I must say that these little value type nuances have cost me days of debugging time, which is why I spend time pointing them out in this book. I hope you’ll remember some of these nuances and that you’ll be prepared for them if and when they strike you and your code. Certainly, you shouldn’t be scared of value types. They are useful, and they have their place. After all, a program needs a little **Int32** love now and then. Just keep in mind that value types and reference types have very different behaviors depending on how they’re used. In fact, you should take the preceding code and declare the **Point** as a **class** instead of a **struct** to appreciate the different behavior that results. Finally, you’ll be very happy to know that the core value types that ship in the **FCL—Byte, Int32, UInt32, Int64, UInt64, Single, Double, Decimal, BigInteger, Complex**, all **enums**, and so on—are all immutable, so you should experience no surprising behavior when using any of these types.

# ## Object Equality and Identity

Frequently, developers write code to compare objects with one another. This is particularly true when placing objects in a collection and you’re writing code to sort, search, or compare items in a collection. In this section, I’ll discuss object equality and identity, and I’ll also discuss how to define a type that properly implements object equality.

The **System.Object** type offers a virtual method named **Equals**, whose purpose is to return **true** if two objects contain the same value. The implementation of **Object**’s **Equals** method looks like this:

```
public class Object {
    public virtual Boolean Equals(Object obj) {

        // If both references point to the same object,
        // they must have the same value.
        if (this == obj) return true;

        // Assume that the objects do not have the same value.
        return false;
    }
}
```

At first, this seems like a reasonable default implementation of **Equals**: it returns **true** if the **this** and **obj** arguments refer to the same exact object. This seems reasonable because **Equals** knows that an object must have the same value as itself. However, if the arguments refer to different objects, **Equals** can’t be certain if the objects contain the same values, and therefore, **false** is returned. In other words, the default implementation of **Object**’s **Equals** method really implements identity, not value equality.

Unfortunately, as it turns out, **Object**’s **Equals** method is not a reasonable default, and it should have never been implemented this way. You immediately see the problem when you

copies the fields in the boxed Point to a temporary Point on the thread's stack! The m_x and m_y fields of this temporary point are changed to 3 and 3, but the boxed Point isn't affected by this call to Change. When WriteLine is called the fourth time, (2, 2) is displayed again. Many developers do not expect this.

Some languages, such as C++/CLI, let you change the fields in a boxed value type, but C# does not. However, you can fool C# into allowing this by using an interface. The following code is a modified version of the previous code.

```csharp
using System;

// Interface defining a Change method
internal interface IChangeBoxedPoint {
    void Change(Int32 x, Int32 y);
}


// Point is a value type.
internal struct Point : IChangeBoxedPoint {
    private Int32 m_x, m_y;

    public Point(Int32 x, Int32 y) {
        m_x = x;
        m_y = y;
    }

    public void Change(Int32 x, Int32 y) {
        m_x = x; m_y = y;
    }

    public override String ToString() {
        return String.Format("({0}, {1})", m_x.ToString(), m_y.ToString());
    }
}

public sealed class Program {
    public static void Main() {
        Point p = new Point(1, 1);

        Console.WriteLine(p);

        p.Change(2, 2);
        Console.WriteLine(p);

        Object o = p;
        Console.WriteLine(o);

        ((Point) o).Change(3, 3);
        Console.WriteLine(o);

        // Boxes p, changes the boxed object and discards it
        ((IChangeBoxedPoint) p).Change(4, 4);
        Console.WriteLine(p);

        // Changes the boxed object and shows it
        ((IChangeBoxedPoint) o).Change(5, 5);
        Console.WriteLine(o);
    }
}
```

This code is almost identical to the previous version. The main difference is that the Change method is defined by the IChangeBoxedPoint interface, and the Point type now implements this interface. Inside Main, the first four calls to WriteLine are the same and produce the same results I had before (as expected). However, I’ve added two more examples at the end of Main.

In the first example, the unboxed Point, p, is cast to an IChangeBoxedPoint. This cast causes the value in p to be boxed. Change is called on the boxed value, which does change its m_x and m_y fields to 4 and 4, but after Change returns, the boxed object is immediately ready to be garbage collected. So the fifth call to WriteLine displays (2, 2). Many developers won’t expect this result.

In the last example, the boxed Point referred to by o is cast to an IChangeBoxedPoint. No boxing is necessary here because o is already a boxed Point. Then Change is called, which does change the boxed Point’s m_x and m_y fields. The interface method Change has allowed me to change the fields in a boxed Point object! Now, when WriteLine is called, it displays (5, 5) as expected. The purpose of this whole example is to demonstrate how an interface method is able to modify the fields of a boxed value type. In C#, this isn’t possible without using an interface method.

![](img/857bdf6cef9e242b53a37f88df9a1287_163_0.png)

> **Important** Earlier in this chapter, I mentioned that value types should be immutable: that is, they should not define any members that modify any of the type’s instance fields. In fact, I recommended that value types have their fields marked as readonly so that the compiler will issue errors should you accidentally write a method that attempts to modify a field. The previous example should make it very clear to you why value types should be immutable. The unexpected behaviors shown in the previous example all occur when attempting to call a method that modifies the value type’s instance fields. If after constructing a value type, you do not call any methods that modify its state, you will not get confused when all of the boxing and unboxing/field copying occurs. If the value type is immutable, you will end up just copying the same state around, and you will not be surprised by any of the behaviors you see.
>
> A number of developers reviewed the chapters of this book. After reading through some of my code samples (such as the preceding one), these reviewers would tell me that they’ve sworn off value types. I must say that these little value type nuances have cost me days of debugging time, which is why I spend time pointing them out in this book. I hope you’ll remember some of these nuances and that you’ll be prepared for them if and when they strike you and your code. Certainly, you shouldn’t be scared of value types. They are useful, and they have their place. After all, a program needs a little Int32 love now and then. Just keep in mind that value types and reference types have very different behaviors depending on how they’re used. In fact, you should take the preceding code and declare

- 3. If the `this` and `obj` arguments refer to objects of different types, return `false`. Obviously, checking if a `String` object is equal to a `FileStream` object should result in a `false` result.
- 4. For each instance field defined by the type, compare the value in the `this` object with the value in the `obj` object. If any fields are not equal, return `false`.
- 5. Call the base class's `Equals` method so it can compare any fields defined by it. If the base class's `Equals` method returns `false`, return `false`; otherwise, return `true`.

So Microsoft should have implemented `Object`'s `Equals` like this.

```csharp
public class Object {
   public virtual Boolean Equals(Object obj) {
      // The given object to compare to can't be null
      if (obj == null) return false;

      // If objects are different types, they can't be equal.
      if (this.GetType() != obj.GetType()) return false;

      // If objects are same type, return true if all of their fields match
      // Because System.Object defines no fields, the fields match
      return true;
   }
}
```

But, because Microsoft didn't implement `Equals` this way, the rules for how to implement `Equals` are significantly more complicated than you would think. When a type overrides `Equals`, the override should call its base class's implementation of `Equals` unless it would be calling `Object`'s implementation. This also means that because a type can override `Object`'s `Equals` method, this `Equals` method can no longer be called to test for identity. To fix this, `Object` offers a static `ReferenceEquals` method, which is implemented like this.

```csharp
public class Object {
   public static Boolean ReferenceEquals(Object objA, Object objB) {
      return (objA == objB);
   }
}
```

You should always call `ReferenceEquals` if you want to check for identity (if two references point to the same object). You shouldn't use the C# `==` operator (unless you cast both operands to `Object` first) because one of the operands' types could overload the `==` operator, giving it semantics other than identity.

As you can see, the .NET Framework has a very confusing story when it comes to object equality and identity. By the way, `System.ValueType` (the base class of all value types) does override `Object`'s `Equals` method and is correctly implemented to perform a value equality check (not an identity check). Internally, `ValueType`'s `Equals` is implemented this way:

- 1. If the `obj` argument is `null`, return `false`.
- 2. If the `this` and `obj` arguments refer to objects of different types, return `false`.
- 3. For each instance field defined by the type, compare the value in the `this` object with the value in the `obj` object by calling the field's `Equals` method. If any fields are not equal, return `false`.
- 4. Return `true`. `Object`'s `Equals` method is not called by `ValueType`'s `Equals` method.

Internally, `ValueType`'s `Equals` method uses reflection (covered in Chapter 23, "Assembly Loading and Reflection") to accomplish step 3. Because the CLR's reflection mechanism is slow, when defining your own value type, you should override `Equals` and provide your own implementation to improve the performance of value equality comparisons that use instances of your type. Of course, in your own implementation, do not call `base.Equals`.

When defining your own type, if you decide to override `Equals`, you must ensure that it adheres to the four properties of equality:

- **`Equals` must be reflexive**; that is, `x.Equals(x)` must return `true`.
- **`Equals` must be symmetric**; that is, `x.Equals(y)` must return the same value as `y.Equals(x)`.
- **`Equals` must be transitive**; that is, if `x.Equals(y)` returns `true` and `y.Equals(z)` returns `true`, then `x.Equals(z)` must also return `true`.
- **`Equals` must be consistent**. Provided that there are no changes in the two values being compared, `Equals` should consistently return `true` or `false`.

If your implementation of `Equals` fails to adhere to all of these rules, your application will behave in strange and unpredictable ways.

When overriding the `Equals` method, there are a couple more things that you'll probably want to do:

- **Have the type implement the `System.IEquatable<T>` interface's `Equals` method** This generic interface allows you to define a type-safe `Equals` method. Usually, you'll implement the `Equals` method that takes an `Object` parameter to internally call the type-safe `Equals` method.
- **Overload the `==` and `!=` operator methods** Usually, you'll implement these operator methods to internally call the type-safe `Equals` method.

Furthermore, if you think that instances of your type will be compared for the purposes of sorting, you'll want your type to also implement `System.IComparable`'s `CompareTo` method and `System.IComparable<T>`'s type-safe `CompareTo` method. If you implement these methods, you'll also want to overload the various comparison operator methods (`<`, `<=`, `>`, `>=`) and implement these methods internally to call the type-safe `CompareTo` method.


```csharp
#if INEFFICIENT
                // When compiling the following line, v is boxed
                // three times, wasting time and memory.
                Console.WriteLine("{0}, {1}, {2}", v, v, v);
#else
                // The lines below have the same result, execute
                // much faster, and use less memory.
                Object o = v; // Manually box v (just once).

                // No boxing occurs to compile the following line.
                Console.WriteLine("{0}, {1}, {2}", o, o, o);
#endif
            }
        }
```

If the code is compiled with the INEFFICIENT symbol defined, the compiler will generate code to box v three times, causing three objects to be allocated from the heap! This is extremely wasteful since each object will have exactly the same contents: 5. If the code is compiled without the INEFFICIENT symbol defined, v is boxed just once, so only one object is allocated from the heap. Then, in the call to Console.WriteLine, the reference to the single boxed object is passed three times. This second version executes much faster and allocates less memory from the heap.

In these examples, it’s fairly easy to recognize when an instance of a value type requires boxing. Basically, if you want a reference to an instance of a value type, the instance must be boxed. Usually this happens because you have a value type instance and you want to pass it to a method that requires a reference type. However, this situation isn’t the only one in which you’ll need to box an instance of a value type.

Recall that unboxed value types are lighter-weight types than reference types for two reasons:

- They are not allocated on the managed heap.
- They don’t have the additional overhead members that every object on the heap has: a type object pointer and a sync block index.

Because unboxed value types don’t have a sync block index, you can’t have multiple threads synchronize their access to the instance by using the methods of the System.Threading.Monitor type (or by using C#’s lock statement).

Even though unboxed value types don’t have a type object pointer, you can still call virtual methods (such as Equals, GetHashCode, or ToString) inherited or overridden by the type. If your value type overrides one of the virtual methods, then the CLR can invoke the method nonvirtually because value types are implicitly sealed and cannot have any types derived from them. In addition, the value type instance being used to invoke the virtual method is not boxed. However, if your override of the virtual method calls into the base type's implementation of the method, then the value type instance does get boxed when calling the base type's implementation so that a reference to a heap object gets passed to the `this` pointer in the base method.

However, calling a nonvirtual inherited method (such as GetType or MemberwiseClone) always requires the value type to be boxed because these methods are defined by `System.Object`, so the methods expect the `this` argument to be a pointer that refers to an object on the heap.

In addition, casting an unboxed instance of a value type to one of the type’s interfaces requires the instance to be boxed, because interface variables must always contain a reference to an object on the heap. (I’ll talk about interfaces in Chapter 13, “Interfaces.”) The following code demonstrates:

```csharp
using System;

internal struct Point : IComparable {
    private readonly Int32 m_x, m_y;

    // Constructor to easily initialize the fields
    public Point(Int32 x, Int32 y) {
        m_x = x;
        m_y = y;
    }

    // Override ToString method inherited from System.ValueType
    public override String ToString() {
        // Return the point as a string. Note: calling ToString prevents boxing
        return String.Format("({0}, {1})", m_x.ToString(), m_y.ToString());
    }

    // Implementation of type-safe CompareTo method
    public Int32 CompareTo(Point other) {
        // Use the Pythagorean Theorem to calculate
        // which point is farther from the origin (0, 0)
        return Math.Sign(Math.Sqrt(m_x * m_x + m_y * m_y)
            - Math.Sqrt(other.m_x * other.m_x + other.m_y * other.m_y));
    }

    // Implementation of IComparable’s CompareTo method
    public Int32 CompareTo(Object o) {
        if (GetType() != o.GetType())
            throw new ArgumentException("o is not a Point");
        // Call type-safe CompareTo method
        return CompareTo((Point)o);
    }
}
```

```csharp
public static class Program {
    public static void Main() {
        // Create two Point instances on the stack.
        Point p1 = new Point(10, 10);
        Point p2 = new Point(20, 20);

        // p1 does NOT get boxed to call ToString (a virtual method).
        Console.WriteLine(p1.ToString()); // "(10, 10)"

        // p1 DOES get boxed to call GetType (a non-virtual method).
        Console.WriteLine(p1.GetType()); // "Point"

        // p1 does NOT get boxed to call CompareTo.
        // p2 does NOT get boxed because CompareTo(Point) is called.
        Console.WriteLine(p1.CompareTo(p2)); // "-1"

        // p1 DOES get boxed, and the reference is placed in c.
        IComparable c = p1;
        Console.WriteLine(c.GetType()); // "Point"

        // p1 does NOT get boxed to call CompareTo.
        // Since CompareTo is not being passed a Point variable,
        // CompareTo(Object) is called which requires a reference to
        // a boxed Point.
        // c does NOT get boxed because it already refers to a boxed Point.
        Console.WriteLine(p1.CompareTo(c)); // "0"

        // c does NOT get boxed because it already refers to a boxed Point.
        // p2 does get boxed because CompareTo(Object) is called.
        Console.WriteLine(c.CompareTo(p2)); // "-1"

        // c is unboxed, and fields are copied into p2.
        p2 = (Point) c;

        // Proves that the fields got copied into p2.
        Console.WriteLine(p2.ToString()); // "(10, 10)"
    }
}
```

This code demonstrates several scenarios related to boxing and unboxing:

- **Calling ToString** In the call to ToString, p1 doesn't have to be boxed. At first, you'd think that p1 would have to be boxed because ToString is a virtual method that is inherited from the base type, System.ValueType. Normally, to call a virtual method, the CLR needs to determine the object's type in order to locate the type's method table. Since p1 is an unboxed value type, there's no type object pointer. However, the just-in-time (JIT) compiler sees that Point overrides the ToString method, and it emits code that calls ToString directly (nonvirtually) without having to do any boxing. The compiler knows that polymorphism can't come into play here since Point is a value type, and no type can derive from it to provide another implementation of this virtual method. Note that if Point's ToString method internally calls base.ToString(), then the value type instance would be boxed when calling System.ValueType's ToString method.

- **Calling GetType** In the call to the nonvirtual GetType method, p1 does have to be boxed. The reason is that the Point type inherits GetType from System.Object. So to call GetType, the CLR must use a pointer to a type object, which can be obtained only by boxing p1.

- **Calling CompareTo (first time)** In the first call to CompareTo, p1 doesn't have to be boxed because Point implements the CompareTo method, and the compiler can just call it directly. Note that a Point variable (p2) is being passed to CompareTo, and therefore the compiler calls the overload of CompareTo that accepts a Point parameter. This means that p2 will be passed by value to CompareTo and no boxing is necessary.

- **Casting to IComparable** When casting p1 to a variable (c) that is of an interface type, p1 must be boxed because interfaces are reference types by definition. So p1 is boxed, and the pointer to this boxed object is stored in the variable c. The following call to GetType proves that c does refer to a boxed Point on the heap.

- **Calling CompareTo (second time)** In the second call to CompareTo, p1 doesn’t have to be boxed because Point implements the CompareTo method, and the compiler can just call it directly. Note that an IComparable variable (c) is being passed to CompareTo, and therefore, the compiler calls the overload of CompareTo that accepts an Object parameter. This means that the argument passed must be a pointer that refers to an object on the heap. Fortunately, c does refer to a boxed Point, and therefore, that memory address in c can be passed to CompareTo, and no additional boxing is necessary.

- **Calling CompareTo (third time)** In the third call to CompareTo, c already refers to a boxed Point object on the heap. Since c is of the IComparable interface type, you can only call the interface’s CompareTo method that requires an Object parameter. This means that the argument passed must be a pointer that refers to an object on the heap. So p2 is boxed, and the pointer to this boxed object is passed to CompareTo.

- **Casting to Point** When casting c to a Point, the object on the heap referred to by c is unboxed, and its fields are copied from the heap to p2, an instance of the Point type residing on the stack.

I realize that all of this information about reference types, value types, and boxing might be overwhelming at first. However, a solid understanding of these concepts is critical to any .NET Framework developer’s long-term success. Trust me: having a solid grasp of these concepts will allow you to build efficient applications faster and easier.

## Changing Fields in a Boxed Value Type by Using Interfaces (and Why You Shouldn’t Do This)

Let’s have some fun and see how well you understand value types, boxing, and unboxing. Examine the following code, and see whether you can figure out what it displays on the console:

```csharp
using System;

// Point is a value type.
internal struct Point {
    private Int32 m_x, m_y;

    public Point(Int32 x, Int32 y) {
        m_x = x;
        m_y = y;
```

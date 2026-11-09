```
```csharp
            // p1 does NOT get boxed to call CompareTo.
            // p2 does NOT get boxed because CompareTo(Point) is called.
            Console.WriteLine(p1.CompareTo(p2));// "-1"

            // p1 DOES get boxed, and the reference is placed in c.
            IComparable c = p1;
            Console.WriteLine(c.GetType());// "Point"

            // p1 does NOT get boxed to call CompareTo.
            // Since CompareTo is not being passed a Point variable,
            // CompareTo(Object) is called which requires a reference to
            // a boxed Point.
            // c does NOT get boxed because it already refers to a boxed Point.
            Console.WriteLine(p1.CompareTo(c));// "0"

            // c does NOT get boxed because it already refers to a boxed Point.
            // p2 does get boxed because CompareTo(Object) is called.
            Console.WriteLine(c.CompareTo(p2));// "-1"

            // c is unboxed, and fields are copied into p2.
            p2 = (Point) c;

            // Proves that the fields got copied into p2.
            Console.WriteLine(p2.ToString());// "(10, 10)"
        }
```
```

This code demonstrates several scenarios related to boxing and unboxing:

+   - **Calling ToString**   In the call to ToString, p1 doesn't have to be boxed. At first, you'd think that p1 would have to be boxed because ToString is a virtual method that is inherited from the base type, System.ValueType. Normally, to call a virtual method, the CLR needs to determine the object's type in order to locate the type's method table. Since p1 is an unboxed value type, there's no type object pointer. However, the just-in-time (JIT) compiler sees that Point overrides the ToString method, and it emits code that calls ToString directly (nonvirtually) without having to do any boxing. The compiler knows that polymorphism can't come into play here since Point is a value type, and no type can derive from it to provide another implementation of this virtual method. Note that if Point's ToString method internally calls base.ToString(), then the value type instance would be boxed when calling System.ValueType's ToString method.

+   - **Calling GetType**   In the call to the nonvirtual GetType method, p1 does have to be boxed. The reason is that the Point type inherits GetType from System.Object. So to call GetType, the CLR must use a pointer to a type object, which can be obtained only by boxing p1.

+   - **Calling CompareTo (first time)**   In the first call to CompareTo, p1 doesn't have to be boxed because Point implements the CompareTo method, and the compiler can just call it directly.

Note that a Point variable (p2) is being passed to CompareTo, and therefore the compiler calls the
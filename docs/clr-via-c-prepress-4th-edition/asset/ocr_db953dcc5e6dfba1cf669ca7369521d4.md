overload of CompareTo that accepts a Point parameter. This means that p2 will be passed by value to CompareTo and no boxing is necessary.

+   - **Casting to IComparable**  When casting p1 to a variable (c) that is of an interface type, p1 must be boxed because interfaces are reference types by definition. So p1 is boxed, and the pointer to this boxed object is stored in the variable c. The following call to GetType proves that c does refer to a boxed Point on the heap.
+   
+   - **Calling CompareTo (second time)**  In the second call to CompareTo, p1 doesn’t have to be boxed because Point implements the CompareTo method, and the compiler can just call it directly. Note that an IComparable variable (c) is being passed to CompareTo, and therefore, the compiler calls the overload of CompareTo that accepts an Object parameter. This means that the argument passed must be a pointer that refers to an object on the heap. Fortunately, c does refer to a boxed Point, and therefore, that memory address is c can be passed to CompareTo, and no additional boxing is necessary.
+   
+   - **Calling CompareTo (third time)**  In the third call to CompareTo, c already refers to a boxed Point object on the heap. Since c is of the IComparable interface type, you can only call the interface’s CompareTo method that requires an Object parameter. This means that the argument passed must be a pointer that refers to an object on the heap. So p2 is boxed, and the pointer to this boxed object is passed to CompareTo.
+   
+   - **Casting to Point**  When casting c to a Point, the object on the heap referred to by c is unboxed, and its fields are copied from the heap to p2, an instance of the Point type residing on the stack.

I realize that all of this information about reference types, value types, and boxing might be overwhelming at first. However, a solid understanding of these concepts is critical to any .NET Framework developer’s long-term success. Trust me: having a solid grasp of these concepts will allow you to build efficient applications faster and easier.

# Changing Fields in a Boxed Value Type by Using Interfaces (and Why You Shouldn’t Do This)

Let’s have some fun and see how well you understand value types, boxing, and unboxing. Examine the following code, and see whether you can figure out what it displays on the console:

```
using System;

// Point is a value type.
internal struct Point {
    private Int32 m_x, m_y;

    public Point(Int32 x, Int32 y) {
        m_x = x;
        m_y = y;
```
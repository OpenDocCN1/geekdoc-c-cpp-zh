In code, the CLR is actually checking the object's type twice: The operator first checks to see
of o is compatible with the Employee type. If it is, inside the if statement, the CLR verifies that
o refers to an Employee when performing the cast. The CLR's checking improves security, but
certainly comes at a performance cost, because the CLR must determine the actual type of the object
referred to by the variable (o), and then the CLR must walk the inheritance hierarchy, checking each
base type against the specified type (Employee). Because this programming paradigm is quite common,\# offers a way to simplify this code and improve performance by providing an operator.

```
Employee e = o as Employee;
if (e != null) {
    // Use within the 'if' statement.
}
```

In this code, the CLR checks if o is compatible with the Employee type, and if it is, returns a
on-null reference to the same object. If o is not compatible with the Employee type, as the operator
returns null. Notice that the operator causes the CLR to verify an object's type just once.
if statement simply checks whether e is null; this check can be performed faster than verifying an
object's type.

The operator works just as casting except that the operator will never throw an exception
stead. If the object cannot be cast, the result is null. You'll want to check whether the
resulting reference is null, or attempting to use the resulting reference will cause a System.Null-
ReferenceException to be thrown. The following code demonstrates:

```
Object o = new Object(); // Creates a new Object object
Employee e = o as Employee; // Casts to an Employee
// The cast above fails: no exception is thrown, but e is set to null.
```

e.ToString(); // Accessing throws a NullReferenceException.

To make you understand everything just presented, take the following quiz. Assume that
these two class definitions exist.

```
internal class B { // Base class
}
internal class D : B { // Derived class
}
```

Now examine the lines of C# code in Table 4-3. For each line, decide whether the line would
compile and execute successfully (marked OK in Table 4-3), cause a compile-time error (CTE), or cause a
run-time error (RTE).
# 518 Chapter 9: Introducing Structs and Records

+   3. Implement the strongly typed Equals() helper method, as shown in Listing 9.21, and check if obj is null (reference types only).

```
public bool Equals(Foo? other)
{
    if (other is null) return false;
    // Step 5
    return (this.Number, this.Name) == (other.Number, other.Name);
    return true;
}
```

+   4. For reference types that don't derive from System.Object, check base.Equals(), enabling refactoring.

+   5. Compare each identifying data for equality, preferably using a tuple.

+   6. Override GetHashCode().

+   7. Override the == and != operators (see Chapter 10 – Operator Overloading).

Steps 3 to 4 in an overload of Equals() that takes the custom data type specifically (such as Coordinate). This way, a comparison of two Coordinates will avoid Equals(object? obj) and its type check altogether.
Equals() should never throw any exceptions. It is a valid choice to compare any object with any other object, and doing so should never result in an exception.

> Guidelines

DO implement GetHashCode(), Equals(), the == operator, and the = operator—not one of these without the three.

DO use the same algorithm when implementing Equals(), ==, and !=.

DO NOT throw exceptions from implementations of GetHashCode(), Equals(), =, and !=.
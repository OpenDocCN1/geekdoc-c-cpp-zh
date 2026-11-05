+   - Inheritance tree independence: if B and C are instances of Class2 inherited from Class1: Class1.Equals(A,B) must always return the same value as the call to Class2.Equals(A,B).

```
```csharp
class Student : IEquatable<Student>
{
    public string Name { get; set; } = "";

    public bool Equals(Student other)
    {
        if (ReferenceEquals(other, null)) return false;
        if (ReferenceEquals(other, this)) return true;
        return string.Equals(Name, other.Name);
    }

    public override bool Equals(object obj)
    {
        if (ReferenceEquals(null, obj)) return false;
        if (ReferenceEquals(this, obj)) return true;

        return Equals(obj as Student);
    }

    public override int GetHashCode()
    {
        return Name?.GetHashCode() ?? 0;
    }

    public static bool operator ==(Student left, Student right)
    {
        return Equals(left, right);
    }

    public static bool operator !=(Student left, Student right)
    {
        return !Equals(left, right);
    }
}
```
```

# Section 3.3: Relational Operators

# Equals

Checks whether the supplied operands (arguments) are equal

```
```
"a" == "b"    // Returns false.
"a" == "a"    // Returns true.
1 == 0          // Returns false.
1 == 1          // Returns true.
false == true   // Returns false.
false == false  // Returns true.
```
```

Unlike Java, the equality comparison operator works natively with strings.

The equality comparison operator will work with operands of differing types if an implicit cast exists from one to the other. If no suitable implicit cast exists, you may call an explicit cast or use a method to convert to a compatible type.

```
```
1 == 1.0          // Returns true because there is an implicit cast from int to double.
new Object() == 1.0  // Will not compile.
```
```
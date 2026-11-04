The generic version of IComparable is declared like this:

```
public interface IComparable<T>
```

In this version, the type of data being compared is passed as a type argument to T. This causes the declaration of CompareTo() to be changed, as shown next.

```
int CompareTo(T obj)
```

Here, the type of data that CompareTo() operates on can be explicitly specified. This makes IComparable<T> type-safe. For this reason, IComparable<T> is now preferable to IComparable.

# The IEquatable<T> Interface

IEquatable<T> is implemented by those classes that need to define how two objects should be compared for equality. It defines only one method, Equals(), which is shown here:

```
bool Equals(T obj)
```

The method returns true if obj is equal to the invoking object and false otherwise. IEquatable<T> is implemented by several classes and structures in the .NET Framework, including the numeric structures, Char, Int32, Boolean, and String.

# The IConvertible Interface

The IConvertible interface is implemented by all of the value-type structures, string, and DateTime. It specifies various type conversions. Normally, classes that you create will not need to implement this interface.

# The ICloneable Interface

By implementing the ICloneable interface, you enable a copy of an object to be made. ICloneable defines only one method, Clone(), which is shown here:

```
object Clone()
```

This method makes a copy of the invoking object. How you implement Clone() determines how the copy is made. In general, there are two types of copies: deep and shallow. When a deep copy is made, the copy and original are completely independent. Thus, if the original object contained a reference to another object O, then a copy of O will also be made. In a shallow copy, members are copied, but objects referred to by members are not. If an object refers to some other object O, then after a shallow copy, both the copy and the original will refer to the same O, and any changes to O affect both the copy and the original. Usually, you will implement Clone() so that it performs a deep copy. Shallow copies can be made by using MemberwiseClone(), which is defined by Object. Here is an example that illustrates ICloneable. It creates a class called Test that contains a reference to an object of a class called X. Test uses Clone() to create a deep copy.

```
// Demonstrate ICloneable.

using System;

class X {
```
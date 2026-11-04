# Appendix B: Reserved Identifiers Defined

# abstract

Abstract is a modifier used to declare a generic class. Abstract classes cannot be instantiated,nor can they be modified with a sealed or static modifier. Only abstract classes may use abstract methods and accessors, but all nonabstract classes derived from those classes must include implementations of those references. Abstract methods are also implicitly virtual and their inheriting properties may be overriden (see Example B.1).

# Example B.1.

```
public abstract class Area {}
class Appendix B {
    static void Main() {}
}
```

# as

As is a binary operator that allows for a conversion from an expression to a data type. It is also a useful tool when attempting to avoid exceptions, since it will return a null if the conversion fails (see Example B.2).

# Example B.2.

```
public class Appendix_B {
    public static void Main() {
        object MyString = new object();
        string s = MyString as string;
    }
}
```

# base

Base is the keyword used to access members of a base class from within an inheriting class reference. It is delineated using the keyword base followed by that particular member's definition. A base class can be accessed as a constructor, instance, and/or with an overriding modifier, but they cannot be used with the static modifier (see Example B.3).
implicit interface method implementations are required to match. Thus it is impossible to implicitly implement I<object,C,string>.H<T>. This interface method can be implemented only using an explicit interface member implementation:

```
class C: I<object,C,string>
{
    ...
    public void H<U>(U u) where U: class {...}
    void I<object,C,string>.H<T>(T t) {
        string s = t;  // Okay
        H<T>(t);
    }
}
```

In this example, the explicit interface member implementation invokes a public method having strictly weaker constraints. Note that the assignment from t to s is valid since T inherits a constraint of T: string, even though this constraint is not expressible in source code.

# 13.4.4 Interface Mapping

A class or struct must provide implementations of all members of the interfaces that are listed in the base class list of the class or struct. The process of locating implementations of interface members in an implementing class or struct is known as interface mapping.

Interface mapping for a class or struct C locates an implementation for each member of each interface specified in the base class list of C. The implementation of a particular interface member I.M, where I is the interface in which the member M is declared, is determined by examining each class or struct S, starting with C and repeating for each successive base class of C, until a match is located:

+   - If S contains a declaration of an explicit interface member implementation that matches I and M, then this member is the implementation of I.M.
+   - Otherwise, if S contains a declaration of a nonstatic public member that matches M, then this member is the implementation of I.M. If more than one member matches, it is unspecified which member is the implementation of I.M. This situation can occur only if S is a constructed type where the two members as declared in the generic type have different signatures, but the type arguments make their signatures identical.

A compile-time error occurs if implementations cannot be located for all members of all interfaces specified in the base class list of C. Note that the members of an interface include those members that are inherited from base interfaces.
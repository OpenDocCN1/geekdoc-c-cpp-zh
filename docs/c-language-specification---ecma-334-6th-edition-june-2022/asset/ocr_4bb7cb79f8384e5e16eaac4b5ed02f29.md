# 17.6.5 Interface mapping

A class or struct shall provide implementations of all members of the interfaces that are listed in the base class list of the class or struct. The process of locating implementations of interface members in an implementing class or struct is known as *interface mapping.*

Interface mapping for a class or struct C locates an implementation for each member of each interface specified in the base class list of C. The implementation of a particular interface member I.M, where I is the interface in which the member M is declared, is determined by examining each class or struct S, starting with C and repeating for each successive base class of C, until a match is located:

+   - If S contains a declaration of an explicit interface member implementation that matches I and M, then this member is the implementation of I.M.
+   - Otherwise, if S contains a declaration of a non-static public member that matches M, then this member is the implementation of I.M. If more than one member matches, it is unspecified which member is the implementation of I.M. This situation can only occur if S is a constructed type where the two members as declared in the generic type have different signatures, but the type arguments make their signatures identical.

A compile-time error occurs if implementations cannot be located for all members of all interfaces specified in the base class list of C. The members of an interface include those members that are inherited from base interfaces.

Members of a constructed interface type are considered to have any type parameters replaced with the corresponding type arguments as specified in §14.3.3.

*Example:* For example, given the generic interface declaration:

```
interface I<T>
{
    T F(int x, T[] y);
    T this[int y] { get; }
}
```

the constructed interface I<string[]> has the members:

```
string[] F(int x, string[,] y);
string[] this[int y] { get; }
```

*end example*

For purposes of interface mapping, a class or struct member A matches an interface member B when:

+   - A and B are methods, and the name, type, and formal parameter lists of A and B are identical.
+   - A and B are properties, the name and type of A and B are identical, and A has the same accessors as B (A is permitted to have additional accessors if it is not an explicit interface member implementation).
+   - A and B are events, and the name and type of A and B are identical.
+   - A and B are indexers, the type and formal parameter lists of A and B are identical, and A has the same accessors as B (A is permitted to have additional accessors if it is not an explicit interface member implementation).

Notable implications of the interface-mapping algorithm are:

+   - Explicit interface member implementations take precedence over other members in the same class or struct when determining the class or struct member that implements an interface member.
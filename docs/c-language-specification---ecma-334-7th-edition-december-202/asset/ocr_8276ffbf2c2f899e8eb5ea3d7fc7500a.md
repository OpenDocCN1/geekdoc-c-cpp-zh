```
{
    Console.WriteLine("A.B.F");
}
}
```

class B is a nested type because it is declared within class A, and class A is a non-nested type because it is declared within a compilation unit.

*end example*

# 15.3.9.2 Fully qualified name

The fully qualified name (§7.8.3) for a nested type declaration is S . N where S is the fully qualified name of the type declaration in which type N is declared and N is the unqualified name (§7.8.2) of the nested type declaration (including any generic_dimension_specifier (§12.8.17)).

# 15.3.9.3 Declared accessibility

Non-nested types can have public or internal declared accessibility and have internal declared accessibility by default. Nested types can have these forms of declared accessibility too, plus one or more additional forms of declared accessibility, depending on whether the containing type is a class or struct:

+   - A nested type that is declared in a class can have any of the permitted kinds of declared accessibility and, like other class members, defaults to private declared accessibility.
+   - A nested type that is declared in a struct can have any of three forms of declared accessibility (public, internal, or private) and, like other struct members, defaults to private declared accessibility.

Example: The example

```
public class List
{
    // Private data structure
    private class Node
    {
        public object Data;
        public Node Next;

        public Node(object data, Node next)
        {
            this.Data = data;
            this.Next = next;
        }
    }

    private Node first = null;
    private Node last = null;

    // Public interface
    public void AddToFront(object o) {...}
    public void AddToBack(object o) {...}
    public object RemoveFromFront() {...}
    public object RemoveFromBack() {...}
    public int Count { get {...} }
}
```
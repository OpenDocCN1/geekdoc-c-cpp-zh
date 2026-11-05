The two namespace declarations above contribute to the same declaration space, in this case declaring two classes with the fully qualified names Megacorp.Data.Customer and Megacorp.Data.Order. Because the two declarations contribute to the same declaration space, it would have caused a compile-time error if each contained a declaration of a class with the same name.

As specified above, the declaration space of a block includes any nested blocks. Thus, in the following example, the F and G methods result in a compile-time error because the name i is declared in the outer block and cannot be redeclared in the inner block. However, the H and I methods are valid since the two i’s are declared in separate non-nested blocks.

```
class A
{
    void F() {
        int i = 0;
        if (true) {
            int i = 1;
        }
    }
    void G() {
        if (true) {
            int i = 0;
        }
        int i = 1;
    }
    void H() {
        if (true) {
            int i = 0;
        }
        if (true) {
            int i = 1;
        }
    }
    void I() {
        for (int i = 0; i < 10; i++)
            H();
        for (int i = 0; i < 10; i++)
            H();
    }
}
```

# 3.4 Members

Namespaces and types have members. The members of an entity are generally available through the use of a qualified name that starts with a reference to the entity, followed by a '.' token, followed by the name of the member.

Members of a type are either declared in the type declaration or inherited from the base class of the type. When a type inherits from a base class, all members of the base class, except instance constructors, destructors and static constructors, become members of the derived type. The declared accessibility of a base class member does not control whether the member is inherited—inheriance extends to any member that isn’t an instance constructor, static constructor, or destructor. However, an inherited member may not be accessible in a derived type, either because of its declared accessibility (§3.5.1) or because it is hidden by a declaration in the type itself (§3.7.1.2).

# 3.4.1 Namespace members

Namespaces and types that have no enclosing namespace are members of the global namespace. This corresponds directly to the names declared in the global declaration space.
# ISO/IEC 14882:2017(E)

has a virtual base class of type V. Given the class C defined above, an object of class C will have one subobject of V, as shown in Figure 4. end note]

+   7 [Note: A class can have both virtual and non-virtual base classes of a given type.

```
class B { / ... / };
class X : virtual public B { / ... / };
class Y : virtual public B { / ... / };
class Z : public B { / ... / };
class AA : public X, public Z { / ... / };
```

For an object of class AA, all virtual occurrences of base B in the lattice of AA correspond to a single B subobject within the type of AA, and every other occurrence of a (non-virtual) base class B in the lattice of AA one-to-one with a distinct B subobject within the type of AA. Given the class AA defined above, class AA has two subobjects of B: Z and the virtual B shared by X and Y, as shown in Figure 5.

![](bbox=[0.368, 0.345, 0.632, 0.423])

end note Figure 5 Virtual and non-virtual base class

# 13.2 Member lookup [class.member.lookup]

+   1 Member name lookup determines the name of a (id-expression) in class (6.3.7). Name lookup can result in an ambiguity, in which case the program is ill-formed. For an id-expression, name lookup begins in the scope of the thing; for a qualified-id, name lookup begins in the scope of the nested-name-specifier. Name lookup takes precedence before access (6.4, 14.4).

+   2 The following steps define the set of name lookup for member f in a class C.

+   3 The lookup set for f in C, S(f,C), consists of two component sets: the declarations set (possibly including using-declarations) f; the subobject set, a set of subsets where declarations of these members are overridden. In the declaration set, using-declarations are replaced by those of designated declarations that are not hidden or overridden (10.3.3), and type declarations (including nested-class declarations). S(f,C) is calculated as follows:

+   4 If C contains a declaration of name f, the declaration set contains every declaration of f declared in C that satisfies the requirements of the language construct in which the lookup occurs. Note: Looking up in an elaborated-type-specifier (6.4.4) or base-specifier (10.3), for instance, ignores all non-type declarations, while looking up a name in a nested-name-specifier (6.4.3) ignores function, variable, and enumerator declarations. As an example, looking up a name in a using-declaration (10.33) includes the declaration of a class or enumeration that would ordinarily be hidden by another declaration of name in the same scope. end note] If the resulting declaration set is not empty, the subobject contains C itself, and calculation is complete.

+   5 Otherwise (i.e., C does not contain a declaration of f or the resulting declaration set is empty), S(f,C) is initially empty. If C has base classes, the lookup set for f in each direct base class subobject B, and merge each lookup set S(f,B) into S(f,C).

§ 13.2 ISO/IEC 14882:2017 - All rights reserved 258
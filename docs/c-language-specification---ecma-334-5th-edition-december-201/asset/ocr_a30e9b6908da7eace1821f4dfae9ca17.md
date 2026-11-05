Depending on the context in which a member declaration takes place, only certain types of declared accessibility are permitted. Furthermore, when a member declaration does not include any access modifiers, the context in which the declaration takes place determines the default declared accessibility.

+   - Namespaces implicitly have public declared accessibility. No access modifiers are allowed on namespace declarations.
+   - Types declared directly in compilation units or namespaces (as opposed to within other types) can have public or internal declared accessibility and default to internal declared accessibility.
+   - Class members can have any of the five kinds of declared accessibility and default to private declared accessibility. [Note: A type declared as a member of a class can have any of the five kinds of declared accessibility, whereas a type declared as a member of a namespace can have only public or internal declared accessibility. end note]
+   - Struct members can have public, internal, or private declared accessibility and default to private declared accessibility because structs are implicitly sealed. Struct members introduced in a struct (that is, not inherited by that struct) cannot have protected or protected internal declared accessibility. [Note: A type declared as a member of a struct can have public, internal, or private declared accessibility, whereas a type declared as a member of a namespace can have only public or internal declared accessibility. end note]
+   - Interface members implicitly have public declared accessibility. No access modifiers are allowed on interface member declarations.
+   - Enumeration members implicitly have public declared accessibility. No access modifiers are allowed on enumeration member declarations.

# 8.5.3 Accessibility domains

The accessibility domain of a member consists of the (possibly disjoint) sections of program text in which access to the member is permitted. For purposes of defining the accessibility domain of a member, a member is said to be top-level if it is not declared within a type, and a member is said to be nested if it is declared within another type. Furthermore, the program text of a program is defined as all program text contained in all source files of the program, and the program text of a type is defined as all program text contained in the type-declarations of that type (including, possibly, types that are nested within the type).

The accessibility domain of a predefined type (such as object, int, or double) is unlimited.

The accessibility domain of a top-level unbound type T (§9.4.4) that is declared in a program P is defined as follows:

+   - If the declared accessibility of T is public, the accessibility domain of T is the program text of P and any program that references P.
+   - If the declared accessibility of T is internal, the accessibility domain of T is the program text of P.

[Note: From these definitions, it follows that the accessibility domain of a top-level unbound type is always at least the program text of the program in which that type is declared. end note]

The accessibility domain for a constructed type T<A1, ..., An> is the intersection of the accessibility domain of the unbound generic type T and the accessibility domains of the type arguments A1, ..., An.

The accessibility domain of a nested member M declared in a type T within a program P, is defined as follows (noting that M itself might possibly be a type):

+   - If the declared accessibility of M is public, the accessibility domain of M is the accessibility domain of T.
+   - If the declared accessibility of M is protected internal, let D be the union of the program text of P and the program text of any type derived from T, which is declared outside P. The accessibility domain of M is the intersection of the accessibility domain of T with D.
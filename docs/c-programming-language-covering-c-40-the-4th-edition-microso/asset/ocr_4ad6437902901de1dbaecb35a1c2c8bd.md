In the above example, the constructed type D<int> has a non-inherited member public int G(string s) obtained by substituting the type argument int for the type parameter T. D<int> also has an inherited member from the class declaration B. This inherited member is determined by first determining the base class type B<int[]> of D<int> by substituting int for T in the base class specification B<T[]>. Then, as a type argument to B, int[] is substituted for U in public U F(long index), yielding the inherited member public int[] F(long index).

# 10.3.4 The new Modifier

A class-member-declaration is permitted to declare a member with the same name or signature as an inherited member. When this occurs, the derived class member is said to hide the base class member. Hiding an inherited member is not considered an error, but it does cause the compiler to issue a warning. To suppress the warning, the declaration of the derived class member can include a new modifier to indicate that the derived member is intended to hide the base member. This topic is discussed further in §3.7.1.2.

If a new modifier is included in a declaration that doesn’t hide an inherited member, a warning to that effect is issued. This warning is suppressed by removing the new modifier.

# 10.3.5 Access Modifiers

A class-member-declaration can have any one of the five possible kinds of declared accessibility (§3.5.1): public, protected internal, protected, internal, or private. Except for the protected internal combination, it is a compile-time error to specify more than one access modifier. When a class-member-declaration does not include any access modifiers, private is assumed.

# 10.3.6 Constituent Types

Types that are used in the declaration of a member are called the constituent types of that member. Possible constituent types are the type of a constant, field, property, event, or indexer; the return type of a method or operator; and the parameter types of a method, indexer, operator, or instance constructor. The constituent types of a member must be at least as accessible as that member itself (§3.5.4).

# 10.3.7 Static and Instance Members

Members of a class are either static members or instance members. Generally speaking, it is useful to think of static members as belonging to class types and instance members as belonging to objects (instances of class types).
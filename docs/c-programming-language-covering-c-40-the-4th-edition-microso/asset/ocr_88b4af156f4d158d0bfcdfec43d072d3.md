+   - The members of ulong are the members of the System.UInt64 struct.
+   - The members of char are the members of the System.Char struct.
+   - The members of float are the members of the System.Single struct.
+   - The members of double are the members of the System.Double struct.
+   - The members of decimal are the members of the System.Decimal struct.
+   - The members of bool are the members of the System.Boolean struct.

# 3.4.3 Enumeration Members

The members of an enumeration are the constants declared in the enumeration and the members inherited from the enumeration's direct base class System.Enum and the indirect base classes System.ValueType and object.

# 3.4.4 Class Members

The members of a class are the members declared in the class and the members inherited from the base class (except for class object, which has no base class). The members inherited from the base class include the constants, fields, methods, properties, events, indexers, operators, and types of the base class, but not the instance constructors, destructors, and static constructors of the base class. Base class members are inherited without regard to their accessibility.

A class declaration may contain declarations of constants, fields, methods, properties, events, indexers, operators, instance constructors, destructors, static constructors, and types.

The members of object and string correspond directly to the members of the class types they alias:

+   - The members of object are the members of the System.Object class.
+   - The members of string are the members of the System.String class.

# 3.4.5 Interface Members

The members of an interface are the members declared in the interface and in all base interfaces of the interface. The members in class object are not, strictly speaking, members of any interface (§13.2). However, the members in class object are available via member lookup in any interface type (§7.4).

# 3.4.6 Array Members

The members of an array are the members inherited from class System.Array.
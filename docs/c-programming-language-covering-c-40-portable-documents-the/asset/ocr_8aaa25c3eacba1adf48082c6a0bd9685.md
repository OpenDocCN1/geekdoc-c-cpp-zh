The following rules apply to all operator declarations:

+   - An operator declaration must include both a public and a static modifier.
+   - The parameter(s) of an operator must be value parameters. It is a compile-time error for an operator declaration to specify ref or out parameters.
+   - The signature of an operator (§10.10.1, §10.10.2, §10.10.3) must differ from the signatures of all other operators declared in the same class.
+   - All types referenced in an operator declaration must be at least as accessible as the operator itself (§3.5.4).
+   - It is an error for the same modifier to appear multiple times in an operator declaration.

Each operator category imposes additional restrictions, as described in the following sections.

Like other members, operators declared in a base class are inherited by derived classes. Because operator declarations always require the class or struct in which the operator is declared to participate in the signature of the operator, it is not possible for an operator declared in a derived class to hide an operator declared in a base class. Thus the new modifier is never required, and therefore never permitted, in an operator declaration.

Additional information on unary and binary operators can be found in §7.3.

Additional information on conversion operators can be found in §6.4.

# ### 10.10.1 Unary Operators

The following rules apply to unary operator declarations, where T denotes the instance type of the class or struct that contains the operator declaration:

+   - A unary +, -, !, or ~ operator must take a single parameter of type T or T? and can return any type.
+   - A unary ++ or -- operator must take a single parameter of type T or T? and must return that same type or a type derived from it.
+   - A unary true or false operator must take a single parameter of type T or T? and must return type bool.

The signature of a unary operator consists of the operator token (+, -, !, ~, ++, --, true, or false) and the type of the single formal parameter. The return type is not part of a unary operator's signature, nor is the name of the formal parameter.
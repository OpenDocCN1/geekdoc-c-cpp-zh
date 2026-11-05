The member-access is evaluated and classified as follows:

+   - If K is zero, E is a namespace, and E contains a nested namespace with name I, then the result is that namespace.
+   - Otherwise, if E is a namespace and E contains an accessible type having name I and K type parameters, then the result is that type constructed with the given type arguments.
+   - If E is a predefined-type or a primary-expression classified as a type, if E is not a type parameter, and if a member lookup (§7.4) of I in E with K type parameters produces a match, then E.I is evaluated and classified as follows:

If I identifies a type, then the result is that type constructed with the given type arguments.

If I identifies one or more methods, then the result is a method group with no associated instance expression. If a type argument list was specified, it is used in calling a generic method (§7.6.5.1).

If I identifies a static property, then the result is a property access with no associated instance expression.

If I identifies a static field:
- If the field is readonly and the reference occurs outside the static constructor of the class or struct in which the field is declared, then the result is a value—namely, the value of the static field I in E.
- Otherwise, the result is a variable—namely, the static field I in E.

If I identifies a static event:
- If the reference occurs within the class or struct in which the event is declared, and the event was declared without event-accessor-declarations (§10.8), then E.I is processed exactly as if I were a static field.
- Otherwise, the result is an event access with no associated instance expression.

If I identifies a constant, then the result is a value—namely, the value of that constant.

If I identifies an enumeration member, then the result is a value—namely, the value of that enumeration member.

Otherwise, E.I is an invalid member reference, and a compile-time error occurs.
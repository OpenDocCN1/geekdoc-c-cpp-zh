are non-null, the lifted operator unwraps the operands and applies the underlying operator to produce the bool result.

+   - For the relational operators
+     - < > <= >=

a lifted form of an operator exists if the operand types are both non-nullable value types and if the result type is bool. The lifted form is constructed by adding a single ? modifier to each operand type. The lifted operator produces the value false if one or both operands are null. Otherwise, the lifted operator unwraps the operands and applies the underlying operator to produce the bool result.

# 12.5 Member lookup

# 12.5.1 General

A member lookup is the process whereby the meaning of a name in the context of a type is determined. A member lookup can occur as part of evaluating a simple-name (§12.7.3) or a member-access (§12.7.5) in an expression. If the simple-name or member-access occurs as the primary-expression of an invocation-expression (§12.7.6.2), the member is said to be invoked.

If a member is a method or event, or if it is a constant, field or property of either a delegate type (§20) or the type dynamic (§9.2.4), then the member is said to be invocable.

Member lookup considers not only the name of a member but also the number of type parameters the member has and whether the member is accessible. For the purposes of member lookup, generic methods and nested generic types have the number of type parameters indicated in their respective declarations and all other members have zero type parameters.

A member lookup of a name N with K type arguments in a type T is processed as follows:

+   - First, a set of accessible members named N is determined:
+     - If T is a type parameter, then the set is the union of the sets of accessible members named N in each of the types specified as a primary constraint or secondary constraint (§15.2.5) for T, along with the set of accessible members named N in object.
+     - Otherwise, the set consists of all accessible (§8.5) members named N in T, including inherited members and the accessible members named N in object. If T is a constructed type, the set of members is obtained by substituting type arguments as described in §15.3.3. Members that include an override modifier are excluded from the set.
+   - Next, if K is zero, all nested types whose declarations include type parameters are removed. If K is not zero, all members with a different number of type parameters are removed. When K is zero, methods having type parameters are not removed, since the type inference process (§12.6.3) might be able to infer the type arguments.
+   - Next, if the member is invoked, all non-invocable members are removed from the set.
+   - Next, members that are hidden by other members are removed from the set. For every member S.M in the set, where S is the type in which the member M is declared, the following rules are applied:
+     - If M is a constant, field, property, event, or enumeration member, then all members declared in a base type of S are removed from the set.
+     - If M is a type declaration, then all non-types declared in a base type of S are removed from the set, and all type declarations with the same number of type parameters as M declared in a base type of S are removed from the set.
+     - If M is a method, then all non-method members declared in a base type of S are removed from the set.
+   - Next, interface members that are hidden by class members are removed from the set. This step only has an effect if T is a type parameter and T has both an effective base class other than object and a
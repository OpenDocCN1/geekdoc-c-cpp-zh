A member lookup of a name N with K type parameters in a type T is processed as follows:

+   - First, a set of accessible members named N is determined:
+     - If T is a type parameter, then the set is the union of the sets of accessible members named N in each of the types specified as a primary constraint or secondary constraint (§10.1.5) for T, along with the set of accessible members named N in object.
+     - Otherwise, the set consists of all accessible (§3.5) members named N in T, including inherited members and the accessible members named N in object. If T is a constructed type, the set of members is obtained by substituting type arguments as described in §10.3.2. Members that include an override modifier are excluded from the set.

+   - Next, if K is zero, all nested types whose declarations include type parameters are removed. If K is not zero, all members with a different number of type parameters are removed. Note that when K is zero, methods having type parameters are not removed, since the type inference process (§7.5.2) might be able to infer the type arguments.

+   - Next, if the member is *invoked*, all non-*invocable* members are removed from the set.

> VLADIMIR RESHETNIKOV This rule allows you to invoke an extension method even if a non-invocable instance member with the same name exists in the type T. For example, you can invoke extension method Count() on a collection even if it has an instance property Count of type int.

+   - Next, members that are hidden by other members are removed from the set. For every member S.M in the set, where S is the type in which the member M is declared, the following rules are applied:
+     - If M is a constant, field, property, event, or enumeration member, then all members declared in a base type of S are removed from the set.
+     - If M is a type declaration, then all nontypes declared in a base type of S are removed from the set, and all type declarations with the same number of type parameters as M declared in a base type of S are removed from the set.
+     - If M is a method, then all nonmethod members declared in a base type of S are removed from the set.

> VLADIMIR RESHETNIKOV Any members removed from the set on this step can still cause other members to be removed from the set. Thus the order in which the members are processed is not important.
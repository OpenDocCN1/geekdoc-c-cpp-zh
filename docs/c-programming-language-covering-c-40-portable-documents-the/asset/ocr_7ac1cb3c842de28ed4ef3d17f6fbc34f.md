using-directive occurs. A using-directive may make zero or more namespace or type names available within a particular compilation-unit or namespace-body, but does not contribute any new members to the underlying declaration space. In other words, a using-directive is not transitive, but rather affects only the compilation-unit or namespace-body in which it occurs.

+   - The scope of a type parameter declared by a type-parameter-list on a class-declaration (§10.1) is the class-base, type-parameter-constraints-clauses, and class-body of that class-declaration.
+   - The scope of a type parameter declared by a type-parameter-list on a struct-declaration (§11.1) is the struct-interfaces, type-parameter-constraints-clauses, and struct-body of that struct-declaration.
+   - The scope of a type parameter declared by a type-parameter-list on an interface-declaration (§13.1) is the interface-base, type-parameter-constraints-clauses, and interface-body of that interface-declaration.
+   - The scope of a type parameter declared by a type-parameter-list on a delegate-declaration (§15.1) is the return-type, formal-parameter-list, and type-parameter-constraints-clauses of that delegate-declaration.
+   - The scope of a member declared by a class-member-declaration (§10.1.6) is the class-body in which the declaration occurs. In addition, the scope of a class member extends to the class-body of those derived classes that are included in the accessibility domain (§3.5.2) of the member.
+   - The scope of a member declared by a struct-member-declaration (§11.2) is the struct-body in which the declaration occurs.
+   - The scope of a member declared by an enum-member-declaration (§14.3) is the enum-body in which the declaration occurs.
+   - The scope of a parameter declared in a method-declaration (§10.6) is the method-body of that method-declaration.
+   - The scope of a parameter declared in an indexer-declaration (§10.9) is the accessor-declarations of that indexer-declaration.
+   - The scope of a parameter declared in an operator-declaration (§10.10) is the block of that operator-declaration.
+   - The scope of a parameter declared in a constructor-declaration (§10.11) is the constructor-initializer and block of that constructor-declaration.
+   - The scope of a parameter declared in a lambda-expression (§7.15) is the lambda-expression-body of that lambda-expression.
+   - The scope of a parameter declared in an anonymous-method-expression (§7.15) is the block of that anonymous-method-expression.
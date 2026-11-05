+   - If the declaration includes the partial modifier, then it does not include any of the following modifiers: new, public, protected, internal, private, virtual, sealed, override, abstract, or extern.

Methods are classified according to what, if anything, they return:

+   - If ref is present, the method is returns-by-ref and returns a variable reference, that is optionally read-only;
+   - Otherwise, if return_type is void, the method is returns-no-value and does not return a value;
+   - Otherwise, the method is returns-by-value and returns a value.

The return_type of a returns-by-value or returns-no-value method declaration specifies the type of the result, if any, returned by the method. Only a returns-no-value method may include the partial modifier (§15.6.9). If the declaration includes the async modifier then return_type shall be void or the method returns-by-value and the return type is a task type (§15.15.1).

The ref_return_type of a returns-by-ref method declaration specifies the type of the variable referenced by the variable_reference returned by the method.

A generic method is a method whose declaration includes a type_parameter_list. This specifies the type parameters for the method. The optional type_parameter_constraints_clauses specify the constraints for the type parameters.

A generic method_declaration for an explicit interface member implementation shall not have any type_parameter_constraints_clauses; the declaration inherits any constraints from the constraints on the interface method.

Similarly, a method declaration with the override modifier shall not have any type_parameter_constraints_clauses and the constraints of the method's type parameters are inherited from the virtual method being overridden.

The member_name specifies the name of the method. Unless the method is an explicit interface member implementation (§18.6.2), the member_name is simply an identifier.

For an explicit interface member implementation, the member_name consists of an interface_type followed by a '.' and an identifier. In this case, the declaration shall include no modifiers other than (possibly) extern or async.

The optional formal_parameter_list specifies the parameters of the method (§15.6.2).

The return_type or ref_return_type, and each of the types referenced in the formal_parameter_list of a method, shall be at least as accessible as the method itself (§7.5.5).

The method_body of a returns-by-value or returns-no-value method is either a semicolon, a block body or an expression body. A block body consists of a block, which specifies the statements to execute when the method is invoked. An expression body consists of =>, followed by a null_conditional_invocation_expression or expression, and a semicolon, and denotes a single expression to perform when the method is invoked.

For abstract and extern methods, the method_body consists simply of a semicolon. For partial methods the method_body may consist of either a semicolon, a block body or an expression body. For all other methods, the method_body is either a block body or an expression body.

If the method_body consists of a semicolon, the declaration shall not include the async modifier.

The ref_method_body of a returns-by-ref method is either a semicolon, a block body or an expression body. A block body consists of a block, which specifies the statements to execute when the method is
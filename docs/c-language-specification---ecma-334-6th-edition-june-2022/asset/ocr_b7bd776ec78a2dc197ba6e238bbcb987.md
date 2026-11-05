Similarly, a method declaration with the override modifier shall not have any type_parameter_constraints_clauses and the constraints of the method's type parameters are inherited from the virtual method being overridden. The member_name specifies the name of the method. Unless the method is an explicit interface member implementation (§17.6.2), the member_name is simply an identifier. For an explicit interface member implementation, the member_name consists of an interface_type followed by a "." and an identifier. In this case, the declaration shall include no modifiers other than (possibly) extern or async.

The optional formal_parameter_list specifies the parameters of the method (§14.6.2).

The return_type and each of the types referenced in the formal_parameter_list of a method shall be at least as accessible as the method itself (§7.5.5).

The method_body is either a semicolon, a block body or an expression body. A block body consists of a block, which specifies the statements to execute when the method is invoked. An expression body consists of =>, followed by a null_conditional_invocation_expression or expression, followed by a semicolon, and denotes a single expression to perform when the method is invoked.

For abstract and extern methods, the method_body consists simply of a semicolon. For partial methods the method_body may consist of either a semicolon, a block body or an expression body. For all other methods, the method_body is either a block body or an expression body.

If the method_body consists of a semicolon, the declaration shall not include the async modifier.

The name, the number of type parameters, and the formal parameter list of a method define the signature (§7.6) of the method. Specifically, the signature of a method consists of its name, the number of its type parameters, and the number, parameter_mode_modifiers (§14.6.2.1), and types of its formal parameters. The return type is not part of a method's signature, nor are the names of the formal parameters, the names of the type parameters, or the constraints. When a formal parameter type references a type parameter of the method, the ordinal position of the type parameter (not the name of the type parameter) is used for type equivalence.

The name of a method shall differ from the names of all other non-methods declared in the same class. In addition, the signature of a method shall differ from the signatures of all other methods declared in the same class, and two methods declared in the same class may not have signatures that differ solely by ref and out.

The method's type_parameters are in scope throughout the method_declaration, and can be used to form types throughout that scope in return_type, method_body, and type_parameter_constraints_clauses but not in attributes.

All formal parameters and type parameters shall have different names.

# 14.6.2 Method parameters

# 14.6.2.1 General

The parameters of a method, if any, are declared by the method's formal_parameter_list.

```
formal_parameter_list
: fixed_parameters
| fixed_parameters ',' parameter_array
| parameter_array
;

fixed_parameters
: fixed_parameter (',' fixed_parameter)*
```
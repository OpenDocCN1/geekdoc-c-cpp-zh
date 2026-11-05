and the constraints of the method's type parameters are inherited from the virtual method being overridden. The member-name specifies the name of the method. Unless the method is an explicit interface member implementation (§18.6.2), the member-name is simply an identifier. For an explicit interface member implementation, the member-name consists of an interface-type followed by a "." and an identifier. In this case, the declaration shall include no modifiers other than (possibly) extern or async.

The optional formal-parameter-list specifies the parameters of the method (§15.6.2).

The return-type and each of the types referenced in the formal-parameter-list of a method shall be at least as accessible as the method itself (§8.5.5).

For abstract and extern methods, the method-body consists simply of a semicolon. For partial methods the method-body may consist of either a semicolon or a block. For all other methods, the method-body consists of a block, which specifies the statements to execute when the method is invoked.

If the method-body consists of a semicolon, the declaration shall not include the async modifier.

The name, the number of type parameters, and the formal parameter list of a method define the signature (§8.6) of the method. Specifically, the signature of a method consists of its name, the number of its type parameters, and the number, parameter-mode-modifiers (§15.6.2.1), and types of its formal parameters. The return type is not part of a method's signature, nor are the names of the formal parameters, the names of the type parameters, or the constraints. When a formal parameter type references a type parameter of the method, the ordinal position of the type parameter (not the name of the type parameter) is used for type equivalence.

The name of a method shall differ from the names of all other non-methods declared in the same class. In addition, the signature of a method shall differ from the signatures of all other methods declared in the same class, and two methods declared in the same class may not have signatures that differ solely by ref and out.

The method's type-parameters are in scope throughout the method-declaration, and can be used to form types throughout that scope in return-type, method-body, and type-parameter-constraints-clauses but not in attributes.

All formal parameters and type parameters shall have different names.

# 15.6.2 Method parameters

# 15.6.2.1 General

The parameters of a method, if any, are declared by the method's formal-parameter-list.

```
formal-parameter-list:
    fixed-parameters
    fixed-parameters , parameter-array
    parameter-array
fixed-parameters:
    fixed-parameter
    fixed-parameters , fixed-parameter
fixed-parameter:
    attributesopt parameter-modifieropt type identifier default-argumentopt
default-argument:
    = expression
parameter-modifier:
    parameter-mode-modifier
    this
```
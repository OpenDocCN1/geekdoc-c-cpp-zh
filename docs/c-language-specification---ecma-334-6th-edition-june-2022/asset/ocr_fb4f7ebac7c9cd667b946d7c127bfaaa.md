```
; fixed_parameter
: attributes? parameter_modifier? type identifier default_argument?
;

default_argument
: '=' expression
;

parameter_modifier
: parameter_mode_modifier
| 'this'
;

parameter_mode_modifier
: 'ref'
| 'out'
;

parameter_array
: attributes? 'params' array_type identifier
;
```

The formal parameter list consists of one or more comma-separated parameters of which only the last may be a parameter_array.

A fixed_parameter consists of an optional set of attributes (§21); an optional ref, out, or this modifier; a type; an identifier; and an optional default_argument. Each fixed_parameter declares a parameter of the given type with the given name. The this modifier designates the method as an extension method and is only allowed on the first parameter of a static method in a non-generic, non-nested static class. Extension methods are further described in §14.6.10. A fixed_parameter with a default_argument is known as an optional parameter, whereas a fixed_parameter without a default_argument is a required parameter. A required parameter may not appear after an optional parameter in a formal_parameter_list.

A parameter with a ref, out or this modifier cannot have a default_argument. The expression in a default_argument shall be one of the following:

+   - a constant_expression
+   - an expression of the form new S() where S is a value type
+   - an expression of the form default(S) where S is a value type

The expression shall be implicitly convertible by an identity or nullable conversion to the type of the parameter.

If optional parameters occur in an implementing partial method declaration (§14.6.9), an explicit interface member implementation (§17.6.2), a single-parameter indexer declaration (§14.9), or in an operator declaration (§14.10.1) the compiler should give a warning, since these members can never be invoked in a way that permits arguments to be omitted.

A parameter_array consists of an optional set of attributes (§21), a params modifier, an array_type, and an identifier. A parameter array declares a single parameter of the given array type with the given name. The array_type of a parameter array shall be a single-dimensional array type (§16.2). In a method invocation, a parameter array permits either a single argument of the given array type to be specified, or it permits
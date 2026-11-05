function is the *anonymous_function_body* (§7.7). Together with the parameter list (if given) the anonymous-method-body constitutes a declaration space (§7.3). It is thus a compile-time error for the name of a parameter of the anonymous function to match the name of a local variable, local constant or parameter whose scope includes the *anonymous_method_expression* or *lambda_expression*.

If an anonymous function has an *explicit_anonymous_function_signature*, then the set of compatible delegate types and expression tree types is restricted to those that have the same parameter types and modifiers in the same order (§10.7). In contrast to method group conversions (§10.8), contra-variance of anonymous function parameter types is not supported. If an anonymous function does not have an *anonymous_function_signature*, then the set of compatible delegate types and expression tree types is restricted to those that have no out parameters.

Note that an *anonymous_function_signature* cannot include attributes or a parameter array. Nevertheless, an *anonymous_function_signature* may be compatible with a delegate type whose parameter list contains a parameter array.

Note also that *conversion* to an expression tree type, even if compatible, may still fail at compile-time (§8.6).

# 12.19.3 Anonymous function bodies

The body (*expression* or *block*) of an anonymous function is subject to the following rules:

+   - If the anonymous function includes a signature, the parameters specified in the signature are available in the body. If the anonymous function has no signature it can be converted to a delegate type or expression type having parameters (§10.7), but the parameters cannot be accessed in the body.
+   - Except for *in*, *out*, or *ref* parameters specified in the signature (if any) of the nearest enclosing anonymous function, it is a compile-time error for the body to access an *in*, *out*, or *ref* parameter.
+   - Except for parameters specified in the signature (if any) of the nearest enclosing anonymous function, it is a compile-time error for the body to access a parameter of a *ref struct* type.
+   - When the type of *this* is a struct type, it is a compile-time error for the body to access *this*. This is true whether the access is explicit (as in *this.x*) or implicit (as in *x* where *x* is an instance member of the struct). This rule simply prohibits such access and does not affect whether member lookup results in a member of the struct.
+   - The body has access to the outer variables (§12.19.6) of the anonymous function. Access of an outer variable will reference the instance of the variable that is active at the time the *lambda_expression* or *anonymous_method_expression* is evaluated (§12.19.7).
+   - It is a compile-time error for the body to contain a *goto* statement, a *break* statement, or a *continue* statement whose target is outside the body or within the body of a contained *anonymous function*.
+   - A *return* statement in the body returns control from an invocation of the nearest enclosing *anonymous function*, not from the enclosing function member.

It is explicitly unspecified whether there is any way to execute the block of an anonymous function other than through evaluation and invocation of the *lambda_expression* or *anonymous_method_expression*. In particular, the compiler may choose to implement an anonymous function by synthesizing one or more named methods or types. The names of any such synthesized elements shall be of a form reserved for compiler use (§6.4.3).
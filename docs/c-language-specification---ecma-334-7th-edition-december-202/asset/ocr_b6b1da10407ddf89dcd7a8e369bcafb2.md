The optional constructor_initializer specifies another instance constructor to invoke before executing the statements given in the constructor_body of this instance constructor. This is described further in §15.11.2.

When a constructor declaration includes an extern modifier, the constructor is said to be an external constructor. Because an external constructor declaration provides no actual implementation, its constructor_body consists of a semicolon. For all other constructors, the constructor_body consists of either

+   - a block, which specifies the statements to initialize a new instance of the class; or
+   - an expression body, which consists of => followed by an expression and a semicolon, and denotes a single expression to initialize a new instance of the class.

A constructor_body that is a block or expression body corresponds exactly to the block of an instance method with a void return type (§15.6.11).

Instance constructors are not inherited. Thus, a class has no instance constructors other than those actually declared in the class, with the exception that if a class contains no instance constructor declarations, a default instance constructor is automatically provided (§15.11.5).

Instance constructors are invoked by object_creation_expressions (§12.8.16.2) and through constructor_initializers.

# 15.11.2 Constructor initializers

All instance constructors (except those for class object) implicitly include an invocation of another instance constructor immediately before the constructor_body. The constructor to implicitly invoke is determined by the constructor_initializer:

+   - An instance constructor initializer of the form base(argument_list) (where argument_list is optional) causes an instance constructor from the direct base class to be invoked. That constructor is selected using argument_list and the overload resolution rules of §12.6.4. The set of candidate instance constructors consists of all the accessible instance constructors of the direct base class. If this set is empty, or if a single best instance constructor cannot be identified, a compile-time error occurs.
+   - An instance constructor initializer of the form this(argument_list) (where argument_list is optional) invokes another instance constructor from the same class. The constructor is selected using argument_list and the overload resolution rules of §12.6.4. The set of candidate instance constructors consists of all instance constructors declared in the class itself. If the resulting set of applicable instance constructors is empty, or if a single best instance constructor cannot be identified, a compile-time error occurs. If an instance constructor declaration invokes itself through a chain of one or more constructor initializers, a compile-time error occurs.

If an instance constructor has no constructor initializer, a constructor initializer of the form base() is implicitly provided.

> Note: Thus, an instance constructor declaration of the form
> C(...) {...}
> is exactly equivalent to
> C(...) : base() {...}
> end note
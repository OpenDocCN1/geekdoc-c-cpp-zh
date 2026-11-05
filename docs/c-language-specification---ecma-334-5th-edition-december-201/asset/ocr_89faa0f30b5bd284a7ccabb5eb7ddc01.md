the conversion from Digit to byte is implicit because it never throws exceptions or loses information, but the conversion from byte to Digit is explicit since Digit can only represent a subset of the possible values of a byte. end example]

# 15.11 Instance constructors

# 15.11.1 General

An *instance constructor* is a member that implements the actions required to initialize an instance of a class. Instance constructors are declared using *constructor-declarations*:

```
```
constructor-declaration:
    attributes_opt constructor-modifiers_opt constructor-declarator constructor-body

constructor-modifiers:
    constructor-modifier
    constructor-modifiers constructor-modifier

constructor-modifier:
    public
    protected
    internal
    private
    extern

constructor-declarator:
    identifier ( formal-parameter-list_opt ) constructor-initializer_opt

constructor-initializer:
    : base ( argument-list_opt )
    : this ( argument-list_opt )

constructor-body:
    block
    ;
```
```

A *constructor-declaration* may include a set of *attributes* (§22), a valid combination of the four access modifiers (§15.3.6), and an *extern* (§15.6.8) modifier. A constructor declaration is not permitted to include the same modifier multiple times.

The *identifier* of a *constructor-declarator* shall name the class in which the instance constructor is declared. If any other name is specified, a compile-time error occurs.

The optional *formal-parameter-list* of an instance constructor is subject to the same rules as the *formal-parameter-list* of a method (§15.6). As the *this* modifier for parameters only applies to extension methods (§15.6.10), no parameter in a constructor's *formal-parameter-list* shall contain the *this* modifier. The formal parameter list defines the signature (§8.6) of an instance constructor and governs the process whereby overload resolution (§12.6.4) selects a particular instance constructor in an invocation.

Each of the types referenced in the *formal-parameter-list* of an instance constructor shall be at least as accessible as the constructor itself (§8.5.5).

The optional *constructor-initializer* specifies another instance constructor to invoke before executing the statements given in the *constructor-body* of this instance constructor. This is described further in §15.11.2.

When a constructor declaration includes an *extern* modifier, the constructor is said to be an *external constructor*. Because an external constructor declaration provides no actual implementation, its *constructor-body* consists of a semicolon. For all other constructors, the *constructor-body* consists of a *block*, which specifies the statements to initialize a new instance of the class. This corresponds exactly to the *block* of an instance method with a *void* return type (§15.6.11).
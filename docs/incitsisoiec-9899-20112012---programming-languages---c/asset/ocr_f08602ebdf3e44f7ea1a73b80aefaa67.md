list, the resulting type is the so-qualified atomic type.

If an attempt is to modify an object defined with a const-qualified type through use of Ivalue with non-const-qualified type, the behavior is undefined. If an attempt is to refer to an object defined by a volatile-qualified type through use of Ivalue with non-volatile-qualified type, the behavior is undefined.¹133)

An object that has volatile-qualified type may be modified in ways unknown to the implementation or have other unknown side effects. Therefore any expression referring to such an object shall be evaluated strictly according to the rules of the abstract machine, as described in 5.1.2.3. Furthermore, at every sequence point the value stored in the object shall agree with that prescribed by the abstract machine, except as modified by the unknown factors previously mentioned.¹134 What constitutes an access to an object that has volatile-qualified type is implementation-defined.

An object that is accessed through a restricted-qualified pointer has a special association with that pointer. This association, defined in 6.7.3.1 below, requires that all accesses to that object use, directly or indirectly, the value of that particular pointer.¹135 The intended use of the restrict qualifier (like the register storage class) is to promote optimization, and deleting all instances of the qualifier from all preprocessing units composing a conforming program does not change its meaning (i.e., observable behavior).

If the specification of an array type includes any type qualifiers, the element type is so-qualified, not the array type. If the specification of a function type includes any type qualifiers, the behavior is undefined.¹136)

For qualified types to be compatible, both shall have the identically qualified version of a compatible type; the order of type qualifiers within a list of specifiers or qualifiers does not affect the specified type.

EXAMPLE 1 An object declared

```
extern const volatile int real_time_clock;
```

> 133 This applies to those objects that behave as if they were defined with qualified types, even if they are never actually defined as objects in the program (such as an object at a memory-mapped input/output address).

> 134 A volatile declaration may be used to describe an object corresponding to a memory-mapped input/output port or an object accessed by an asynchronously interrupting function. Actions on objects shall not be "optimized out" by an implementation or reordered except as permitted by the rules for evaluating expressions.

> 135 For example, a statement that assigns a value by malloc to a single pointer establishes this association between the allocated object and the pointer.

> 136 Both of these can occur through the use of typedefs.
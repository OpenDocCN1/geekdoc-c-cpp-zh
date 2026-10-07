# ISO/IEC 9899:2011 (E)

# © ISO/IEC 2011 – All rights reserved

list, the resulting type is the so-qualified atomic type.

6 If an attempt is made to modify an object defined with a const-qualified type through use of an lvalue with non-const-qualified type, the behavior is undefined. If an attempt is made to refer to an object defined with a volatile-qualified type through use of an lvalue with non-volatile-qualified type, the behavior is undefined.¹133)

7 An object that has volatile-qualified type may be modified in ways unknown to the implementation or have other unknown side effects. Therefore any expression referring to such an object shall be evaluated strictly according the rules of the abstract machine, as described in 5.1.2.3. Furthermore, at every sequence point the last value stored in the object shall agree with that predicted by the abstract machine, except as modified by the unknown factors mentioned previously.¹134) What constitutes an access to an object with volatile-qualified type is implementation-defined.

8 An object that is accessed through a restricted-qualified pointer has a special association with that pointer. Association, defined in 6.7.3.1, requires that all accesses to such object, directly or indirectly, the value of that particular pointer.¹135) The intended use of the restrict qualifier (like the register storage class) is to promote optimization, and deleting all instances of the qualifier from all preprocessing units composing a functioning program does not change its meaning (i.e., observable behavior).

9 If the specification of an array type includes any qualifiers, the element type is so qualified, the array type. If the specification of a function type includes any qualifiers, the behavior is undefined.¹136)

10 For two qualified types to be compatible, both shall have the identically qualified version of a compatible type; the order of type qualifiers within a list of specifiers or qualifiers does not affect the specified type.

11 EXAMPLE 1 An object declared

```
extern const volatile real_time_clock;
```

> 133) This applies to objects that behave as if they were defined with qualified types, even if they are never actually declared as objects in the program (as an object at a memory-mapped input/output address).

> 134) A volatile declaration may be used to describe an object corresponding to a memory-mapped input/output port or an object accessed by an asynchronously interrupting function. Actions on objects declared shall not be “optimized” by an implementation or reordered as per the rules of evaluating expressions.

> 135) For example, a statement that assigns a value returned by malloc to a single pointer establishes this association between the allocated object and the pointer.

> 136) Both of these can occur through the use of typedefs.

122

Language

6.7.3
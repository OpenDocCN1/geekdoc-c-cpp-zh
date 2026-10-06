# ISO/IEC 14882:2017(E)

{: The last two operators are function (8.2.2) and subscribing (8.2.1). The operators new delete(), (), and are formed from more than one token. — end note }

+   * Both the unary and binary forms

+   * * can be overloaded.

+   * 3 The following operators cannot be overloaded:

+   * * : = ?

nor can the preprocessing symbols # and ## (Clause 19). instead they were invoked to evaluate the operators

4 Operator functions cannot be called directly; they can be explicitly called, however, using the operator-function-id as the implement (16.5.1—16.5.7) name of the function call syntax (8.2.2). [Example:

```
complex z = a.operator(b);
// complex z = a*b
void* p = operator new(size_t(n));
```

— end example

5 The allocation and deallocation functions, new operator, operator delete and operator delete(), are described completely in 6.7.4. The attributes and restrictions in the rest of this subclass do not apply unless explicitly stated in 6.7.4.

An operator either be a non-static member function or a non-member function that has least one parameter whose type is a class, a reference to a class, or a reference to an enumeration. It is not permitted to change the precedence, grouping, or number of operands. The meaning of operators =, (unary), &, and (comma,), defined for each type, can be changed for specific class and enumeration types by defining operator functions that implement these operators. Operator functions are inherited in the same manner as base functions.

7 The identifies identified operators applied to basic types (type, +==) where explicitly stated below. do not hold for operator functions. Some predefined operators, as =, require an operand to be a value when applied to basic types; this is not required by operator functions.

8 Operator functions cannot have default arguments (11.3.6), except as unary and binary operators, as operator functions cannot have more or fewer parameters than the number required for the corresponding operator, as described in the rest of this subclass.

* Operators not mentioned explicitly in subclaes 16.5.3 through 16.5.7 act as unary and binary operators obeying the rules of 16.5.1 and 16.5.2.

[over.unary]

# 10.5.1 Unary operators

1 A prefix operator shall be implemented by a non-static member function (12.2.1) or a non-member function with one parameter. For, any prefix operator, @x can be interpreted as either x.operator() or operator(x). If both forms of the operator function have been declared, the rules of 16.5.1.2 determine if, any interpretation is used. See 16.5.7 for an explanation of the unary operators ++ and --.

2 The unary and binary forms of the same operator are considered to have the same name. [ Note: Consequently

# 16.5.2 Binary operators

[over.binary]

1 A binary operator shall be implemented by either a non-static member function (12.2.1) or a non-member function with two parameters. Then, for any binary operator, @xy can be interpreted as either x.operator(y) or operator(x,y). If both forms of the operator function have been declared,

§ 16.5.2

©ISO/IEC 2017 - All rights reserved

335
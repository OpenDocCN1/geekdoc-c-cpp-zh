Types in Scheme include lists, symbols, atoms, and numbers. Predefined test functions include number? and symbol?. (Such test functions are called **predicates** and always end in a question mark.)

# Example 3

Ada is a strongly typed language, and all type errors cause compilation error messages. However, even in Ada, certain errors, like range errors in array subscripting, cannot be caught prior to execution, since the value of a subscript is not in general known until runtime. However, the Ada standard guarantees that all such errors will cause exceptions and, if these exceptions are not caught and handled by the program itself, program termination. Typically, such runtime type-checking errors result in the raising of the predefined exception Constraint_Error.

An essential part of type checking is **type inference**, where the types of expressions are inferred from the types of their subexpressions. Type-checking rules (that is, when constructs are type correct) and type inference rules are often intermingled. For example, an expression e1 + e2 might be declared type correct if e1 and e2 have the same type, and that type has a “+” operation (type checking), and the result type of the expression is the type of e1 and e2 (type inference). This is the rule in Ada, for example. In other languages this rule may be softened to include cases where the type of one subexpression is automatically convertible to the type of the other expression.

As another example of a type-checking rule, in a function call, the types of the actual parameters or arguments must match the types of the formal parameters (type checking), and the result type of the call is the result type of the function (type inference).

Type-checking and type inference rules have a close interaction with the type equivalence algorithm. For example, the C declaration

```
void p ( struct { int i; double r; } x ){\n...\n}
```

is an error under C’s type equivalence algorithm, since no actual parameter can have the type of the formal parameter x, and so a type mismatch will be declared on every call to p. As a result, a C compiler will usually issue a warning here (although, strictly speaking, this is legal C).¹³ Similar situations occur in Pascal and Ada.

The process of type inference and type checking in statically typed languages is aided by explicit declarations of the types of variables, functions, and other objects. For example, if x and y are variables, the correctness and type of the expression x + y is difficult to determine prior to execution unless the types of x and y have been explicitly stated in a declaration. However, explicit type declarations are not an absolute requirement for static typing: The languages ML and Haskell perform static type checking but do not require types to be declared. Instead, types are inferred from context using an inference mechanism that is more powerful than what we have described (it will be described in Section 8.8).

Type inference and correctness rules are often one of the most complex parts of the semantics of a language. Nonorthogonalities are hard to avoid in imperative languages such as C. In the remainder of this section, we will discuss major issues and problems in the rules of a type system.

> ¹³ This has been raised to the level of an error in C++.
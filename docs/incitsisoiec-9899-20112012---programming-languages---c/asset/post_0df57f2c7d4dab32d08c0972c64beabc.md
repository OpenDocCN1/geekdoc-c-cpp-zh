
## 6.5.1 Primary expressions

### Semantics

An identifier is a primary expression, provided it has been declared as designating an object (in which case it is an Ivalue) or a function (in which case it is a function designator).^{91}

A constant is a primary expression. Its type depends on its form and value, as detailed in 6.4.4.

A string literal is a primary expression. It is an Ivalue with type as detailed in 6.4.5.

A parenthesized expression is a primary expression. Its type and value are identical to those of the unparenthesized expression. It is an Ivalue, a function designator, or a void expression if the unparenthesized expression is, respectively, an Ivalue, a function designator, or a void expression.

A generic selection is a primary expression. Its type and value depend on the selected generic association, as detailed in the following subclause.

**Forward references:** declarations (6.7).

### 6.5.1.1 Generic selection

### Syntax

```
generic-selection: ( assignment-expression , generic-assoc-list )
generic-assoc-list:
gener-association
generic-assoc-list , generic-association
generic-association:
type-name : assignment-expression
default : assignment-expression
```

91) Thus, an undeclared identifier is a violation of the syntax.

### Constraints

A generic selection shall have no more than one default generic association. The type name in a generic association shall specify a complete object other than a variably modified type. No two generic associations in the same generic selection shall specify compatible types. The controlling expression of a generic selection shall have type compatible with at most one of the types named in its generic association list. If a generic selection has no default generic association, its controlling expression shall have type compatible with exactly one of the types named in its generic association list.

### Semantics

The controlling expression of generic selection is not evaluated. If a generic selection has a generic association with a type name that is compatible with the type of the controlling expression, then the result expression of the generic selection is the expression in that generic association. Otherwise, the result expression of the generic selection is the expression in the default generic association. None of the expressions from any other generic association of the generic selection is evaluated.

The type and value of generic selection are identical to those of its result expression. It is an lvalue, a function designator, or a void expression if its result expression is, respectively, an lvalue, a function designator, or a void expression.

EXAMPLE The cbrt type-generic macro _Generic(X), could be implemented as follows:

```
#define cbrt (X) _Generic(X) \\
long double: cbrtl, \\
default: cbrt, \\
float: cbrtf \\
) (X)
```

## 6.5.2 Postfix operators

### Syntax

```
postfix-expression:
primary-expression
postfix-expression [ argument-expression-listopt ]
postfix-expression ( argument-expression-listopt )
postfix-expression . identifier
postfix-expression -> identifier
postfix-expression ++
postfix-expression --
( type-name ) { initializer-list }
( type-name ) { initializer-list },
```

### 6.5.2.1 Array subscribing

One of the expressions shall have type "pointer to complete object type", the other expression shall have integer type, and the result has "type".

### Semantics

A postfix followed by an expression in square brackets [] is a subscribed designation of an element of an array object. The definition of the subscript operator [] is that E1 [E2] is identical to (* (E1) + (E2)). Because of the conversion rules that apply to the binary + operator, E1 is an array object (equivalently, a pointer to the initial element of an array) and E2 is an integer, E1 [E2] designates the E2-th element of E (counting from zero).

Successive subscript operators designate an element of a multidimensional array object. If E is an n-dimensional array (n≥2) with dimensions i×j...×k, then E (used as other than an lvalue) is converted to a pointer to an (n−1)-dimensional array with dimensions j×...×k. If the unary * operator is applied to this pointer explicitly, or implicitly a result of subscripting, the result is the referenced (n−1)-dimensional array, which itself is converted into a pointer if used as other than an lvalue. It follows from that these arrays are stored in row-major order (last subscript varies fastest).EXAMPLE Consider the array object defined by the declaration x is 3×5 array of ints; precisely, x is an array of element objects, each of which is an array. In the expression x[i], which is equivalent to ((x) + (i)), x is first converted to a pointer to the initial array of ints. Then i is adjusted according to the type of x, which multiplies i by the size of the object to which the pointer points, so x[i][j] yields an int.

Forward references: additive operators (6.5), address and indirection operators (6.5.3), array declarators (6.7).

## 6.5.2.2 Function calls

### Constraints

1 The expression that denotes the called object shall have type pointer to function returning void or returning a complete object

2 If the expression denotes the called function has a type that includes a prototype, the number of arguments shall agree with the number of parameters. Each argument shall have a type such that its value may be assigned to an object with the unqualified version of the type of its corresponding parameter.

### Semantics

3 A postfix expression followed by parentheses () containing a possibly empty, comma-separated list of expressions is a function call. The postfix expression denotes the called function. The list of expressions specifies the arguments to the function.

4 An argument may be an expression of any object type. In preparing for the call to a function, the arguments are evaluated, and each parameter is assigned the value of the argument.

5 If the expression denotes the called function has type pointer to returning an object type, the function call has the same type as that object, as specified in 6.8. Otherwise, the function call has type void.

6 If the expression denotes the called function has a type that does not include a prototype, the integer promotions are performed on each argument, and arguments that have type float are promoted to double. These are called default promotions. If the number of arguments does not equal the number of parameters, the behavior is undefined. If the function is defined with a type that includes a prototype, and either the prototype ends with ellipsis (...) or the types of the arguments after promotion are not compatible with the types of the parameters, the behavior is undefined. If the function is defined with a type that does not include a prototype, and the types of the arguments after promotion are not compatible with those of the parameters after promotion, the behavior is undefined, except for the following cases:

- one promoted type is a signed integer type, the other promoted type is the corresponding unsigned integer type, and the value is representable in both types

92) Most often, this is the result of converting an identifier that is a function demonstr.

93) A function may change the values of its parameters, but these changes cannot affect the values of the arguments. On the other hand, it is possible to pass a pointer to an object, and the function may change the value of the object pointed to. A parameter declared to have array or function type is adjusted to a pointer type as described in 6.9.1.

If the expression denotes the called function has a type that does include a prototype, the arguments are implicitly converted, as if by assignment, the types of the corresponding parameters, taking the type of each parameter to be the unqualified version of its declared type. The ellipsis notation in a function prototype declares argument type conversion to stop after the last declared parameter. The default argument promotions are performed on trailing arguments.

No other conversions are performed implicitly; in particular, the number and types of arguments are not compared with those of the parameters in a function definition that does not include a function prototype declarator.

If the function is defined with a type that is not compatible with the type (of the expression) pointed to by the expression that denotes the called function, the behavior is undefined.

There is a sequence point after the evaluations of the function designator and the actual arguments before the actual call. Every evaluation in the calling function (including other functions) that is not otherwise specifically sequenced before or after the execution of the body of the called function is indeterminately sequenced with respect to the execution of the called function.

Recursive function calls shall be permitted, both directly and indirectly through any chain of other functions.

EXAMPLE In the function

```
*pf(f[1()]) (f2(), f3() + f4())
```

the functions f1, f2, f3, and f4 may be called in any order. All side effects have to be completed before the function pointed to by pf[f[1]] is called.

Forward references: function declarators (including prototypes) (6.7.6.3), function definitions (6.9.1), the return statement (6.8.6.4), simple assignment (6.5.16.1).

## 6.5.2 Structure and union members

### Constraints

The first operand of the . operator shall have an atomic, qualified, or unqualified structure or type, and the second operand shall name a member of that type.

The first operand of the -> operator shall have type "pointer to atomic, qualified, or unqualified structure" or "pointer to atomic, qualified, or unqualified union", and the second operand shall name a member of the type pointed to.

⁴) In other words, function executions do not “interleave” with each other.

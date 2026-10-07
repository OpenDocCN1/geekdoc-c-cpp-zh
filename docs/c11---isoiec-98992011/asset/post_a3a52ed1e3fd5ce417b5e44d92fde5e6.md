
## 6.5.1 Primary expressions

### Syntax

- 1 primary-expression:
  identifier
  constant
  string-literal
  ( expression )
  generic-selection

### Semantics

- 2 An identifier is a primary expression, provided it has been declared as designating an object (in which case it is an lvalue) or a function (in which case it is a function designator).9)

- 3 A constant is a primary expression. Its type depends on its form and value, as detailed in 6.4.4.

- 4 A string is a primary expression. It is an lvalue with type as detailed in 6.4.5.

- 5 A parenthesized expression is a primary expression. Its type and value are identical to those of the unparenthesized expression. It is an lvalue, a function designator, or a void expression if the unparenthesized expression is, respectively, an lvalue, a function designator, or a void expression.

- 6 A generic selection is a primary expression. Its type and value depend on the selected generic association, as detailed in the following clause.

Forward references: declarations (6.7).

## 6.5.1.1 Generic selection

### Syntax

- 1 generic-selection:
  _Generic { assignment-expression , generic-assoc-list }
  generic-assoc-list:
  generic-association
  generic-assoc-list , generic-association
  generic-association:
  type-name : assignment-expression
  default : assignment-expression

> 9) Thus, an undeclared identifier is a violation of the syntax.

Constraints

A generic selection shall have no more than one default generic association. The type name in a generic association shall specify a complete object other than a variably modified type. No two generic associations in the same generic selection shall specify compatible types. The controlling expression of a generic selection shall have type compatible with at most one of the types named in its generic association list. If a generic selection has no default generic association, its controlling expression shall have type compatible with exactly one of the types named in its generic association.

### Semantics

The controlling expression of a generic selection is not evaluated. If a generic selection has a generic association with a type name that is compatible with the type of the controlling expression, then the result expression of the generic selection is the expression in that generic association. Otherwise, the result expression of the generic selection is the expression in the default generic association. None of the expressions from any other generic association of the generic selection is evaluated.

The type and value of a generic selection are identical to those of its result expression. It is an lvalue, a function descriptor, or a void expression if its result expression is, respectively, lvalue, a function descriptor, or a void expression.

- EXAMPLE The cbrt type-generic macro could be implemented as:

```
#define cbrt (X) _Generic(X, \
double: cbrtl, \
default: cbrt, \
float: cbrtf \
) (X)
```

## 6.5.2 Postfix operators

### Syntax

```
postfix-expression:
  primary-expression
  postfix-expression [ expression ]
  postfix-expression ( argument-expression-list_opt )
  postfix-expression . identifier
  postfix-expression -> identifier
  postfix-expression ++
  postfix-expression --
  ( type-name ) { initializer-list }
  ( type-name ) { initializer-list , }
```

- argument-expression-list:
  assignment-expression
  argument-expression-list , assignment-expression

## 6.5.2.1 Array subscribing

### Constraints

- One of the expressions shall have type "pointer to complete object type", the other expression shall have integer type, and the result has type "type".

### Semantics

- A postfix expression followed by square brackets [] is a subscribed designation of an array object. The definition of the subscript operator [] is that E1[E2] is identical to (* ((E1)+(E2))). Because of the conversion it applied to the binary +, if E1 is an array object (equivalently, a pointer to the initial element of an array object) and E2 is an integer, E1[E2] designates the E element of E1 (counting from zero).

- Successive subscript operators denote the element of a multidimensional array object. If E is an n-dimensional array (n ≥ 2) with dimensions j×...×k, then E (used as other than an lvalue) is converted to a pointer to an (n−1)-dimensional array with dimensions j×...×k. If the unary * operator is applied explicitly, or implicitly as a result of subscribing, the result is the referenced (n−1)-dimensional array, which itself is converted into a pointer if other than an lvalue. It follows that these arrays are stored in row-major order (last subscript varies fastest).

- EXAMPLE Consider the array object defined by the
int *x[3] [5];

Here x is a 3×5 array of ints; more precisely, x is an array of three elements, each of which is an array of five ints. In the expression x[i], which is equivalent to (* ((x)+(i))), is first converted to a pointer to the initial array and is then adjusted according to the type of x, which conceptually entails multiplying i by the size of the object to which the pointer points, namely an array of int objects. The results are added and applied to, so x[j] yields an int.

Forward references: additive operators (6.5.6), address and indirection operators (6.5.3.2), array declarators (6.7.6).

## 6.5.2.2 Function calls

### Constraints

- The expression that denotes the called function9) shall have type pointer to function returning void or returning a complete object type other than array type.

- If the expression that denotes the called function has a type that includes a prototype, the number of arguments shall agree with the number of parameters. Each argument shall have a type such that its value may be assigned to an object with the unqualified version of the type of its parameter.

### Semantics

- A postfix expression followed by parentheses () containing a possibly empty, comma-separated list of expressions is a function call. The postfix expression denotes the called function. The list of expressions specifies the arguments to the function.

- An argument may be an expression of any complete object type. In preparing for the call to a function, the arguments are evaluated, and each parameter is assigned the value of the corresponding argument9

- If the expression that denotes the called function has type pointer to returning an object type, the function call has the same type as that object, and has the value determined as specified in 8.6.6.4. Otherwise, the function call has type void.

- If the expression that denotes the called function has a type that does not include a prototype, the integer promotion performed on each argument, and arguments that have type float are promoted to double. These are called the default argument promotions. If the number of arguments does not equal the number of parameters, the behavior is undefined. If the function is defined with a type that includes a prototype, and either the prototype ends with an ellipsis ( , ... ) or the types of the arguments after promotion are not compatible with the types of the parameters, the behavior is undefined. If the function is defined with a type that does not include a prototype, and the types of the arguments after promotion are not compatible with those of the parameters after promotion, the behavior is undefined, except for the following cases:

- one promoted type is a signed integer type, the other promoted type is the corresponding unsigned integer type, and the value is representable in both types;

> 9 Most often, this is the result of converting an identifier that is a function designation.

> 10 A function may change the value of its parameters, but these changes cannot affect the value of the arguments. On the other hand, it is possible to pass a pointer to an object, and the function may change the value of the object pointed to. A parameter declared to have array or function type is adjusted to have a pointer as described in 6.9.1.

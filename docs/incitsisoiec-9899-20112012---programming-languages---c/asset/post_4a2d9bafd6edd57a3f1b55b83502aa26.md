
If an array of unknown size is initialized, its size is determined by the largest indexed element with an explicit initializer. The array type is completed at the end of its initializer list.

The evaluations of the initialization list expressions are indeterminately sequenced with respect to one another and thus the order in which any side effects occurs is unspecified.¹152)

EXAMPLE 1 Provided that <complex.h> has included, the declarations

```c
int i = 3.5;
double complex c = 5 + 3 * I;
```

define and initialize i with the value c and with the value 5.0 + i30.

EXAMPLE 2 The declaration

```c
int x[] = { 1, 3, 5 };
```

defines and initializes x as a one-dimensional array object that has three elements, as no size was specified and there are three initializers.

EXAMPLE 3 The declaration

```c
int y[4][3] = {
{ 1, 3, 5 },
{ 2, 4, 6 },
{ 3, 5, 7 },
};
```

is a definition with a fully bracketed initialization: 1, 3 and initialize the first row of y (the array object y[0]), namely y[0][0], y[0][1], and y[0][2]. Likewise the next two lines y[1] and y[2]. The initializer ends early, y[3] is initialized with zeros. Precisely the same effect could have been achieved

```c
int y[4][3] = {
{ 1, 3, 5, 2, 4, 6, 3, 5, 0 },
};
```

The initializer for y[0] does not begin with a left brace, so three elements from the list are used. Likewise the next three are taken successively for y[1] and y[2].

EXAMPLE 4 The declaration

```c
int z[4][3] = {
{ 1 }, { 2 }, { 3 }, { 4 },
};
```

initializes the first column of z as specified and initializes the rest with zeros.

EXAMPLE 5 The declaration

```c
struct { int a[3], b; } w[] = { 1 }, { 2 };
```

is a definition with an inconsistently bracketed initialization. It defines an array with two structures: w[0].a[0] is 1 and w[1].a[0] is 2; all the other elements are zero.

152) In particular, the evaluation order need not be the same as the order of subobject initialization.

EXAMPLE 6 The declaration

```c
short q[4][3][2] = {
 { 1 },
  { 2, 3 },
  { 4, 5, 6 }
};
```

contains an incomplete but consistently bracketed initialization. It defines a three-dimensional array object q[0][0][0] is 1, q[1][0][0] is 2, q[1][0][1] is 3, and 4, 5, and 6 initialize q[2][0][0]. q[2][0][1] is 1, and q[2][1][0] respectively: all the rest are zero. The initializer for q[0][0][0] does not begin with a left brace, so up to six items from the current list may be used. There is only one, so the values for the five elements are initialized with zero. Likewise, the initializers for q[1][0] and q[2][0] do not begin with a left brace, so each uses up to six items, initializing their respective two-dimensional subaggregates. If there had more than six items in any of the lists, a diagnostic message would have been issued.

```c
short q[4][3][2] = {
 1, 0, 0, 0, 0,
  2, 3, 0, 0, 0,
  4, 5, 6
}
```

or by:

```c
short q[4][3][2] = {
 { 1 },
 {
 { 2, 3 },
 {
 { 4, 5 },
 { 6 },
 };};
```

in a fully bracketed format.

Note that the fully bracketed and minimally bracketed forms of initialization are, in general, less likely to cause confusion.

EXAMPLE 7 One form of initialization that completes array types involves typedefed names. Given the declaration

```c
typedef int a[]; // OK - declared with block scope
```

the declaration

```c
A a = { 1, 2 }, b = { 3, 4, 5 };
```

is identical to

```c
int a[] = { 1, 2 }, b[] = { 3, 4, 5 };
```

due to the rules for incomplete types.

EXAMPLE 8 The declaration

```c
char s[] = "abc", t[3] = "abc";
```

defines “plain” char array objects s and t whose elements are initialized with character string literals. This declaration is identical to

```c
char s[] = { 'a', 'b', 'c', '\0' };
t[] = { 'a', 'b', 'c' };
```

The contents of the arrays are modifiable. On the other hand, the declaration

```c
char *p = "abc";
```

p with type "pointer to char" and initializes it to point to an object with type "array of char" with length 4 elements initialized with a character string literal. If an attempt is made to modify the contents of the array, behavior is undefined.

EXAMPLE 9 Arrays are initialized to correspond to the elements of an enumeration using designators:

```c
enum { member_one, member_two };
const char *nm[] = {
    [member_two] = "two",
    [member_one] = "one"
};
```

EXAMPLE 10 Structures are initialized to nonzero values depending on their order:

```c
div_t answer = { .quot = 2, .rem = -1 };
```

EXAMPLE 11 Designators can be used to provide explicit initialization when unbracketed lists might be misunderstood:

```c
struct { int a[3], b; } w[] = [0].a = {1}, [1].a = {2};
```

EXAMPLE 12 Space can be "allocated" from both ends of an array by a single designator:

```c
int a[MAX] = {
    1, 3, 5, 7, 9, [MAX] = 8, 6, 4, 2
};
```

In the above, if MAX is greater than ten, there will be zero-valued elements in the middle; if it is less than ten, some of the values provided by the first initializers will be overridden by the second.

EXAMPLE 13 Any member of a union can be initialized:

```c
union { /* ... */ } u = { .any_member = 42 };


Forward references: <stddef.h>.

## 6.7.10 Static assertions

### Syntax
```c
static_assert(constant-expression, string_literal);
```

### Constraints
The constant expression shall compare unequal to 0.

### Semantics
If the value of the constant expression compares to 0, the declaration has no effect. Otherwise, the constraint is violated and the implementation shall produce a diagnostic message that includes the text of the string literal, except that characters not in the basic character set are not required to appear in the message.

Forward references: (7.2).

## 6.8 Statements and blocks

### Syntax
```
statement:
- labeled-statement
- compound-statement
- expression-statement
- selection-statement
- iteration-statement
- jump-statement
```

### Semantics
A statement specifies an action to be performed. Except as indicated, statements are executed in sequence.

A block allows a set of declarations and statements to be grouped into one syntactic unit. The initializers of objects that have automatic storage duration, and the variable length declarators of ordinary identifiers with block scope, are evaluated and the values are stored in the objects (including storing an indeterminate value without an initializer) each time the declaration is reached in the order of execution, as if it were a statement, and within each declaration in the order that appear.

A full expression is an expression that is not part of another expression or of a declarator. Each of the following is a full expression:
- an initializer that is not part of a compound literal;
- the expression in an expression statement;
- the controlling expression of a selection statement (**if** or **switch**);
- the controlling expression of a **while** or **do** statement;
- each of the (optional) expressions of a **for** statement;
- the (optional) expression in a **return** statement. There is a sequence point between the evaluation of a full expression and the evaluation of the next expression to be evaluated.

**Forward references:** expression and null statements (6.8.3), selection statements (6.8.4), iteration statements (6.8.5), the **return** statement (6.8.6).

## 6.8.1 L statements

### Syntax
```
labeled-statement:
- identifier : statement
- case constant-expression : statement
- default : statement
```

### Constraints
A **case** or **default** label shall appear only in a **switch** statement. Further constraints on such labels are discussed under the **switch** statement. Label names shall be unique within a function.

### Semantics
Any statement may be preceded by a prefix that declares an identifier as a label name. Labels in themselves do not alter the flow of control, which continues unimpeded across them.

Forward references: the goto (6.8.6.1), the switch statement (6.8.4.2).

## 6.8.2 Compound statement

### Syntax
```
compound-statement:
  { block-item-list opt }

  block-item-list:
    block-item
    block-item-list block-item

  block-item:
    declaration
    statement
```

### Semantics
A compound statement is a block.

## 6.8.3 Expression and null statements

### Syntax
```
expression-statement:
  expression_opt ;
```

### Semantics
The expression in an expression statement is evaluated as a void expression for its side effects.^{153}

A null statement (consisting of just a semicolon) performs no operations.

EXAMPLE 1 If a function call is evaluated as an expression statement for its side effects only, the discarding of its value may be made explicit by converting the expression to a void expression by means of a cast:

```c
int p(int);
/* ... * */
(void)p(0);
```

> 153) Such assignments, and function calls which have side effects.


# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

## 6.9.1 Function definitions

## Syntax

```
function-definition:
declaration-specifiers declarator declaration-list_opt compound-statement
declaration-list:
declaration
declaration-list declaration
```

The identifier declared in a function definition (which is the name of the function) shall have a function type, as specified by the declarator portion of the function definition.^{162}

The return type of a function shall be void or a complete object type other than array type.

The storage-class specifier, if any, in the declaration specifications shall be either auto or static.

If the declaration includes a parameter type, the declaration of each parameter shall include an identifier, except for the special case of a parameter list consisting of a single parameter of type void, in which case there shall not be an identifier. No declaration list shall follow.

If the declaration includes an identifier list, each declaration in the declaration list shall have at least one declarator, and every identifier in the identifier list shall be declared. An identifier declared as a typedefed name shall not be redeclared as a parameter. The declarations in the declaration list shall contain no storage-class specifier other than register and no initializations.

> 162) The intent is that the type in a function definition cannot be inherited from a typedef:

```
typedef int F(void);               // type F is "function with no parameters
                                               returning int;
F f, g;                              // f and g both have compatible type with F
F ( /* ... */ )                     // WRONG: syntax/constraint error
F g ( /* ... */ )                   // WRONG: declaration g returns a function
int F(void) ( /* ... */ )           // RIGHT: F has type compatible with F
int g ( /* ... */ )                   // RIGHT: g has type compatible with F
F *e(void) ( /* ... */ )          // e returns a pointer to a function
int (*fp)(void);                     // same: parentheses
F *fp;                               // fp points to a function that has type F
```

## Semantics

7 The declarator in a function definition specifies the name of the function defined and the identifiers of its parameters. If the declarator includes a parameter type list, the list also specifies the types of all the parameters; such a declarator also serves as a function prototype for later calls to the same function in the same translation unit. If the declarator includes an identifier list,¹⁶³ the types of the parameters shall be declared in a following declarator list. In either case, the type of each parameter is adjusted in 6.7.6.3 for a parameter list; the resulting type shall be a complete object type.

8 If a function that accepts a variable number of arguments is defined without a parameter list that ends with the ellipsis notation, the behavior is undefined.

9 Each parameter has automatic storage duration; its identifier is an lvalue.¹¹⁶⁴ The layout of the storage for parameters is unspecified.

10 Entry to the function, the size expressions of each variably modified parameter are evaluated and the value of each argument expression is converted to the type of the corresponding parameter as if assignment. (Array expressions and function designators as arguments were converted to pointers before the call.)

11 After all parameters have been assigned, the compound statement that constitutes the body of the function definition is executed.

12 If the } that terminates a function is reached, and the value of the function call is used by the caller, the behavior is undefined.

13 EXAMPLE 1 In the following:

```
extern int max(int a, int b)
{
    return a > b ? a : b;
}
```

extern is the storage-class specifier and int is the type specifier; max(int a, b) is the function declarator;
{
    return a > b ? a : b;
}

is the function body. The following similar function definition uses the identifier-list form for the parameter declarations:

> ¹⁶³ See “future language directions” (6.11.7).

> ¹⁶⁴ A parameter identifier cannot be declared in the function body except in an enclosed block.

## 6.9.1 Language 157

```
extern int max(a, b)
int a, b;
{
    return a > b ? a : b;
}
```

Here int a, b; is the declaration list for the parameters. The difference between these two definitions is that the first acts as a prototype declaration that forces conversion of the arguments of subsequent calls to the function, whereas the second form does not.

- EXAMPLE 2 To pass one function to another, one might say

```
int f(void);
/* ... */
g(f);
```

The definition of g might read

```
void g(int *funcp)
{
    /* ... */
    (*funcp)(); /* or funcp(); ... */
}
```

or, equivalently,

```
void g(int func(void))
{
    /* ... */
    func(); /* or (*func)(); ... */
}
```

## 6.9.2 External object definitions

## Semantics

- If the declaration of an identifier for an object has file scope and an initializer, the declaration is an external definition for the identifier.

- A declaration of an identifier for an object has file scope without an initializer, and without a storage-class qualifier or with the storage-class qualifier static, constitutes a tentative definition. If a translation unit contains one or more tentative definitions for an identifier, and the translation unit contains no external definition for that identifier, the behavior is exactly as if the translation unit contains a file scope declaration of that identifier, with the composite type as of the end of the translation unit, with an initializer equal to 0.

- If the declaration of an identifier for an object is a tentative definition and has internal linkage, the declared type should not be an incomplete type.

## EXAMPLE 1

```
int i1 = 1;               // definition, external linkage
static int i2 = 2;     // definition, internal linkage
extern i3 = 3;      // definition, external linkage
int i4;                                // tentative definition, external linkage
static int i5;          // tentative definition, internal linkage

int i1;                 // valid tentative definition, refers to previous
int i2;                 // 6.2.2 renders undefined, linkage disagreement
int i3;                 // valid tentative definition, refers to previous
int i4;                 // valid tentative definition, refers to previous
int i5;                 // 6.2.2 renders undefined, linkage disagreement

extern i1;             // refers to previous, whose linkage is external
extern int i2;         // refers to previous, whose linkage is internal
extern int i3;         // refers to previous, whose linkage is external
extern int i4;         // refers to previous, whose linkage is external
extern int i5;         // refers to previous, whose linkage is internal
```

## EXAMPLE 2

If at the end of the translation unit containing the array i still has incomplete type, the implicit initializer causes it to have one element, which is set to zero on program startup.

```
int i1[];
```

## 6.10 Preprocessing directives

## Syntax

```
preprocessing-file:
  groupopt
group:
  group-part
  group group-part
group-part:
  if-section
  control-line
  text-line
  # non-directive
if-section:
  if-group elifgroupsopt else-groupopt endif-line
group:
  # if constant-expression new-line groupopt
  # ifdef identifier new-line groupopt
  # endif identifier new-line groupopt
elif-groups:
  elif-group
  elif-groups elif-group
elif-group:
  # elif constant-expression new-line groupopt
else-group:
  # else new-line groupopt
endif-line:
  # endif new-line
```

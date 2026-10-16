Early programming languages, such as Fortran 77 and the original version of C, did not require parameter type checking; most later languages require it. However, the relatively recent languages Perl, JavaScript, and PHP do not.

C and C++ require some special discussion in the matter of parameter type checking. In the original C, neither the number of parameters nor their types were checked. In C89, the formal parameters of functions can be defined in two ways. They can be defined as in the original C; that is, the names of the parameters are listed in parentheses and the type declarations for them follow, as in the following function:

```
double sin(x)
double x;
{ . . . }
```

Using this form avoids type checking, thereby allowing calls such as

```
double value;
int count;
. . .
value = sin(count);
```

to be legal, although they are never correct.

The alternative to the original C definition approach is called the prototype method, in which the formal parameter types are included in the list, as in

```
double sin(double x)
{ . . . }
```

If this version of sin is called with the same call, that is, with the following, it is also legal:

```
value = sin(count);
```

The type of the actual parameter (int) is checked against that of the formal parameter (double). Although they do not match, int is coercible to double (it is a widening coercion), so the conversion is done. If the conversion is not possible (for example, if the actual parameter had been an array) or if the number of parameters is wrong, then a semantics error is detected. So in C89, the user chooses whether parameters are to be type checked.

In C99 and C++, all functions must have their formal parameters in prototype form. However, type checking can be avoided for some of the parameters by replacing the last part of the parameter list with an ellipsis, as in

```
int printf(const char* format_string, . . .);
```

A call to printf must include at least one parameter, a pointer to a literal character string. Beyond that, anything (including nothing) is legal. The way printf determines whether there are additional parameters is by the presence
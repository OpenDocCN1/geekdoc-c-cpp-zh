If, in a parameter declaration, an identifier can be treated either as a typedef name or as a parameter name, it shall be taken as a typedef name.

12 If the function declarator is not part of a definition of that function, parameters may have incomplete type and may use the [* notation in their sequences of declarator specifiers to specify variable length arrays.

13 The storage-class specifier in the declaration specifiers for a parameter declaration, if present, is ignored unless the declared parameter is one of the members of the parameter type list for a function definition.

14 An identifier list declares only the identifiers of the parameters of the function. An empty list in a function declarator that is part of a definition of that function specifies that the function has no parameters. The empty list in a function declarator that is not part of a definition of that function specifies no information about the number or types of the parameters is supplied.¹⁴⁵

15 For two function types to be compatible, both shall specify compatible return types.¹⁴⁶ Moreover, the parameter type list, if both are present, shall agree in the number of parameters and in use of the ellipsis terminator; corresponding parameters shall have compatible types. If one type has a parameter type list and the other is specified by a function declarator that is not part of a function definition and contains an empty identifier list, the parameter list shall not have an ellipsis terminator and the type of each parameter shall be compatible with the type that results from the application of the default argument promotions. If one type has a parameter type list and the other type is specified by a function definition that contains a (possibly empty) identifier list, both shall agree in the number of parameters, and the type of each prototype parameter shall be compatible with the type that results from the application of the default argument promotions to the type of the corresponding identifier. In the determination of type compatibility and of composite type, each parameter declared with function or array type is taken as the adjusted type and each parameter declared with qualified type is taken as the unqualified version of its declared type.

16 EXAMPLE 1 The declaration

```
int f(void), *fip(), (*pfi);
```

declares a function f with no parameters returning an int, and a pointer pfi to a function with no parameter specification returning a pointer to an int. It is especially useful to compare the two. The binding of *fip is *(f()), so that the declaration suggests, and the same construction in an expression requires, the calling of a function fip, and then indirection through the pointer to yield an int. In the declarator (*pfi)(), the extra parentheses are necessary to indicate that indirection to a pointer yields a function

¹⁴⁵ See “future language directions” (6.11.6).

¹⁴⁶ If both function types are “old style”, parameter types are not compared.
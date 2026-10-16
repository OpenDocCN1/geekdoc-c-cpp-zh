>= & && || ++ -- ->* ,
-> [] () new new[] delete delete[]

The following operators cannot be defined by a user:

:: scope resolution (§6.3.4, §16.2.12)
. member selection (§8.2)
->* member selection through pointer to member (§20.6)

They take a name, rather than a value, as their second operand and provide the primary means of referring to members. Allowing them to be overloaded would lead to subtleties [Stroustrup,1994]. The named “operators” cannot be overloaded because they report fundamental facts about their operands:

sizeof size of object (§6.2.8)
alignof alignment of object (§6.2.9)
typedef type_info of an object (§22.5)

Finally, the ternary conditional expression operator cannot be overloaded (for no particularly fundamental reason):

?: conditional evaluation (§9.4.1)

In addition, user-defined literals (§19.2.6) are defined by using the operator"" notation. This is a kind of syntactic subterfuge because there is no operator called "". Similarly, operator T() defines a conversion to a type T (§18.4).

It is not possible to define new operator tokens, but you can use the function call notation when this set of operators is not adequate. For example, use pow(), not **. These restrictions may seem Draconian, but more flexible rules can easily lead to ambiguities. For example, defining an operator ** to mean exponentiation may seem an obvious and easy task, but think again. Should ** bind to the left (as in Fortran) or to the right (as in Algol)? Should the expression a**p be interpreted as a**(p) or as (a)**(p)? There are solutions to all such technical questions. However, it is most uncertain if applying subtle technical rules will lead to more readable and maintainable code. If in doubt, use a named function.

The name of an operator function is the keyword operator followed by the operator itself, for example, operator<<. An operator function is declared and can be called like any other function. A use of the operator is only a shorthand for an explicit call of the operator function. For example:

```
void f(complex a, complex b) {
complex c = a + b; // shorthand
complex d = a.operator+(b); // explicit call
}
```

Given the previous definition of complex, the two initializers are synonymous.

# 18.2.1 Binary and Unary Operators

A binary operator can be defined by either a nonstatic member function taking one
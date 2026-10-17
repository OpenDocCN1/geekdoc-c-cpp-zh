|  |  |
|---|---|
| Condition ? X : Y | Conditional operator (?). If Condition is true then it returns value of X otherwise returns value of Y. |
| , | Comma operator causes a sequence of operations to be performed. The value of the entire comma expression is the value of the last expression of the comma-separated list. |
| . (dot) and -> (arrow) | Member operators are used to reference individual members of classes, structures, and unions. |
| Cast | Casting operators convert one data type to another. For example, int(2.2000) would return 2. |
| & | Pointer operator ‘&’ returns the address of a variable. For example &a; will give actual address of the variable. |
| * | Pointer operator * is pointer to a variable. For example *var; will pointer to a variable var. |

# Operators Precedence in C++

Operator precedence determines the grouping of terms in an expression. This affects how an expression is evaluated. Certain operators have higher precedence than others; for example, the multiplication operator has higher precedence than the addition operator:

For example x = 7 + 3 * 2; here, x is assigned 13, not 20 because operator * has higher precedence than +, so it first gets multiplied with 3*2 and then adds into 7.

Here, operators with the highest precedence appear at the top of the table, those with the lowest appear at the bottom. Within an expression, higher precedence operators will be evaluated first.

| Category | Operator | Associativity |
|---|---|---|
| Postfix | () [] -> . ++ -- | Left to right |
| Unary | + - ! ~ ++ -- (type)* & sizeof | Right to left |
| Multiplicative | * / % | Left to right |
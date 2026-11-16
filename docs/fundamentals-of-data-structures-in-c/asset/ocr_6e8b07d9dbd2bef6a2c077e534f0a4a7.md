# 1.7.9 Special Operators

Some of the special operators used in C are listed below. These operators are referred as separators or punctuators.

| Symbol | Name | Meaning |
| :--- | :--- | :--- |
| & | Ampersand | Also referred as **address operator** usually precedes the identifier name, which indicates the memory location (address) of the identifier. |
| * | Asterisk | Also referred as an **indirection operator** and it is an unary operator, which usually precedes the identifier name, which indicates the creation of a pointer operator. |
| {} | Braces | The opening and closing braces indicate the start and end of a compound statement or a function. A semicolon is not necessary after the closing brace of the statement, except in case of structure declaration. |
| [] | Brackets | Also referred as **array subscript operator** is used to indicate single and multi dimensional array subscripts. |
| : | Colon | Used in labels. |
| , | Comma | Used to link the related expressions together. Comma used expressions are linked from left to right and the value of the right most expression is the value of the combined expression. The comma operator has the lowest precedence of all operators. For example in the expression, sum = (x = 5, y = 3, x + y) ; The result will be sum = 8. The comma operator is also used to seperate variables during declaration. For example, int a, b, c ; |
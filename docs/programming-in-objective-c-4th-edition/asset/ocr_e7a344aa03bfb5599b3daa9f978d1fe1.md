# Program 6.9. Output

Type in your expression.
178.99 - 326.8
-147.81

After the expression has been read in, the value of operator is successively compared against the values specified by each case. When a match is found, the statements contained inside the case are executed. The break statement then sends execution out of the switch statement, where execution of the program is completed. If none of the cases matches the value of operator, the default case, which displays "Unknown operator.", is executed.

The break statement in the default case is actually unnecessary in the preceding program because no statements follow this case inside the switch. Nevertheless, it is a good programming habit to remember to include the break at the end of every case.

When writing a switch statement, be in mind that no two case values can be the same. However, you can associate more than one case value with a particular set of program statements. This is done simply by listing the multiple case values (with the keyword case before the value and a colon after each case) before the common statements that are to be executed. As an example, in the switch statement that follows, the multiply:method is executed if operator is equal to an asterisk or to the lowercase letter x:

```
switch ( operator )
{
    ...
    case '*':
    case 'x':
        deskCalc multiply: value2];
```
loops involves when the controlling Boolean expression is checked. When a while statement is executed, the Boolean expression is checked before the loop body is executed. If the Boolean expression evaluates to false, then the body is not executed at all. With a do-while statement, the body of the loop is executed first and the Boolean expression is checked after the loop body is executed. Thus, the do-while statement always executes the loop body at least once. After this start-up, the while loop and the do-while loop behave very much the same. After each iteration of the loop body, the Boolean expression is again checked; if it is true, then the loop is iterated again. If it has changed from true to false, then the loop statement ends.

# DISPLAY 3.9 Syntax of the while Statement and do-while Statement

A while Statement with a Single Statement Body

while (Boolean_Expression)
    Statement  ← Body

A while Statement with a Multistatement Body

while (Boolean_Expression)
{
    Statement_1
    Statement_2
    .
    .
    Statement_Last
}  Body

A do-while Statement with a Single Statement Body

do
    Statement  ← Body
while (Boolean_Expression);

A do-while Statement with a Multistatement Body

do
{
    Statement_1
    Statement_2
    .
    .
    Statement_Last
} while (Boolean_Expression);  Body
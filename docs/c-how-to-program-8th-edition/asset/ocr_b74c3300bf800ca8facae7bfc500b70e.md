Just as a block can be placed anywhere a single statement can be placed, it’s also possible to have no statement at all, which is called a **null statement** or an **empty statement**. The null statement is represented by placing a semicolon (`;`) where a statement would normally be.

> **Common Programming Error 4.2**
> 
> *Placing a semicolon after the condition in an if statement leads to a logic error in single-selection if statements and a syntax error in double-selection if...else statements (when the if part contains an actual body statement).*

![](bbox=[0.159, 0.192, 0.219, 0.237])

# 4.7 while Repetition Statement

A **repetition statement** specifies that a program should repeat an action while some condition remains true. The pseudocode statement

```
While there are more items on my shopping list
    Purchase next item and cross it off my list
```

describes the repetition that occurs during a shopping trip. The condition, “there are more items on my shopping list” is either true or false. If it’s true, then the action, “Purchase next item and cross it off my list” is performed. This action will be performed repeatedly while the condition remains true. The statement contained in the While repetition statement constitutes the body of the While, which can be a single statement or a block. Eventually, the condition will become false (when the last item on the shopping list has been purchased and crossed off the list). At this point, the repetition terminates, and the first pseudocode statement after the repetition statement executes.

As an example of C++’s while repetition statement, consider a program segment designed to find the first power of 3 larger than 100. Suppose the integer variable product has been initialized to 3. When the following while repetition statement finishes executing, product contains the result:

```
int product = 3;

while ( product <= 100 )
    product = 3 * product;
```

When the while statement begins execution, product’s value is 3. Each repetition multiplies product by 3, so product takes on the values 9, 27, 81 and 243 successively. When product becomes 243, the while statement condition—product <= 100—becomes false. This terminates the repetition, so the final value of product is 243. At this point, program execution continues with the next statement after the while statement.

> **Common Programming Error 4.3**
> 
> *Not providing, in the body of a while statement, an action that eventually causes the condition in the while to become false normally results in a logic error called an infinite loop, in which the repetition statement never terminates. This can make a program appear to “hang” or “freeze” if the loop body does not contain statements that interact with the user.*

![](bbox=[0.159, 0.799, 0.219, 0.845])

The UML activity diagram of Fig. 4.6 illustrates the flow of control that corresponds to the preceding while statement. Once again, the symbols in the diagram (besides the initial state, transition arrows, a final state and three notes) represent an action state and a
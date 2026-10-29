executed. So before the first check of the expression, initial values for the tested expression’s variables must be assigned, and before the expression is reevaluated, there must be one or more statements that alter these values.

The for statement also provides a single place for all expression-altering statements: the altering list, the last item inside for’s parentheses. All items in this list are executed by the for statement at the end of the loop, just before the expression is reevaluated.

Figure 5.5 illustrates the internal workings of a for loop. As shown, when the for loop is completed, control is transferred to the first executable statement following the loop.

![](bbox=[0.18, 0.46, 0.88, 0.92])

Figure 5.5 The for statement's flow of control
After the statement in Line 4 executes, the loop condition in Line 2 is reevaluated. Because current is not NULL, the loop condition evaluates to true, so the statements in Lines 3 and 4 execute (see Figure 17-21).

![](bbox=[0.187, 0.193, 1.0, 0.396])

**FIGURE 17-21** List and stack after the statements `stack.push(current);` and `current = current->link;` execute

After the statement in Line 4 executes, the loop condition in Line 2 is evaluated again. Because current is not NULL, the loop condition evaluates to true, so the statements in Lines 3 and 4 execute (see Figure 17-22).

![](bbox=[0.189, 0.591, 1.0, 0.829])

**FIGURE 17-22** List and stack after the statements `stack.push(current);` and `current = current->link;` execute

After the statement in Line 4 executes, the loop condition in Line 2 is evaluated again. Because current is NULL, the loop condition evaluates to false, and the while loop in
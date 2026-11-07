After the statement in Line 4 executes, the loop condition in Line 2 is re-evaluated. Because `current` is not NULL, the loop condition evaluates to true, so the statements in Lines 3 and 4 execute. (See Figure 19-21.)

![](bbox=[0.182, 0.183, 0.912, 0.402])

**FIGURE 19-21** List and stack after the statements `stack.push(current);` and `current = current->link;` execute

After the statement in Line 4 executes, the loop condition, in Line 2, is evaluated again. Because `current` is not NULL, the loop condition evaluates to true, so the statements in Lines 3 and 4 execute. (See Figure 19-22.)

![](bbox=[0.184, 0.553, 0.912, 0.836])

**FIGURE 19-22** List and stack after the statements `stack.push(current);` and `current = current->link;` execute

After the statement in Line 4 executes, the loop condition in Line 2 is evaluated again. Because `current` is NULL, the loop condition evaluates to false, and the while loop in
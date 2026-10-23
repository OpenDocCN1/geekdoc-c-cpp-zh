# 5.6.1 Parenthesis matching

To compute the complex expression, we enclose it in parenthesis to ensure that the expression is computed in correct order. It is equally important that correct number of parenthesis are used in right order. We have already learned in mathematics that the order of closing the bracket is governed by the order of opening brackets. We close the bracket that is opened last. It is illustrated with the help of following example.

```
2+ [4.9+1-{23*5-(54+12) +90/15} +98]
```

In the aforementioned example, the bracket ‘(‘ is opened at the end, accordingly it has to be closed first. Similarly, same rule is applicable for the other brackets. It is equally significant that the bracket opened is also closed. Otherwise, this will also leads to the parenthesis mismatch. In brief, followings points are to be examined for correctness of parenthesis:

+   - Brackets are opened and closed in the correct sequence.
+   - Numbers of open brackets have the correspondingly closing brackets.
+   - Closing bracket should not be more that the brackets opened.

To accomplish the above objectives, stack is extremely useful. To evaluate any expression, we consider that the expression is made of operand and operator. Symbols ‘+’, ‘-’, ‘*’ etc. are known as operator. We scan the given expression, character by character; stack pushes the opening brackets. Once it encounters the closing bracket, it pops an item from the stack. The bracket that is received from the pop operation should be corresponding to the closing bracket. If these criteria are fulfilled, then it moves forward with other elements. In case of non-match, program terminates at this point itself and flashes the suitable message related to mismatch. To implement this task, we have used two functions based on brackets.

+   - Bracket checking.
+   - Expression evaluation

In the bracket checking program, each brackets are assigned priority. In the program, due care was taken to ensure that the brackets with the higher priority is not replacing the bracket with the lower priority. In other terms ‘(‘should not come before ‘[‘or ‘{‘. Various possibilities that may take place with the parenthesis mismatching have been illustrated in the figure 5.4.

In our program, we would scan character by character from the beginning of the expression. Upon encountering the opening bracket, we will push it into the stack. Further, we would continue to scan the expression. Upon encountering the closing bracket, the top element of the stack will be popped by using the pop function. The item popped will be checked with the closing brackets, if it is correct matching then we will proceed further otherwise we terminate here itself and the error message will be flashed to the user.

To meet the case of extra opening bracket(s), if there is no element in the expression but stack is empty, this will imply that there are extra brackets in the expression. Similarly, if the closing bracket is encountered and the stack is empty, it is the case of extra closing brackets. All these cases have been considered in the following figure 5.4
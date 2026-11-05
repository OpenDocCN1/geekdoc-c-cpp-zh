+   - Definitely assigned. This indicates that on all possible control flows to this point, v has been assigned a value.
+   - Not definitely assigned. For the state of a variable at the end of an expression of type bool, the state of a variable that isn't definitely assigned might (but doesn't necessarily) fall into one of the following sub-states:
+     - Definitely assigned after true expression. This state indicates that v is definitely assigned if the Boolean expression evaluated as true, but is not necessarily assigned if the Boolean expression evaluated as false.
+     - Definitely assigned after false expression. This state indicates that v is definitely assigned if the Boolean expression evaluated as false, but is not necessarily assigned if the Boolean expression evaluated as true.

The following rules govern how the state of a variable v is determined at each location.

# 9.4.4.2 General rules for statements

+   - v is not definitely assigned at the beginning of a function member body.
+   - The definite assignment state of v at the beginning of any other statement is determined by checking the definite assignment state of v on all control flow transfers that target the beginning of that statement. If (and only if) v is definitely assigned on all such control flow transfers, then v is definitely assigned at the beginning of the statement. The set of possible control flow transfers is determined in the same way as for checking statement reachability (§12.2).
+   - The definite assignment state of v at the end point of a block, checked, unchecked, if, while, do, for, foreach, lock, using, or switch statement is determined by checking the definite assignment state of v on all control flow transfers that target the end point of that statement. If v is definitely assigned on all such control flow transfers, then v is definitely assigned at the end point of the statement. Otherwise, v is not definitely assigned at the end point of the statement. The set of possible control flow transfers is determined in the same way as for checking statement reachability (§12.2).

*Note:* Because there are no control paths to an unreachable statement, v is definitely assigned at the beginning of any unreachable statement. end note

# 9.4.4.3 Block statements, checked, and unchecked statements

The definite assignment state of v on the control transfer to the first statement of the statement list in the block (or to the end point of the block, if the statement list is empty) is the same as the definite assignment statement of v before the block, checked, or unchecked statement.

# 9.4.4.4 Expression statements

For an expression statement stmt that consists of the expression expr:

+   - v has the same definite assignment state at the beginning of expr as at the beginning of stmt.
+   - If v if definitely assigned at the end of expr, it is definitely assigned at the end point of stmt; otherwise, it is not definitely assigned at the end point of stmt.

# 9.4.4.5 Declaration statements

+   - If stmt is a declaration statement without initializers, then v has the same definite assignment state at the end point of stmt as at the beginning of stmt.
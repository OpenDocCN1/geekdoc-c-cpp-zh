However, because n is 0, execution of the function reaches the anchor case, stopping the recursion, and the function returns the value 1. The sequence of recursive calls from an initial call to the anchor case is sometimes referred to as the winding phase of the recursion, because it is like winding the spring of a wind-up clock until it is fully wound.

Once the anchor case has been reached, backtracking that actually performs the computation begins. The run-time stack is popped, and control returns to the function call whose activation record is now on top, (i.e., power(3.0, 1)) where it finishes evaluating the expression power(3.0, 0) * 3.0, producing 1.0 * 3.0:

![](bbox=[0.11, 0.345, 0.82, 0.43])

Because that marks the end of that function execution, the run-time stack is popped, and control returns to the function call whose activation record is exposed (i.e., power(3.0, 2)) where the expression power(3.0, 1) * 3.0 can now be evaluated to 3.0 * 3.0:

![](bbox=[0.21, 0.56, 0.75, 0.645])

That function call is complete, so the run-time stack is again popped, and control returns to the function whose activation record is exposed (i.e., power(3.0, 3)) and resumes evaluation of the expression power(3.0, 2) * 3.0, giving 9.0 * 3.0:

![](bbox=[0.29, 0.775, 0.65, 0.86])

Because execution has reached the end of that function call, the run-time stack is popped, control returns to the function whose activation record is uncovered (i.e., power(3.0, 4)), and the expression power(3.0, 3) * 3.0 evaluates to 27 * 3.0:

![](bbox=[0.35, 0.99, 0.62, 1.08])

The result (81.0) is the return value of the original function call power(3.0, 4).

This phase in which values are returned from the anchor case back through each of the previous calls is sometimes referred to as the unwinding phase of the recursion, because like a wind-up clock performing its task as its spring unwinds, a recursive function performs its task by unwinding the recursive calls stacked up in its winding phase.
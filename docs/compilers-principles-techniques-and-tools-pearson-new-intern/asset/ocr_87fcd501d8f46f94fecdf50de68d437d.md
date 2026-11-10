# 7.2. STACK ALLOCATION OF SPACE

**Example 7.4:** Figure 7.6 shows snapshots of the run-time stack as control flows through the activation tree of Fig. 7.4. Dashed lines in the partial trees go to activations that have ended. Since array *a* is global, space is allocated for it before execution begins with an activation of procedure *main*, as shown in Fig. 7.6(a).

![](bbox=[0.281, 0.277, 0.759, 0.583])

Figure 7.6: Downward-growing stack of activation records

When control reaches the first call in the body of *main*, procedure *r* is activated, and its activation record is pushed onto the stack (Fig. 7.6(b)). The activation record for *r* contains space for local variable *i*. Recall that the top of stack is at the bottom of diagrams. When control returns from this activation, its record is popped, leaving just the record for *main* on the stack.

Control then reaches the call to *q* (quicksort) with actual parameters 1 and 9, and an activation record for this call is placed on the top of the stack, as in Fig. 7.6(c). The activation record for *q* contains space for the parameters *m* and *n* and the local variable *i*, following the general layout in Fig. 7.5. Notice that space once used by the call of *r* is reused on the stack. No trace of data local to *r* will be available to *q*(1, 9). When *q*(1, 9) returns, the stack again has only the activation record for *main*.

Several activations occur between the last two snapshots in Fig. 7.6. A recursive call to *q*(1, 3) was made. Activations *p*(1, 3) and *q*(1, 0) have begun and ended during the lifetime of *q*(1, 3), leaving the activation record for *q*(1, 3)
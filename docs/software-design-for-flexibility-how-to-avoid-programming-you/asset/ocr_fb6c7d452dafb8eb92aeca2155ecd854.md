programmer explicit control over time. A computation can be captured and suspended at one moment it restored and continued at any future time. This makes it possible to write coroutines (cooperative multitasking), and with the addition of a timer interrupt mechanism we get timesharing (preemptive multitasking). On the occasions that you may need to deal explicitly with continuations, Scheme lets you do so by creating an explicit procedure that is the current continuation. But before we can take charge of this power we need a deeper understanding of continuations.

A continuation is a captured control state of a computation.27 If a continuation is invoked, the computation continues represented by the continuation. A continuation may represent the act of returning a value of a subexpression to the evaluation of the enclosing expression. The continuation is then a procedure that when invoked returns its argument to the evaluation of the enclosing expression as the value of the subexpression. A continuation can be invoked multiple times, allowing a computation to be resumed at a particular point with different values returned by the continuation. We will see an shortly.

Scheme provides call-with-current-continuation (abbreviated call/cc), which gives access to the continuations that under expression structure. The argument to call/cc is a procedure that gets the continuation of the call/cc expression as its argument. Again: a continuation is a first-class procedure that takes one argument—the value to be returned when the continuation is called.28 Here is a simple example:

```
(set! foo)
(+ 1
 (call/cc
 (lambda (k)
 ;; k is the continuation
 ;; of the call/cc expression.
 ;; so if we call k with 6
 ;; then foo will get the value 11
 (k (* 2 3)))
 (/ 8 2)))
```
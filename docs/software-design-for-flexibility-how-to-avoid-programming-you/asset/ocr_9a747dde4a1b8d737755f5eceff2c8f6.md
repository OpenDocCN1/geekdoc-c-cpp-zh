more powerful than that: they can be reentered once invoked. The following example illustrates the idea:30

```
(define the-continuation #f)
(define (test)
let ((i 0))
;; The argument to call/cc assigns the
;; continuation produced by call/cc to the
;; global variable the-continuation.
(call/cc (lambda (k) (set! the-continuation k))
;; When the-continuation is called, execution
;; resumes here.
(set! i (+ i 1))
i))
```

The behavior is perhaps surprising. The procedure test creates a local variable i initialized to 0. It creates a continuation representing the control state of returning from the call/cc expression in the body of the let expression and stores that state in the global variable the-continuation. It increments i and returns i's new value: 1.

```
(test)
l
```

When the-continuation is called, the call/cc returns to the body of the let expression. Execution proceeds to increment i and return its new value. The continuation can be reused to increment i again and return its new value.

```
(the-continuation 'OK)
2
```

```
(the-continuation 'OK)
3
```

(The argument OK is the value of the call/cc; it is ignored by the let body.)
We save the continuation in another-continuation, so we can make a new one to be stored in the-continuation by
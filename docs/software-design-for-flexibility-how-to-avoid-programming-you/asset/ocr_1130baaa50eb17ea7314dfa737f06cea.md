out of data items, it fails to match. This is the key to the backtracking search that is needed when there are segment variables.

```
(define (match:segment variable)
(define (match-segment data dictionary succeed)
(and (list? data)
  (let ((binding (match:lookup variable dictionary))
    (if binding
      (match:segment-equal?
        data
        (match:binding-value binding)
        (lambda (n) (succeed (length dictionary))))
      (let ((n (length data))
        (let lp ((i 0))
          (and ( succeed (match:extend-dict
            variable
            (list-head data i)
            dictionary)
            i))
          (lp (+ i 1)))))))))))
segment-match
```

# For example:

```
((match:segment '?? a))
'(z z) (match:new-dict) result-receiver)
(success ((a () ??)) 0
```

Of course, a zero-length segment is okay.
If we want to see all of the possible matches, we change the result receiver to return #f after printing the successful result. This causes the matcher procedure to come up with an alternative value, possible.

```
(define (print-all-results dict n-eaten)
(pp '(success ,(match:bindings dict) ,n-eaten))
;; returning #f we force backtracking.
#f)
```

```
((match:segment '?? a))
'(z z) (match:new-dict) print-all-results)
(success ((a () ??)) 0)
(success ((a (z) ??)) 1)
(success ((a (z z) ??)) 2)
```
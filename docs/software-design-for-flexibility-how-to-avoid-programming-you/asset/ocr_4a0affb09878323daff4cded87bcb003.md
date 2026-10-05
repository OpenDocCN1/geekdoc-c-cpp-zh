(gmatch:seq2 matcher (gmatch:* matcher)))

The remaining special path patterns are and and or, each of which contains a number of subpath patterns. An and element must match all of the subpath patterns starting at the current node. An or element must match at least one of the subpath patterns starting at the current node.

```
(define (gmatch:compile- elt-lists)
(gmatch:and map gmatch:compile-path-elts elt-lists))
```

```
(define (gmatch:compile-or elt-lists)
(gmatch:or map gmatch:compile-path-elts elt-lists))
```

# The procedures and or are where the real work happens:

```
(define (gmatch:and matchers)
(lambda (object dict succeed)
(if (null? matchers)
(succeed object dict)
(let loop ((match matchers) (dict dict))
((car matches) object dict)
(if (null? (cdr matchers))
succeed
(lambda object* dict*)
(loop (cdr matchers) dict*))))))
```

```
(define (gmatch:or matchers)
(lambda (object dict succeed)
(let loop ((matches matchers))
(if (pair? matchers)
(or ((car matchers) object dict succeed)
(loop (cdr matchers))))
#f)))
```

The procedure compile-var compiles a pattern variable. It is called from compile-path and compile-target, and has four mutually exclusive cases to handle variables with or without the optimal name and predicate:

```
(define (gmatch:compile-var var)
(cond ((match-list? var gmatch:var-type?)
(gmatch:var-matcher (car var) #f #f))
((match-list? var gmatch:var-type? symbol)?)
(gmatch:var-matcher (car var) (cadr var) #f)))
```
```
(term (car terms)) rest2 (cdr terms))
(cond ((and (match:element-var? term)
      (match:vars-equal? var term))
      (succeed dict fail rest1 rest2))
  (match:has-binding? var dict)
  ((unify:dispatch
    (cons (match:get-value var dict) rest1
    terms))
    (succeed dict))
  else
  (let ((dict* (do-substitute var term dict))
    (if dict*
        (succeed dict* fail rest1 rest2)
        (fail)))))
```

In-substitute we first use the old dictionary to clean the incoming term by replacing any previously eliminated variables with their values. Then we check if there are any restrictions on what objects may match. Finally we check for any occurrences of var in the cleaned term (term*). If the cleaned term contains a reference to var, the match cannot proceed.8 If our match passes all tests, we make a new dictionary that includes the new binding of var to the cleaned term. The binding values in the new dictionary must also be cleaned of references to var.

```
(define (do-substitute var term dict)
(let ((term* (match:dict-substitution dict term))
(and (match:satisfies-restriction? var term*))
  (or (and (match:var? term*)
      (match:vars-equal? var term*))
  (not (match:occurs-in? var term*))
  (match:extend-dict var term*))
(match:map-dict-values
(match:single-substitution var term*)))
dict)))))
```

Now that we know how to handle variables we have to install this handler in our generic dispatcher procedure. The only subtlety here is that the variable to be eliminated may appear in either term list. We guarantee that the term list containing the variable is the first argument to maybe-substitute.
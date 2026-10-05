```
(lambda (dict))
(and dict)
  (let ((subst match:dict-substitution dict))
    (let ((p1* (subst p1)) (p2* (subst p2))
      (if not (equal? p1* p2))
        (error "Bad dictionary")
        (pp p1*))))
  (pp p1*))
```

```
a b b (?? w) b b c
a a b b (?? w) b b c
a a b b (?? w) b b c (a b b b b b b c)
a a b b b b b c
a a b b (?? w) b b c (a b b b b b b c)
a a b b (?? y) b b c (a b b b b b b c)
#f
```

So we see that “solution” is a valid solution to the problem of finding values for the variables when substituted back into the given patterns the patterns the same. In this case of five are the most general unifiers, and they are unique up to renaming of the variables. The other four are not as general as possible. By unification is supposed to produce the most general common substitution instance of the two input patterns, up to renaming of variables. With segments, this very useful pattern matcher is not really a unifier.

Actually the problem is a bit worse. There are perfectly good matches that are not found by this program. Here is an example:

```
;;; A missing match!
(unify:internal '((?? x) 3) (?? x))
  '((4 ??)) (4 5))
  (match:new-dict)
  (lambda (dict))
    (pp match:bindings dict))
  #f)
```

```
#f
```

But expressions do match, with the following bindings:

```
((x (4 5) ??) (y (5 3))))
```

How sad! But there is a moral to this story. Using generic procedures, we can make possibly problematic extensions to a correct algorithm without undermining its correctness for uses of the
# Exercise 5.4: Your turn

Invent a fun, interesting construct that can easily be implemented using generic eval/apply but would be rather painful without that kind of generic support.

# Exercise 5.5: Interoperation with the underlying system

As pointed out on page 238, evaluating the expression

```
eval> (map (lambda (x) (* x x)) '(1 2 3)
```

in our interpreter does not work if the map in this expression refers to the map procedure from the underlying Scheme system.
However, if we redefine map for our interpreter it works:

```
eval> (define map f l)
      (if null? l)
        '
        (cons f (car l)) (map f (cdr l))))
map
eval> (map (lambda (x) (* x x)) '(1 2 3))
(1 4 9)
```

Why does it not work to use the underlying procedures that take procedural arguments, such as map? Explain. Outline a strategy to fix the problem and implement your solution. Note: This is subtle to get right, so don't spend infinite time trying to make it perfectly.

# Exercise 5.6: Different quotation

There have interesting languages with very different evaluation and quotation rules. For example, in MDL (see Wikipedia [91]) a
```
(define make-graph-node name)
(let ((edges '()))
  (define (get-name) name)
  (define (all-edges) (list-copy edges))
  (define (%find-edge label)
    (find (lambda edge)
      (eqv? label (edge 'get-label))
    edges))
  (define (has-edge? label)
    (and (%find-edge label #t)) ; boolean value
  (define (get-edge label)
    (let ((edge (%find-edge label)))
      (if not edge)
        (error "No edge with this label:" label)
      edge))
  (define (edge-value label)
    ((get-label) 'get-value))
  (define (connect! label value)
    (if (has-edge? label)
      (error "Two edges with same label:" label))
    (set! edges (cons make-graph-edge label value) edges))
  (define (maybe-connect! value)
    (if (not (default-object? value))
      (connect! label value))))
  (bundle graph-node? get-name all-edges has-edge?
    (cons make-graph-edge label value) connect! edge-value maybe-connect!)) )
```

The argument to make-graph-node is the name of the new node; this is shown when printing a node object. The first argument to the bundle macro is a predicate that the generated bundle will satisfy. In this case, it is defined as

```
(define graph-node? (make-bundle-predicate 'graph-node))
```

We will not show the definitions of other bundle predicates since they are similar.

Edges are also represented as bundle procedures. An edge may have a concrete value or the value may be a promise (constructed by delay) to produce the value when asked. The latter provides for lazy graph structures.

```
(define (make-graph-edge label value)
  (define (get-label) label)
  (define (get-value))
```
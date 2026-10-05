```
(handle-cell-contradiction me)
'contradiction)
else
(set! strongest strongest*)
(alert-propagators! neighbors)
'content-changed)))
```

The procedure test-content! is also used to alert all cells when a premise changes its belief status. Each alerted cell checks if its strongest value has changed, requiring some action, signaling a contradiction or alerting its propagator neighbors. section 7.3.

To hide the implementation details of a cell we provide convenient access procedures:

```
(define (add-cell-neighbor! cell neighbor)
(cell 'add-neighbor! neighbor))
```

```
(define (add-cell-content! cell increment)
(parameterize ((current-reason-source cell))
(cell 'add-content! increment)))
```

```
(define (cell-strongest cell)
(cell 'get-strongest))
```

The current-reason-source parameter in add-cell-content! is part of the layer that gives a reason for every value, as described in footnote 3 on page 333. This useful feature will not be further elaborated.

# 7.2.2 Propagators

To make a propagator we supply a list of input cells, a list of output cells, and a procedure activate! to execute when alerted. The constructor introduces the propagator to its input cells with cell-neighbor!. It also alerts the new propagator that it will be run if needed.

```
(define (propagator inputs outputs activate! name)
(let ((relations make-relations name (*my-parent*)))
(define (get-inputs) inputs)
(define (get-outputs) outputs)
(define (get-relations) relations))
```
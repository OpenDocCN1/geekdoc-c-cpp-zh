given type implemented as a generic procedure that takes object as an argument and returns the value of the property.

```
(define (property-getter property type)
(let ((procedure ; the getter
(most-specific-generic-procedure
(symbol 'get- (property-name property))
1 ; arity
#f)) ; default handler
(define-generic-procedure-procedure
(match-args type)
(lambda (object))
(get-property-value property object))
procedure))
```

This shows the construction of a generic procedure with a generated name (for example get-hunger) that takes one argument, and the addition of a handler that does the actual access. The last argument for most-specific-generic-procedure is the default handler for the procedure; specifying #f that means the default is to signal an error.

We also used define-clock-handler to describe an action to take when the clock ticks. That just adds a handler to a generic procedure clock-tick!, which is already constructed.

```
(define (define-clock-handler type action)
(define-generic-procedure-handler clock-tick)
(match-args type)
(lambda (super)
(super object)
(action object)))
```

This generic procedure supports “chaining,” in which each handler gets an extra argument (in this case super) when called causes any handlers defined on the supersets of the given object to be called. The arguments passed to super have the same meaning as the arguments received here; in case there's just one argument and it is passed along. This is essentially the same mechanism used in languages such as Java, though in that it's done with a magic keyword rather than an argument.

The clock-tick! procedure is called to trigger an action, not to compute a value. Notice that the action-handler we specify will be taken after
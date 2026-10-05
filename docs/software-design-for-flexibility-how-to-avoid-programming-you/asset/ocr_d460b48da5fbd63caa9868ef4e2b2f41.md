This design provides great flexibility. There may be many different kinds of layered data, and for each there is no a priori commitment to any particular layer or number of layers. The only common feature is that each layered datum has a distinguished layer, the base-layer, which contains the object that all the other layer values are annotations on.

Each layer is represented by a bundle that embodies the specifics of that layer. The simplest is the base layer:

```
(define base-layer
(let ()
  (define (get-name) 'base)
  (define (has-value object) #t)
  (define (get-value object)
  (if layered-datum object)
    (object 'get-layer-value base-layer)
    object))
(bundle layer? get-name has-value? get-value)))
```

This shows the primary operation of a layer: the get-value operation that fetches the layer value, if present, or returns a default. In the case of the base layer, the default is itself.

The annotation layers have a little more complexity. The units layer In addition to the above, they also manage a set of named procedures that will be explored when we look at layered procedures. The make-annotation-layer procedure provides the common infrastructure used by all annotation layers; it calls its constructor argument to supply the layer-specific parts.

```
(define make-annotation-layer name constructor)
(define (get-name) name)
(define (has-value? object)
(and (layered-datum object)
  (object 'has-layer? layer)))
(define (get-value object)
  (if has-value? object)
    (object 'get-layer-value layer)
    (layer 'get-default-value))))
(define layer
(constructor get-name has-value? get-value))
layer)
```

We use make-annotation-layer to construct the units layer:
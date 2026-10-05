# 6.2.1 Layered data

A layered data item is a base value annotated with extra information about that value. The annotation is an association of layer names with their values. For example, the number 2 may be the base value in many data items: if we are dealing with tatoes there may be a 2-dollar price tag on a 2-pound bag of potatoes. Each of these instances of the number 2 must be a distinct data item, with different values (dollars or pounds) for the units. There may be other layers as well: the 2-dollar price may have information saying how it was derived from the price paid to the farmer and the cost of transportation and processing.

To address this issue we introduce the layered datum. A layered datum is represented as a bundle that contains an association of layers and their values. So a 2-pound quantity of potatoes and a 2-dollar price for potatoes will be separate layered data items:

```
(define make-layered-datum base-value alist)
  (if null? alist)
    base-value
    (let ((cons base-layer base-value)
      alist))
  (define has-layer? layer)
    (and asv alist #t))
  (define (get-layer-value layer)
    (cdr asv alist))
  (define (annotation-layers)
    (map car (cdr alist)))
  (bundle layered-datum?)
    has-layer? get-layer-value
    annotation-layers)))
```

The associations between layers and their values are represented as an association list, or alist—list of key–value pairs.

For convenience, we provide layered-datum, which takes its layer arguments in property-list form (alternating layer and value, as in the examples on page 300) and calls make-layered-datum with the corresponding alist.

```
(define layered-datum base-value . plist)
  (make-layered-datum base-value (plist->alist plist)))
```
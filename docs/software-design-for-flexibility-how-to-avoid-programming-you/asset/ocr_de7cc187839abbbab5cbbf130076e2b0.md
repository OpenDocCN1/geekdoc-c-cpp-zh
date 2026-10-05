# 6.3.1 Unit arithmetic

We need an arithmetic of units for the units annotation layer on an arithmetic. A unit specification has named base units, and an exponent for each base unit.3 In the units arithmetic, the product of unit specifications is a new unit specification where the exponent of each base unit is the sum of the exponents of the corresponding base units in the arguments.

```
(unit:* (unit 'kilogram 1 'meter 1 'second -1)
  (unit 'second -1))
(unit kilogram 1 meter 1 second -2)
```

Here we assume that the base units are just named by symbols, such as kilogram.

# Representation of unit specifications

To make it easy to create a unit specification, we represent it externally as a property list (with alternating keys and values) of base unit names and exponents.

But internally, it is convenient to represent a unit specification as a tagged list; so we must convert a raw property list to the list representation, plist->alist. We keep the lists sorted by the base unit name. In this conversion we do some error checking. The argument list to unit must be in the form of a property list. The exponent associated with each base unit must be an exact rational number (usually an integer). It is an error if a base unit is duplicated. The sort by base unit names will signal an error if the base unit name is not a symbol.

```
(define (unit . plist)
  (guarantee plist? plist 'unit)
  (let ((alist
    (sort (plist->alist plist)
      (lambda (p1 p2)
        (symbol<? (car p1) (car p2))))))
    (if (sorted-alist-repeated-key? alist)
        (error "Base unit repeated" plist)
        (for-each (lambda (p)
        (guarantee exact-rational? (cdr p))
          alist)))))
```
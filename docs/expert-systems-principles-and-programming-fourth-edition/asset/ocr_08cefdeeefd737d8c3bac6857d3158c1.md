If ?DERIVE is specified in the default attribute, then a value is derived for the slot that satisfies all of the slot attributes. If the default attribute is not specified for a slot, then it is assumed to be (default ?DERIVE). For a single-field slot, this means that a value is selected that satisfies the type, range, and allowed values attributes for the slot. The derived default value for a multifield slot will be a list of identical values that are the minimum allowed cardinality for the slot (zero by default). If one or more values are contained in the default value for a multifield slot, then each value will satisfy the type, range, and allowed values attributes for the slot. An example of derived values is the following:

```
```
CLIPS> (clear.)
CLIPS>
(deftemplate example
   (slot a)
   (slot b (type INTEGER))
   (slot c (allowed-values red green blue))
   (multislot d)
   (multislot e (cardinality 2 2)
                (type FLOAT)
                (range 3.5 10.0))))
CLIPS> (assert (example))
<Fact-0>
CLIPS> (facts)
f-0     (example (a nil)
         (b 0)
         (c red)
         (d)
         (e 3.5 3.5))
For a total of 1 fact.
CLIPS>
```
```

CLIPS guarantees only that the derived default value for a slot satisfies the constraint attributes for the slot. In other words, your programs should not depend on specific derived values (such as the symbol nil for slot a or the integer 0 for slot b in the previous example) being placed in slots. If your program depends upon a specific default value, you should use an expression with the default attribute (which will be explained shortly).

If ?NONE is specified in the default attribute, a value must be supplied for the slot when the fact is asserted. That is, there is no default value. For example,

```
```
CLIPS> (clear.)
CLIPS>
(deftemplate example
   (slot a)
   (slot b (default ?NONE))))
CLIPS> (assert (example))
```
```
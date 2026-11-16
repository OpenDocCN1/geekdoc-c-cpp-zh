```
[TMPLTRHS1] Slot b requires a value because of its
(default ?NONE) attribute.
CLIPS> (assert (example (b 1)))
<Fact-0>
CLIPS> (facts.)
f-0     (example (a nil) (b 1))
For a total of 1 fact.
CLIPS>
```

If one or more expressions are used with the default attribute, the expressions are evaluated when the slot is parsed and this value is stored in the slot whenever the value for the slot is left unspecified in an assert command. The default attribute for a single-field slot must contain exactly one expression. If no expressions are specified in the default attribute for a multifield slot, then a multifield of length zero is used for the default value. Otherwise, the return values of all of the expressions are grouped together to form one multifield value. The following is an example using expressions with the default attribute:

```
CLIPS> (clear.)
CLIPS>
(deftemplate example
   (slot a (default 3))
   (slot b (default (+ 3 4)))
   (multislot c (default a b c))
   (multislot d (default (+ 1 2) (+ 3 4))))
CLIPS> (assert (example))
<Fact-0>
CLIPS> (facts.)
f-0     (example (a 3) (b 7) (c a b c) (d 3 7))
For a total of 1 fact.
CLIPS>
```

# The Default-Dynamic Attribute

When the default attribute is used, the default value for a slot is determined when the slot definition is parsed. It's also possible to have the default value generated when the fact that will use the default value is asserted. This is done with the default-dynamic attribute. When the value of a slot that uses the default-dynamic attribute is left unspecified in an assert command, the expression specified with the default-dynamic attribute is evaluated and used for the slot's value.

As an example, let's consider the problem of deleting facts after a certain amount of time has transpired. First, we'll need some way of knowing when our facts have been asserted. The time function provided by CLIPS will be used to tag the facts with time of creation. It returns the number of seconds that have elapsed since a system-dependent reference time. By itself, the return value of
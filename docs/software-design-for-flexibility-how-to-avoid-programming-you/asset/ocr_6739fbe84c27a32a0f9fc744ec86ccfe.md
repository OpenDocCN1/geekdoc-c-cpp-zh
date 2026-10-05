base-arithmetic-packages
map-of-constant-name-to-constant
map-of-operator-name-to-operation

An arithmetic package produced by make-arithmetic has a name that is useful for debugging. It has the domain predicate noted above. It has a list of arithmetic packages, called the bases, that the new arithmetic will be built from. In addition, the arithmetic will contain a set of named constants, and a set of operators along with their corresponding operations. The final two arguments are used to generate these sets.

An example of the use of a base arithmetic is vectors. A vector is represented as an ordered sequence of coordinates: consequently an arithmetic on vectors is defined in terms of arithmetic on its coordinates. So the base arithmetic for a vector arithmetic is the appropriate arithmetic for the vector's coordinates. A vector arithmetic with numeric coordinates will use a numeric arithmetic as its base, while a vector arithmetic with symbolic coordinates will use a symbolic arithmetic as its base. For brevity, we often use the term “over” to specify the base, as in “vectors over numbers” or “vectors over symbols.”

The base armetics also define the constants and operators that the derived arithmetic will define. The defined constants will be the union of the constants defined by the bases, and the defined operators will be the union of their operators. If there are no bases, then standard sets of constant and operator names will be defined.

Using these new capabilities, we define a numeric arithmetic with applicability information. Since numeric arithmetic is built on the Scheme substrate, the appropriate handler for the operator for Scheme number arguments is just the value of the operator symbol for the Scheme implementation. Also, certain symbols, such as the identity constants for addition and multiplication, are specially mapped.

```
(define numeric-arithmetic
(make-arithmetic 'numeric number?' '()
 (lambda name) ;constant generator
 (case name
  ((additive-identity) 0)
  ((multiplicative-identity) 1)
  (else (default-object))))
```
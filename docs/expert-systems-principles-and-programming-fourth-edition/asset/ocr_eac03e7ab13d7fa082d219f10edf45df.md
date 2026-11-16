The next step in implementing certainty factors is to link the certainty factors of the facts that match the LHS of the rule to the certainty factors of the facts asserted by the RHS of the rule. In MYCIN the certainty factor associated with the LHS of a rule is derived using the following formulas:

```
CF(P1, or P2) = max { CF(P1), CF(P2) }
CF(P1, and P2) = min { CF(P1), CF(P2) }
CF(not P) = - CF(P)
```

where P, P1, and P2 represent patterns from the LHS. Additionally, if the certainty factor of the LHS is less than 0.2 the rule is considered inapplicable and will not be fired.

The certainty factor of a fact asserted from the RHS of a rule is derived by multiplying the certainty factor of the assertion by the certainty factor of the LHS of the rule. The following CLIPS rule translation of the MYCIN rule introduced at the beginning of this section demonstrates the computation of LHS and RHS certainty factors. The rule is placed in the IDENTIFY module, which imports the oav deftemplate from the OAV module:

```
defmodule IDENTIFY (import OAV deftemplate oav))
(defrule IDENTIFY::MYCIN-to-CLIPS-translation
   (oav (object organism)
        (attribute stain)
        (value grammeg)
        (CF ?C1))
   (oav (object organism)
        (attribute morphology)
        (value rod)
        (CF ?C2))
   (oav (object patient)
        (attribute is a)
        (value compromised host)
        (CF ?C3))
   (test (> (min ?C1 ?C2 ?C3) 0.2))
   =>
   (bind ?C4 (* (min ?C1 ?C2 ?C3) 0.6))
   (assert (oav (object organism)
                (attribute identity)
                (value pseudomonas)
                (CF ?C4))))
```

One final step is required for completing the MYCIN certainty factor emulation. The single combine-certainties method used by the combine-certainties rule handles only the case where both certainty factors are positive. By adding additional methods the other cases of certainty combination can be handled. The remaining combination cases are the following:
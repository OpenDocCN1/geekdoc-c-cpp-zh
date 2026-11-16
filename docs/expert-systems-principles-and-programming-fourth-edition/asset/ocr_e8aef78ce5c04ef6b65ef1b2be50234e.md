Because of the underlying algorithm used by CLIPS, the (initial-fact) pattern is added to the beginning of any and CE (implicit or explicit) whose first CE is a not CE or a test CE. Thus the rule:

```
(defrule no-emergencies
  (not (emergency))
  =>
  (printout t "No emergencies" crlf))
```

is converted to the following rule:

```
(defrule no-emergencies
  (initial-fact)
  (not (emergency))
  =>
  (printout t "No emergencies" crlf))
```

Understanding this conversion is useful when examining the output from the matches command. Also note that fact indices for not CEs are not displayed in partial matches or activations for rules. Thus the activation "f-5,+f-3" indicates that the first CE was matched by the fact with fact index 5, the second CE was a not CE that was not matched by any facts and thus is satisfied, and the third CE was matched by the fact with fact index 3.

# 8.16 THE EXISTS CONDITIONAL ELEMENT

The exists conditional element allows you to pattern match based on the existence of at least one fact that matches a pattern without regard to the total number of facts that actually match the pattern. This allows a single partial match or activation for a rule to be generated based on the existence of one fact out of a class of facts. For example, suppose an informational message should be printed whenever an emergency occurs to indicate to the plant operators that they should be on alert. The rule could be written as follows:

```
(deftemplate emergency (slot type))
(defrule operator-alert-for-emergency
  (emergency)
  =>
  (printout t "Emergency: Operator Alert" crlf)
  (assert (operator-alert))))
```

Notice what happens when more than one emergency fact is asserted—the message to the operators is printed more than once:
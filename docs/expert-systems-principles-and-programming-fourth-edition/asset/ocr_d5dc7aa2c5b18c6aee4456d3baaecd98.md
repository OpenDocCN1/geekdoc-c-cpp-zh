Since the location slot is explicitly matched against in the `create-response-team` rule object pattern, changing this slot value will produce behavior analogous to using facts:

```
CLIPS> (send [e1] put-location building-2)
<=> instance [first-response] of RESPONSE-TEAM
building-2
CLIPS> (run)
<=> instance [first-response] of RESPONSE-TEAM
CLIPS>
```

# The Initial-Object Pattern

As discussed in Sections 7.11 and 8.15, under some circumstances CLIPS will add an initial-fact pattern to the LHS of a rule. When using object pattern in a rule, however, CLIPS will under some circumstances use the initial-object pattern instead. The object equivalents of the initial-fact deftemplate and the initial-fact deffacts discussed in Section 7.10 are the INITIAL-OBJECT deffclass and the initial-object definstances:

```
(defclass INITIAL-OBJECT
   (is-a USER))
(definstances initial-object
   (initial-object of INITIAL-OBJECT))
```

If an initial-fact-initial-object pattern needs to be added at some position in a rule, an initial-fact pattern is added if the pattern preceding the insertion position is a fact pattern, otherwise if the pattern preceding the insertion point is an object pattern, then an initial-object pattern is inserted. If there is no pattern preceding the insertion point, then the pattern succeeding the insertion point is used to determine the type of pattern being added. The following format is used for the initial-object pattern:

```
(object (is-a INITIAL-OBJECT)
   (name [initial-object]))
```

Using these new rules for pattern addition, the defrule:

```
(defrule no-emergencies
   (not (object (is-a EMERGENCY)))
   =>
   (printout t "No emergencies" crlf))
```

would be converted to:

```
(defrule no-emergencies
   (object (is-a INITIAL-OBJECT)
      (name [initial-object])))
```
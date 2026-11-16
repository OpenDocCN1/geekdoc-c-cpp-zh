```
=>
(social-security-number ?ss-number))
(printout t ?ss-number crlf))
```

The print-social-security-numbers rule binds the first and middle names of the person to the variables ?first-name and ?middle-name, respectively. These variables, however, are not referred to by actions on the RHS or other pattern or slots on the LHS of the rule. Instead of using a variable, a single-field wildcard can be used when a field is required, but the value is not important. A single-field wildcard is represented by a question mark. Using single-field wildcards, the print-social-security-numbers rule can be rewritten as follows:

```
(defrule print-social-security-numbers
  (print-slot-numbers-for ?last-name)
  (person (name ? ? ?last-name)
    (social-security-number ?ss-number))
=>
  (printout t ?ss-number crlf))
```

Note that the name slot of a person fact must contain exactly three fields for the print-social-security-numbers rule to be activated. For example, the fact:

```
(person (name Joe Public)
  (social-security-number 345-89-3039))
```

would not satisfy the print-social-security-numbers rule.

Notice the importance of not including a space between the question mark and the symbolic name of a variable. The pattern:

```
(person (name ?first ?last))
```

expects two fields for the name slot, but the pattern:

```
(person (name ?first ? last))
```

expects three fields for the name slot, and the last field must be the symbol last.

When a single-field slot is left unspecified in a pattern, CLIPS automatically treats it as if there is a single-field wildcard check for that slot. For example, the pattern:

```
(person (name ?first ?last))
```

is equivalent to:

```
(person (name ?first ?last)
  (social-security-number ?))
```
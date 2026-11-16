The readline function is used to input a person's entire name as a string and the explode$ function then converts it to a multifield value that can be placed in the name slot. The read function is used to input a person's age, which can be placed in the age slot. For both input values it is possible to receive invalid values. For example, the symbol four may be input for the person's age, as the following dialog shows:

```
CLIPS> (reset).]
CLIPS> (run).]
What is your name? Fred Smith.]
What is your age? four.]
CLIPS> (facts).]
f-0 (initial-fact)
f-1 (person (name Fred Smith) (age four))
For a total of 2 facts.
CLIPS>
```

Notice that the same person fact for Fred Smith that caused a constraint violation before and was not added to the fact list has now been added to it. This is because the second level of constraint checking performed by CLIPS, dynamic constraint checking, is disabled by default. Dynamic constraint checking is performed on facts when they are actually asserted, thus catching errors that cannot be detected at parse time.

Dynamic constraint checking can be enabled or disabled using the function set-dynamic-constraint-checking and the current status of dynamic constraint checking can be determined with the get-dynamic-constraint-checking function. With dynamic constraint checking enabled, the following dialog shows how the constraint violation is handled. The Fred Smith person fact is still added to the fact list, but the constraint violation is detected and the execution of rules is halted.

```
CLIPS> (set-dynamic-constraint-checking TRUE).]
FALSE
CLIPS> (reset).]
CLIPS> (run).]
What is your name? Fred Smith.]
What is your age? four.]
[CSTRNCHK1] Slot value (Fred Smith) found in fact f-1 does not match the allowed types for slot age.
[PRCCODE4] Execution halted during the actions of deffrule create-person.
CLIPS> (facts).]
f-0 (initial-fact)
f-1 (person (name Fred Smith) (age four))
```
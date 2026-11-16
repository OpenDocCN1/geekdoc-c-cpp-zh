A single retract command can be used to retract multiple facts at once. For example, the command:

```
(retract 0 1)
```

will retract facts f-0 and f-1.

# 7.8 MODIFYING AND DUPLICATING FACTS

Slot values of deftemplate facts can be modified using the modify command. The syntax of the modify command is:

```
(modify <fact-index> <slot-modifier>+)
```

where <slot-modifier> is:

```
(<slot-name> <slot-value>)
```

For example, if John Q. Public just had a birthday, his age could be changed from 23 to 24 using the modify command.

```
CLIPS> (modify 0 (age 24)).J
<Fact-2>
CLIPS> (facts).J
f-2      (person (name "John Q. Public")
                 (age 24)
                 (eye-color blue)
                 (hair-color black))
For a total of 1 fact.
CLIPS>
```

The modify command works by retracting the original fact and then asserting a new fact with the specified slot values modified. Because of this, a new fact index is generated for a modified fact.

The duplicate command works in the same way with the exception that it does not retract the original fact. Thus, if John's long lost twin brother Jack is found, he can be added to the fact list by duplicating John's fact and changing the name slot.

```
CLIPS> (duplicate 2 (name "Jack S. Public")).J
<Fact-3>
CLIPS> (facts).J
f-2      (person (name "John Q. Public")
                 (age 24)
                 (eye-color blue)
                 (hair-color black))
```
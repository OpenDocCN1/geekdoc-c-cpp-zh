If the symbol * is given as an argument to any of the construct deletion commands, then all constructs of the appropriate type are deleted. For example, (undefrule *) would delete all defrules. The symbol * can also be used with the retract command to remove all facts.

Constructs that are referred to by other constructs cannot be deleted until the referring constructs are deleted. As the following dialog shows, the initial-fact deftemplate cannot be deleted until the initial-fact deffacts is deleted, the fact (initial-fact) is deleted, and the example defrule is deleted (which uses the default initial-fact pattern):

```
```
CLIPS> (defrule example =>)
CLIPS> (undftemplate initial-fact)
[PRNTUTIL4] Unable to delete deftemplate
    initial-fact.
CLIPS> (undeffacts initial-fact)
CLIPS> (undftemplate initial-fact)
[PRNTUTIL4] Unable to delete deftemplate
    initial-fact.
CLIPS> (undefrule example)
CLIPS> (undftemplate initial-fact)
[PRNTUTIL4] Unable to delete deftemplate
    initial-fact.
CLIPS> (retract *)
CLIPS> (undftemplate initial-fact)
CLIPS>
```
```

# Clearing All Constructs from the CLIPS Environment

The clear command can be used to remove all information contained in the CLIPS environment. It removes all constructs currently contained in CLIPS and all facts in the fact list. The syntax of the clear command is:

```
```
(clear)
```
```

After clearing the CLIPS environment, the clear command adds the initial-facts deffacts to the CLIPS environment:

```
```
CLIPS> (list-deffacts)
CLIPS> (list-deftemplates)
environment
response
start-fact
For a total of 3 deftemplates.
CLIPS> (clear)
CLIPS> (list-deffacts)
initial-fact
For a total of 1 deffacts.
```
```
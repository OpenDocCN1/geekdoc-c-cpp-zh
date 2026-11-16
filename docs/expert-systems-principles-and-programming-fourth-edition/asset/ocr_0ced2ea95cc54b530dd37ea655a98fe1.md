```
CLIPS> (ppdefrule RECOVERY::example1)
(defrule RECOVERY::example1
==>
CLIPS> (ppdefrule DETECTION::example1)
(defrule DETECTION::example1
==>
CLIPS>
```

The following commands allow the module to be specified as part of the construct name: ppdefrule, undefrule, ppdeftemplate, undeftemplate, ppdeffacts, undeffacts, matches, refresh, remove-break, and set-break.

# 9.7 IMPORTING AND EXPORTING FACTS

You have learned how to partition constructs by placing them in separate modules. Facts themselves can also be partitioned. Asserted facts are automatically associated with the module in which their corresponding deftemplates are defined. For example:

```
CLIPS>
(deftemplate DETECTION::fault
(slot component))
CLIPS> (assert (fault (component A)))
<Fact-0>
CLIPS> (facts)
f-0 (fault (component A))
For a total of 1 fact.
CLIPS>
(deftemplate ISOLATION::possible-failure
(slot component))
CLIPS> (assert (possible-failure (component B)))
<Fact-1>
CLIPS> (facts)
f-1 (possible-failure (component B))
For a total of 1 fact.
CLIPS> (set-current-module DETECTION)
ISOLATION
CLIPS> (facts)
f-0 (fault (component A))
For a total of 1 fact.
CLIPS>
```

Notice that in the ISOLATION module the only fact listed is the possible-failure fact, whose corresponding deftemplate is contained in the ISOLATION module. The same is true for the fault fact in the DETECTION module.

The facts command, like the list-defrules and similar commands, can accept a module name as an optional argument. The syntax for the facts command is:
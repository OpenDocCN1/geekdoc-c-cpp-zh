
with the exact same combination of fact identifiers. Identical sets of fact identifiers must match one-for-one in both order and fact indices. Examples later in this chapter will show how a single fact can match a pattern in more than one way. In this case, several activations with the same set of fact identifiers for a single rule can be placed on the agenda, one for each distinct match.

Alternatively, the refresh command can be used to make the rule fire again. The refresh command places all activations that have already fired for a rule back on the agenda (with the restriction that the facts that triggered the activation are still present in the fact list). The syntax of the refresh command is:

```
(refresh <rule-name>)
```

and the following commands show how the refresh command could be used to reactivate the fire-emergency rule:

```
CLIPS> (agenda)
CLIPS> (refresh fire-emergency)
CLIPS> (agenda)
0 fire-emergency: f-1
For a total of 1 activation.
CLIPS>
```

### Watching Activations, Rules, and Statistics

If activations are being watched, CLIPS will automatically print a message whenever an activation has been added to or removed from the agenda. As with facts, the character sequence ==> indicates that an activation is being removed from the agenda and the character sequence ===> indicates that an activation is being added to the agenda. After the initial command sequence the activation is printed with the same format used by the agenda command. The following command sequence illustrates activations being watched:

```
CLIPS> (reset)
CLIPS> (watch activations)
CLIPS> (assert (emergency (type fire)))
==> Activation 0 fire-emergency: f-1
<Fact-1>
CLIPS> (agenda)
0 fire-emergency: f-1
For a total of 1 activation.
CLIPS> (retract 1)
==> Activation 0 fire-emergency: f-1
CLIPS> (agenda)
CLIPS>
```

If rules are being watched, CLIPS will print a message whenever a rule is fired. The following command sequence illustrates activations and rules being watched:

```
CLIPS> (reset)
CLIPS> (watch rules)
CLIPS> (assert (emergency (type fire)))
==> Activation 0 fire-emergency: f-1
<Fact-1>
CLIPS> (run)
FIRE 1 fire-emergency: f-1
CLIPS> (agenda)
CLIPS>
```

The number following the symbol FIRE indicates how many rules have fired since the run command was given. For example, if another rule were to fire after the fire-emergency rule, it would be preceded by “FIRE 2.” After the firing order is printed the name of the rule is printed, followed by the fact indices that matched the patterns of the rule. Note that watching activations will not cause a message to be displayed when a rule is fired (and hence removed from the agenda).

It's possible to watch specific rules and activations by specifying one or more rule names at the end of a watch command. For example, (watch activations fire-emergency) would just display activation messages for the fire-emergency rule.

If statistics are being watched, CLIPS will print informational messages such as the following at the completion of a run:

```
CLIPS> (unwatch all)
CLIPS> (reset)
CLIPS> (watch statistics)
CLIPS> (assert (emergency (type fire)))
<Fact-1>
CLIPS> (run)
1 rules fired         Run time is 0.02 seconds
50.0 rules per second
3 mean number of facts (3 maximum)
1 mean number of instances (1 maximum)
1 mean number of activations (1 maximum)
CLIPS> (unwatch statistics)
CLIPS>
```

When statistics are watched, six statistics are printed out after a run command. First displayed are the total number of rules fired, the amount of time in seconds it took to fire the rules, and the average number of rules fired per second (the first statistic divided by the second statistic). In addition, for each cycle of execution, CLIPS keeps statistics on the number of facts, activations, and instances. The mean number of facts is the sum of the total number of facts in the fact list after each rule firing divided by the number of rules fired. The number contained within the parentheses followed by the word maximum indicates the largest number of facts contained in the fact list for any one rule firing. Similarly, the mean and maximum numbers of activations statistics indicate the average number of activations per rule firing and the largest number of activations on the agenda for any one rule firing. The mean and maximum numbers of instances display information associated with COOL.

## 7.13 COMMANDS FOR MANIPULATING CONSTRUCTS

### Displaying the List of Members of a Specified Construct

The list-defrules command is used to display the current list of rules maintained by CLIPS. Similarly, the list-deftemplates and list-deffacts commands, respectively can be used to display the current list of deftemplates or the current list of deffacts. The syntax of these commands is:

```
(list-defrules)
(list-deftemplates)
(list-deffacts)
```

For example,

```
CLIPS> (list-defrules)
fire-emergency
For a total of 1 rule.
CLIPS> (list-deftemplates)
initial-fact
emergency
response
For a total of 3 deftemplates.
CLIPS> (list-deffacts)
initial-fact
For a total of 1 deffacts.
CLIPS>
```

### Displaying the Text Representation of a Specified Construct Member

The ppdefrule (pretty print defrule), ppdeftemplate (pretty print deftemplate), and ppdeffacts (pretty print deffacts) commands are used to display the text representations of a defrule, a deftemplate, and a deffacts respectively. The syntax of these commands is:

```
(ppdefrule <defrule-name>)
(ppdeftemplate <deftemplate-name>)
(ppdeffacts <deffacts-name>)
```

The single argument for each command specifies the name of the defrule, deftemplate, or deffacts to be displayed. When displayed, CLIPS puts different parts of the constructs on different lines for the sake of readability. For example,

```
CLIPS> (ppdefrule fire-emergency)
(defrule MAIN::fire-emergency "An example rule"
   (emergency (type fire))
   =>
   (assert (response
      (action activate-sprinkler-system)))))
CLIPS> (ppdeftemplate response)
(deftemplate MAIN::response
   (slot action))
CLIPS> (ppdeffacts initial-fact)
CLIPS> (deffacts start-fact (start-fact))
CLIPS> (ppdeffacts start-fact)
(deffacts MAIN::start-fact
   (start-fact))
CLIPS>
```

The symbol MAIN:: preceding each of the construct names indicates the module in which the constructs have been placed. Modules provide a mechanism for partitioning a knowledge base and will be discussed in greater detail in Chapter 9. Notice that the initial-fact deffacts has no text representation (since it is automatically created by CLIPS). However, the start-fact deffacts that was entered does have a text representation.

### Deleting a Specified Construct Member

The undefrule, undeftemplate, and undeffacts commands are used to delete a defrule, a deftemplate, and a deffacts, respectively. The syntax of these commands is:

- (undefrule <defrule-name>)
- (undeftemplate <deftemplate-name>)
- (undeffacts <deffacts-name>)

The single argument for each command specifies the name of the defrule, deftemplate, or deffacts to be deleted. For example,

```
CLIPS> (undeffacts start-fact)
CLIPS> (list-deffacts)
initial-fact
For a total of 1 deffacts.
CLIPS> (undefrule fire-emergency)
CLIPS> (list-defrules)
CLIPS>
```

Notice that the initial-fact deffacts and the initial-fact deftemplate can be deleted just like any other user-defined construct. If a reset command were performed now, the (initial-fact) fact would not be added to the fact list.

If the symbol * is given as an argument to any of the construct deletion commands, then all constructs of the appropriate type are deleted. For example, (undefrule *) would delete all defrules. The symbol * can also be used with the retract command to remove all facts.

Constructs that are referred to by other constructs cannot be deleted until the referring constructs are deleted. As the following dialog shows, the initial-fact deftemplate cannot be deleted until the initial-fact deffacts is deleted, the fact (initial-fact) is deleted, and the example defrule is deleted (which uses the default initial-fact pattern):

```
CLIPS> (defrule example =>)
CLIPS> (undeftemplate initial-fact)
[PRNTUTIL4] Unable to delete deftemplate
    initial-fact.
CLIPS> (undeffacts initial-fact)
CLIPS> (undeftemplate initial-fact)
[PRNTUTIL4] Unable to delete deftemplate
    initial-fact.
CLIPS> (undefrule example)
CLIPS> (undeftemplate initial-fact)
[PRNTUTIL4] Unable to delete deftemplate
    initial-fact.
CLIPS> (retract *)
CLIPS> (undeftemplate initial-fact)
CLIPS>
```

### Clearing All Constructs from the CLIPS Environment

The clear command can be used to remove all information contained in the CLIPS environment. It removes all constructs currently contained in CLIPS and all facts in the fact list. The syntax of the clear command is:

```
(clear)
```

After clearing the CLIPS environment, the clear command adds the initial-fact deffacts to the CLIPS environment:

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

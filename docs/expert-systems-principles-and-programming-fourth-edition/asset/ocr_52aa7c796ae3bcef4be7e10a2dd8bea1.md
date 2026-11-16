```
```
(defrule fire-third
   (priority third)
   =>
   (printout t "Print third" crlf))
```
```

The order in which the rules fire depends on the order in which the facts that satisfy the CEs in the LHS of the rules are asserted. For example, if the rules are entered, the following commands will produce the output shown below:

```
```
CLIPS> (unwatch all.)
CLIPS> (reset.)
CLIPS> (assert (priority first))]
<Fact-1>
CLIPS> (assert (priority second))]
<Fact-2>
CLIPS> (assert (priority third))]
<Fact-3>
CLIPS> (run.)
Print third
Print second
Print first
CLIPS>
```
```

Notice the order of output statements. First “Print third” is printed, then “Print second,” and finally “Print first.” The first fact (priority first) activates the rule fire-first. When the second fact is asserted, it activates the rule fire-second, which is stacked on top of the activation for rule fire-first. Finally, the third fact is asserted and its activated rule, fire-third, is stacked on top of the activation for rule fire-second.

In CLIPS, rules of equal salience that are activated by different patterns are prioritized based on the stack order of facts. Rules are fired from the agenda from the top of the stack down. So rule fire-third is fired first because it’s on the top of the stack, then rule fire-second, and finally rule fire-first. If the order in which the facts are asserted is reversed, then the order in which the rules are fired will also be reversed. This is seen in the following output:

```
```
CLIPS> (reset.)
CLIPS> (assert (priority third))]
<Fact-1>
CLIPS> (assert (priority second))]
<Fact-2>
CLIPS> (assert (priority first))]
<Fact-3>
CLIPS> (run.)
Print first
Print second
Print third
CLIPS>
```
```
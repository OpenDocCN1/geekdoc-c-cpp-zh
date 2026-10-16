Next, we have our case statements in a sequence. These are also called case labels and are used for indicating whether the variable matches the case statement value and that the block of code is where the execution flow will go.

One important thing to note is that the execution flow will go into one case label exactly so there will never be a situation where two or more case blocks are executed.

At the end of every case block, there must be the break keyword; this is what sends the flow outside the switch statement and on to the next code section. Notice that we also have a label of default. This is used to indicate that if no other case label works, the flow should be directed here. You don’t have to have the default label last but it tends to be the place where it is used most commonly and it is the best practice. This is because the default block catches anything that isn’t a specific situation for the case labels. In addition, this also takes the place of the last else block in the original long if statement.

Note that case conditions in switch statements do not take general logic. An if statement could be this:

```
if(x < 10)
```

However, you can’t do this:

```
case x < 10:
```

and you can’t do this either:

```
case < 10:
```

If you want complicated logic, go back to using an if statement instead.

# Types Used with Switch Statements

In the example above, we used the int type. While many types can be used in switch statements, not all of them can. Those that can include:

+   - bool
+   - char
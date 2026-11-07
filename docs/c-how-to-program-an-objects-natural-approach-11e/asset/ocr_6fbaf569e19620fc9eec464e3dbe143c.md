# 3.10.4 Top-Down, Stepwise Refinement: Second Refinement

The pseudocode statement

```
initialize variables
```

can be refined as follows:

```
initialize passes to zero
initialize failures to zero
initialize student counter to one
```

Notice that only the counters are initialized at the start of the algorithm.

The pseudocode statement

```
input the 10 exam results, and count passes and failures
```

requires a loop that successively inputs the result of each exam. We know in advance that there are precisely 10 exam results, so counter-controlled looping is appropriate. Inside the loop (i.e., nested within the loop), a double-selection structure will determine whether each exam result is a pass or a failure, then increment the appropriate counter. The preceding pseudocode statement can be refined as follows:

```
while student counter is less than or equal to 10
    prompt the user to enter the next exam result
    input the next exam result

    if the student passed
        add one to passes
    else
        add one to failures

    add one to student counter
```

We use blank lines to isolate the nested *if…else* statement, which improves readability.

The pseudocode statement

```
print a summary of the exam results and decide whether a bonus should be paid
```

can be refined as follows:

```
print the number of passes
print the number of failures
if more than eight students passed
    print “Bonus to instructor!”
```

# 3.10.5 Complete Second Refinement of the Pseudocode

Here we show the complete second refinement. This pseudocode is now sufficiently refined for conversion to C++.

```
1  initialize passes to zero
2  initialize failures to zero
3  initialize student counter to one
4
```

*(continued on next page)*
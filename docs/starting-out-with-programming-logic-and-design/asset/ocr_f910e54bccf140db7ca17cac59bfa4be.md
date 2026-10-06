# The For Loop

General format:

```
For counterVariable = startingValue To maxValue
statement
statement // These statements are the body of the loop.
statement
etc.
End For
```

In the general format, counterVariable is the name of a variable that is used as a counter, startingValue is the value of the counter that will be initially set to, and maxValue is the maximum value that the counter can contain. When the loop executes, the following actions are performed:

+   1. The counter is set to the startingValue.
2. The counter is compared to the maxValue. If the counterVariable is greater than maxValue, the loop stops. Otherwise:
   a. the statements that appear in the body of the loop are executed.
   b. The counter is incremented.
   c. The loop starts over again at step 2.

Here is an example:

```
For counter = 1 To 10
Display "Hello world"
End For
```

# The For Each Loop

General format:

```
For Each var In array
statement
statement
statement
etc.
End For
```

In the general format, var is the name of a variable and array is the name of an array. The loop will iterate once for every element in the array. Each time the loop iterates, it copies an element to the var variable. For example, the first time the loop iterates, var will contain the value of array[0], the second time the loop iterates will contain the value of array[1], and so forth. This continues until the loop has stopped through all elements of the array. The following pseudocode shows an example:

```
Constant INTEGER SIZE = 5
Declare Integer numbers[SIZE] = 5, 10, 15, 20, 25
Declare Integer num
For Each num In numbers
Display num
End For
```
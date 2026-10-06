# Checkpoint

5.19 A program that calculates the total of a series of numbers typically has what
two elements?

5.20 What is an accumulator?

5.21 Should an accumulator be initialized to any specific value? Why or why not?

5.22 Look at the following pseudocode. If it were a real program, what would it
display?

```
Declare Integer number1 = 10, number2 = 5
Set number1 = number1 + number2
Display number1
Display number2
```

5.23 Look at the following pseudocode. If it were a real program, what would it
display?

```
Declare Integer counter, total = 0
For counter = 1 To 5
Set total = total + counter
End For
Display total
```

# Sentinels

> CONCEPT: A sentinel is a special value that marks the end of a list of values.

Consider the following scenario: You are designing a program that will use a loop to
process a list of values. At the time you are designing the program, you do not\know the number of values that will be in the list. In fact, the number of values in the
list could be different each time the program is executed. What is the best way to\esign such a loop? Here are some techniques that you have seen already in this chap-	er, with the disadvantages of using when processing a list of values:

+   - Ask the user, at the end of each loop iteration, there is another
value to process. If the list of values is long, asking this question at the
of each loop iteration might make the program cumbersome for the user.
- Ask the user at the beginning of the program how many items the list contains.
This might also inconvenience the user, however. If the list is very long, and the
user does not know the number of items in the list, it will require the user to
count them.

When processing a long list of values with loop, perhaps a better technique is to use
tinel. A sentinel is a special value that marks the end of a list of items. When a
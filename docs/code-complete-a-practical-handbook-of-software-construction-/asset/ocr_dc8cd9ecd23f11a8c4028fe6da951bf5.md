First, in comments, write the steps the body of the loop needs to perform. It’s easier to write down what needs to be done when you’re not thinking about details of syntax, loop indexes, array indexes, and so on.

```
**Step 1: Creating a Loop from the Inside Out (Pseudocode Example)**

```text
-- get rate from table
-- add rate to total
```
```

Second, convert the comments in the body of the loop to code, as much as you can without actually writing the whole loop. In this case, get the rate for one person and add it to the overall total. Use concrete, specific data rather than abstractions.

> *table* doesn’t have any indexes yet.

```
**Step 2: Creating a Loop from the Inside Out (Pseudocode Example)**

```text
rate = table[ ]
totalRate = totalRate + rate
```
```

The example assumes that *table* is an array that holds the rate data. You don’t have to worry about the array indexes at first. *rate* is the variable that holds the rate data selected from the rate table. Likewise, *totalRate* is a variable that holds the total of the rates.

Next, put in indexes for the *table* array:

```
**Step 3: Creating a Loop from the Inside Out (Pseudocode Example)**

```text
rate = table[ census.Age ][ census.Gender ]
totalRate = totalRate + rate
```
```

The array is accessed by age and sex, so *census.Age* and *census.Gender* are used to index the array. The example assumes that *census* is a structure that holds information about people in the group to be rated.

The next step is to build a loop around the existing statements. Since the loop is supposed to compute the rates for each person in a group, the loop should be indexed by person.

```
**Step 4: Creating a Loop from the Inside Out (Pseudocode Example)**

```text
For person = firstPerson to lastPerson
    rate = table[ census.Age, census.Gender ]
    totalRate = totalRate + rate
End For
```
```

All you have to do here is put the *for* loop around the existing code and then indent the existing code and put it inside a *begin-end* pair. Finally, check to make sure that the variables that depend on the *person* loop index have been generalized. In this case, the *census* variable varies with *person*, so it should be generalized appropriately.
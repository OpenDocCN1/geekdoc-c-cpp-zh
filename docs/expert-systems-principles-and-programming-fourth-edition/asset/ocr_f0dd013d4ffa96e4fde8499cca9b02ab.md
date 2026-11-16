Calling preview-generic with just the question string parameter shows that with all the parameters equal in other ways, the query restriction on method #2 gives it higher precedence than the other applicable method, #5:

```
CLIPS>
(preview-generic check-input "Pick a number").]
check-input #5 () (?$ <gry>)
check-input #1 () S?
CLIPS>
```

Let's look at another situation where an endless loop can occur with the check-input generic function:

```
CLIPS> (check-input "Pick a number" 3 1).]
Pick a number (3-1) 3
Pick a number (3-1) 2
Pick a number (3-1) 1
Pick a number (3-1) 0
.
.
.
```

In this situation, the applicable method is #2, the one with the question string parameter and two integer parameters. Since no integer exists that is greater or equal to 3 and less than or equal to 1, the user can never supply a value to satisfy the generic function. We could solve this problem by creating an additional method with a query restriction that detected the upper limit is less than the lower limit:

```
(defmethod check-input ((?question STRING)
(?value1 INTEGER)
(?value2 INTEGER)
(< ?value2 ?value1)))
(return FALSE))
```

This method just returns the symbol FALSE if it detects the ranges are reversed. We could go a step further and simply switch the values of the ranges. One way to do this would be to duplicate the code but switch the variables at the appropriate places:

```
(defmethod check-input ((?question STRING)
(?value1 INTEGER)
(?value2 INTEGER)
(< ?value2 ?value1)))
```
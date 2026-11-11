of the program cannot depend on which statement is chosen (among those associated with true Boolean expressions). If none of the Boolean expressions are true, a run-time error occurs that causes program termination. This forces the programmer to consider and list all possibilities. Consider the following example:

```
```text
if i = 0 -> sum := sum + i
[] i > j -> sum := sum + j
[] j > i -> sum := sum + i
fi
```
```

If i = 0 and j > i, this statement chooses nondeterministically between the first and third assignment statements. If i is equal to j and is not zero, a run-time error occurs because none of the conditions are true.

This statement can be an elegant way of allowing the programmer to state that the order of execution, in some cases, is irrelevant. For example, to find the largest of two numbers, we can use

```
```text
if x >= y -> max := x
[] y >= x -> max := y
fi
```
```

This computes the desired result without overspecifying the solution. In particular, if x and y are equal, it does not matter which we assign to max. This is a form of abstraction provided by the nondeterministic semantics of the statement.

Now, consider this same process coded in a traditional programming language selector:

```
```text
if (x >= y)
    max = x;
else
    max = y;
```
```

This could also be coded as follows:

```
```text
if (x > y)
    max = x;
else
    max = y;
```
```

There is no practical difference between these two statements. The first assigns x to max when x and y are equal; the second assigns y to max in the same circumstance. This choice between the two statements complicates the formal analysis of the code and the correctness proof of it. This is one of the reasons why guarded commands were developed by Dijkstra.
The append predicate can also be used to create other list operations, such as the following, whose effect we invite the reader to determine. Note that list_op_2 is meant to be used by providing a list as its first parameter and a variable as its second, and the result of list_op_2 is the value to which the second parameter is instantiated.

```
list_op_2([], []).
list_op_2([Head | Tail], List) :- 
list_op_2(Tail, Result), append(Result, [Head], List).
```

As you may have been able to determine, list_op_2 causes the Prolog system to instantiate its second parameter with a list that has the elements of the list of the first parameter, but in reverse order. For example, ([apple, orange, grape], Q) instantiates Q with the list [grape, orange, apple].

Once again, although the LISP and Prolog languages are fundamentally different, similar operations can use similar approaches. In the case of the reverse operation, both the Prolog's list_op_2 and LISP's reverse function include the recursion-terminating condition, along with the basic process of appending the reversal of the CDR or tail of the list to the CAR or head of the list to create the result list.

The following is a trace of this process, now named reverse:

```
trace.
reverse([a, b, c], Q).
```

```
(1) 1 Call: reverse([a, b, c], _6)?
(2) 2 Call: reverse([b, c], _65636)?
(3) 3 Call: reverse([c], _65646)?
(4) 4 Call: reverse([], _65656)?
(4) 4 Exit: reverse([], [])
(5) 4 Call: append([], [c], _65646)?
(5) 4 Exit: append([], [c], [c])
(3) 3 Exit: reverse([c], [c])
(6) 3 Call: append([c], [b], _65636)?
(7) 4 Call: append([], [b], _25)?
(7) 4 Exit: append([], [b], [b])
(6) 3 Exit: append([c], [b], [c, b])
(2) 2 Exit: reverse([b, c], [c, b])
(8) 2 Call: append([c, b], [a], _6)?
(9) 3 Call: append([b], [a], _32)?
(10) 4 Call: append([], [a], _39)?
(10) 4 Exit: append([], [a], [a])
(9) 3 Exit: append([b], [a], [b, a])
(8) 2 Exit: append([c, b], [a], [c, b, a])
(1) 1 Exit: reverse([a, b, c], [c, b, a])
```

```
Q = [c, b, a]
```
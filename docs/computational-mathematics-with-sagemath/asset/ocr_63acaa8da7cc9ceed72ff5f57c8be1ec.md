The very extensive Python library `re` may also be used to search sub-strings, words and regular expressions.

# ### 3.3.6 Shared or Duplicated Data Structures

A list in square brackets `[...]` can be modified by assigning some of its elements, by a change of the number of elements, or by methods like `sort` or `reverse`.

Assigning a list to a variable does not duplicate the data structure, which is shared. In the following example the lists L1 and L2 remain identical: they correspond to two aliases of the same object, and modifying one of them is visible on the other one:

```
~~~
sage: L1 = [11, 22, 33] ; L2 = L1
sage: L1[1] = 222 ; L2.sort() ; L1, L2
([11, 33, 222], [11, 33, 222])
sage: L1[2:3] = [] ; L2[0:0] = [6, 7, 8]
sage: L1, L2
([6, 7, 8, 11, 33], [6, 7, 8, 11, 33])
~~~
```

In contrast, the `map`, `filter` and `flatten` functions duplicate the data structures; so do the list construction by `L[p:q]` or `[...for..if...]`, and the concatenation by `+` and `*`.

In the above example, replacing on the first line `L2 = L1` by one of the next six commands completely changes the following results, since modifications on one list do not propagate to the other one. The two structures become independent, the two lists are distinct even if they have the same value; for example the assignment `L2 = L1[:]` copies the sub-list of L1 from the first to last term, and thus fully duplicates the structure of L1:

```
~~~
L2 = [11, 22, 33]    L2 = copy(L1)    L2 = L1[:]
L2 = []+L1           L2 = L1+[]       L2 = 1*L1
~~~
```

Checking for shared data structures can be done in Sage using the `is` binary operator; if the answer is true, all modifications will have a side effect on both variables:

```
~~~
sage: L1 = [11, 22, 33] ; L2 = L1 ; L3 = L1[:]
sage: [L1 is L2, L2 is L1, L1 is L3, L1 == L3]
[True, True, False, True]
~~~
```

Copy operations on lists operate on one level only. As a consequence, modifying an element in a list of lists has a side effect despite the list copy at the outer level:

```
~~~
sage: La = [1, 2, 3] ; L1 = [La, L2] ; L2 = copy(L1)
sage: L1[1][0] = 5          # [1, [5, 2, 3]] for L1 and L2
sage: [L1 == L2, L1 is L2, L1[1] is L2[1]]
[True, False, True]
~~~
```

The following instruction duplicates a list on two levels:
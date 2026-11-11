As another example, consider the problem of determining whether two given lists are equal. If the two lists are simple, the solution is relatively easy, although some programming techniques with which the reader may not be familiar are involved. A predicate function, `equalsimp`, for comparing simple lists is shown here:

```
```
(DEFINE (equalsimp list1 list2)
    (COND
        ((NULL? list1) (NULL? list2))
        ((NULL? list2) #F)
        ((EQ? (CAR list1) (CAR list2))
            (equalsimp (CDR list1) (CDR list2)))
        (ELSE #F)
    )
)
```
```

The first case, which is handled by the first parameter to `COND`, is for when the first list parameter is the empty list. This can occur in an external call if the first list parameter is initially empty. Because a recursive call uses the `CDRs` of the two parameter lists as its parameters, the first list parameter can be empty in such a call (if the first list parameter is now empty). When the first list parameter is empty, the second list parameter must be checked to see whether it is also empty. If so, they are equal (either initially or the `CARs` were equal on all previous recursive calls), and `NULL?` correctly returns `#T`. If the second list parameter is not empty, it is larger than the first list parameter and `#F` should be returned, as it is by `NULL?`.

The next case deals with the second list being empty when the first list is not. This situation occurs only when the first list is longer than the second. Only the second list must be tested, because the first case catches all instances of the first list being empty.

The third case is the recursive step that tests for equality between two corresponding elements in the two lists. It does this by comparing the `CARs` of the two nonempty lists. If they are equal, then the two lists are equal up to that point, so recursion is used on the `CDRs` of both. This case fails when two unequal atoms are found. When this occurs, the process need not continue, so the default case `ELSE` is selected, which returns `#F`.

Note that `equalsimp` expects lists as parameters and does not operate correctly if either or both parameters are atoms.

The problem of comparing general lists is slightly more complex than this, because sublists must be traced completely in the comparison process. In this situation, the power of recursion is uniquely appropriate, because the form of sublists is the same as that of the given lists. Any time the corresponding elements of the two given lists are lists, they are separated into their two parts, `CAR` and `CDR`, and recursion is used on them. This is a perfect example of the usefulness of the divide-and-conquer approach. If the corresponding elements of the two given lists are atoms, they can simply be compared using `EQ?`.